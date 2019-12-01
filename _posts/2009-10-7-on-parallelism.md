---
layout: post
title: On Parallelism in Gajure
post_date: 7 October, 2009 -- Charlottesville, VA
---

Recently, I read about some experiments in [parallel genetic
programming](http://jan.rychter.com/enblog/2009/8/26/experiments-with-parallel-genetic-programming-in-clojure.html),
and I decided to run my own with
[Gajure](http://github.com/Ejhfast/Gajure). Since I wrote Gajure in
Clojure, I added parallelism without difficulty. All I needed was to
change out a few of my *map* functions with *pmap*, its parallel
counterpart. This took literally a few seconds as the core
selection function *roulette-select* changed by two characters:

<pre>
(defn roulette-select  
    “Select num individuals from pop, with an individual’s  
    fitness porportional to selection likelihood.”  
    [pop fit-fn num]  
        (let [pop-fits (pmap fit-fn pop)  
              inc-fits (iterate (fn [[pfit idx]]  
                                        [(+ (nth pop-fits (+ idx 1)) 
                                            pfit) 
                                         (+ idx 1)])  
                                [(first pop-fits) 0])  
              max-fitness (apply + pop-fits)  
              pick-one (fn [num] (second (first 
                                            (drop-while  
                                                #(< (first %) num)  
                                                inc-fits))))]  
        (pmap (fn \[x\] (nth pop (pick-one (rand-int max-fitness))))  
              (range num))))
</pre>

A genetic algorithm seems a perfect target for parallelism. Within a
given generation, we can independently run fitness computations and
mutation operations for each population member. But performance gains
did not accrue. At least, not on my dual-core machine.

So what happened? The running time to evolve “helloworld” more than
doubled. What previously took 1450ms takes 3162ms with the parallel
implementation. Probably, the overhead involved in creating parallel
mappings outweighs any other benefits, given that I only have two
processors[^1]. I except the triviality of the problem space also
contributes. In an ideal use-case, each fitness evaluation would do more
work. I’ve committed the *pmap* changes to github under a [separate
branch](http://github.com/Ejhfast/Gajure/tree/parallel).

[^1]: Would this change if threads were more lightweight?
