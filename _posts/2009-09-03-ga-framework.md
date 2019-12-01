---
layout: post
title: A Genetic Algorithm Framework in Clojure
post_date: 13 September, 2009 -- Charlottesville, VA
---

[Gajure:](http://github.com/Ejhfast/Gajure) is a framework for constructing
genetic algorithms in Clojure. Genetic algorithms apply an evolutionary model to complex problems, and
so evolve solutions from an initial population of random states. Eliding
a few details, the process boils down (in lisp notation) to this:

<pre>
(defn genetic-algorithm [some-params]  
    (initialize-population)  
        (loop (generations-that-remain)  
            (if (no-generations-left)  
                (print-stuff-and-exit)  
                (pass-again-to-loop  
                    (mutate-population  
                        (crossover-population  
                            (select-population  
                                (population))))))
</pre>

We want to construct an algorithm that accepts functions for
initializing, sorting, crossing over and mutating population members. It
should also take population parameters (e.g. the number of generations
to run, or the mutation rate). Here’s what I came up with:

<pre>
(defn run-ga [func-map setting-map]  
    (let [ipop ((:init-fn func-map) (:pop-sz setting-map))]  
            (loop [pop ipop num (:gen setting-map)]  
            (if (zero? num)  
                (do (println 
                        (first (sort-by 
                                (:fit-fn func-map) > pop ))))  
                (let [total-left (- (:pop-sz setting-map) 
                                    (:children setting-map))]  
                        (do (println 
                            (first (sort-by 
                                        (:fit-fn func-map) 
                                        > 
                                        pop))))  
                        (recur 
                        (concat  
                            ((:mut-fn func-map)  
                                (do-crossover  
                                    ((:sel-fn func-map)  
                                        pop  
                                        (:fit-fn func-map)  
                                        (* (:children setting-map) 
                                            2))  
                                    (:cross-fn func-map)  
                                    2)  
                            (:mut-r setting-map))  
                        ((:init-fn func-map) total-left))  
                        (dec num)))))))
</pre>

This function follows the basic algorithm I laid out earlier. It takes
as input two maps, *func-map* and *setting-map*, which provide
problem-specific functions and settings. The helper-function
*do-crossover* takes a list of parents, and runs a problem-specific
crossover function provided as one of the parameters. All this code
lives on [github](http://github.com/Ejhfast/Gajure), but I’ll display it
here as well.

<pre>
(defn do-crossover [p-list cross-fn num-parents]  
    (map cross-fn (partition num-parents p-list)))
</pre>

Let’s consider an example problem: evolving the string *“helloworld”*.
First we need to define some aspects of the problem space. Simple
enough. The ‘DNA’ of a string is nothing but a list of characters:

<pre>
(def dna (map str  
    [’q ’w ’e ’r ’t ’y ’u ’i ’o ’p ’a ’s ’d ’f ’g ’h ’j ’k ’l  
    ’z ’x ’c ’v ’b ’n ’m]))
</pre>

I wrote a few other helper functions, *rand-from-list* and *rand-pop*,
which are generally useful for creating random populations. The first
will return a ‘random’ list from a list of elements, made up of the
elements in that list. The second will return a list of these random
lists.

<pre>
(defn rand-from-list [lst num]  
    (let [total-el (count lst)]  
        (map (fn [x] (nth lst (rand-int total-el))) (range 0 num))))
</pre>

And the other:

<pre>
(defn rand-pop [lst num num-pop]  
    (map (fn [x] (rand-from-list lst num)) (range 0 num-pop)))
</pre>

Let’s apply them to dna. A function that initializes a random population
of strings might look like this (supposing we limit our population to
strings of 10 characters):

<pre>
(defn some-strings [num]  
    (rand-pop dna 10 num))
</pre>

This is not precisely what I do in my github example (I end up using a
partial) but it is effectively the same thing. On to crossover:

<pre>
(defn list-crossover [[s1 s2]]  
    (let [point (rand-int  
                    (min (count s1)  
                    (count s2)))]  
        (concat (take point s1)  
        (drop point s2))))
</pre>

The function *list-crossover* chooses a cross-point, x, on two lists,
and creates a new list made up of the first x elements of one list, and
the last (length – x) elements of the other. Now mutation:

<pre>
(defn generic-mutation [list prob]  
    (map  
        (fn [s-list]  
        (map  
            (fn [test]  
                (if (> prob (rand-int 100))  
                (let [r-s (rand-int (count list))  
                      r-t (rand-int (count (nth list r-s)))]  
                    (nth (nth list r-s) r-t))  
                test))  
            s-list))  
    list))
</pre>

Mutation is difficult to make ‘generic,’ but *generic-mutation* uses the
base elements of other population members as an approximation for all
the ‘genetic material’ that can be swapped in or out of a mutated
member.

These functions work on most kinds of list populations, but you may need
more complex behavior, so I abstracted them away from the algorithm
itself.

Although nearly done, we still lack what is perhaps the most important
part of the GA: the fitness function. For this example, I use a system
of one point for every directly matching character in the string. As
follows:

<pre>
(defn hello-fitness [lst]  
(reduce  
    +  
    (map #(if (= %1 %2) 1 0)  
        lst  
        ’(“h” “e” “l” “l” “o” “w” “o” “r” “l” “d”))))
</pre>

So now we can define the maps:

<pre>
(def func-map {:fit-fn hello-fitness 
               :mut-fn generic-mutation  
               :sel-fn roulette-select 
               :init-fn (partial rand-pop dna 10)  
               :cross-fn list-crossover})  
(def set-map {:pop-sz 100 :children 50 :mut-r 1 :gen 100})
</pre>

Note that *roulette-select* is another framework helper-method. It
selects population members with a likelihood proportional to the
fitness.

<pre>
(defn roulette-select [pop fit-fn num]  
    (let [pop-fits (map fit-fn pop)  
          inc-fits (iterate 
                        (fn [[pfit idx]]  
                            [(+ (nth pop-fits (+ idx 1)) pfit) 
                                (+ idx 1)])  
                        [(first pop-fits) 0])  
          max-fitness (apply + pop-fits)  
          pick-one (fn [num] 
                        (second 
                            (first 
                                (drop-while 
                                    #(< (first %) num) 
                                    inc-fits))))]  
        (map (fn [x] (nth pop (pick-one (rand-int max-fitness)))) 
             (range num))))
</pre>

Now, we’re finished, so we can run the algorithm:

<pre>
(run-ga func-map set-map)
</pre>

GAs are simple but elegant, and they work surprisingly well on some
sorts of problems. All this code is available on
[github](http://github.com/Ejhfast/Gajure).
