---
layout: post
title: Metaprogramming Ruby
post_date: 9 December, 2010 -- Vienna, VA
---


I just finished the book [Metaprogramming
Ruby](http://pragprog.com/titles/ppmetr/metaprogramming-ruby) and I’ve
stepped away with a much deeper appreciation for some attributes of the
Ruby language. I’m a fan of Clojure, so I was pleased to discover that
Ruby’s object model has a dynamism that begs comparison to the
*data-is-code* philosophy of more lispy languages. For more on this
(although I don’t agree with all the article’s conclusions), read [Why
Ruby is an Acceptable
Lisp](http://www.randomhacks.net/articles/2005/12/03/why-ruby-is-an-acceptable-lisp).

I’ve written some code to demonstrate a few of Ruby’s interesting
features. In particular, consider the class FStore:

<pre>
class FStore  
    attr_accessor :dynamic_methods  
    def initialize  
        dynamic_methods = []
    end
    def mix(s1, s2, s3, &block)
        name = "#{s1.to_s}_#{s2.to_s}_#{s3.to_s}".to_sym
        self.send(name) {|a,b| send(s1, send(s2,a), send(s3,b))}
    end
    def method_missing(symbol, &block)
        if block_given? 
            self.class.send :define_method, symbol, &block
        else
            bdy = proc {|*x| symbol}
            self.class.send :define_method, symbol, bdy
        end
        dynamic_methods << symbol  
    symbol  
    end  
end
</pre>

FStore is a very small
[DST (Domain Specific Language)](http://en.wikipedia.org/wiki/Domain-specific_language),
and with it I can declare methods in a new way:

<pre>
# New object  
e = FStore.new

# Define a bunch of methods dynamically  
e.double {|x| 2*x}  
e.triple {|x| 3*x}  
e.square {|x| x**2}  
e.plus {|x,y| x + y}

# Then you can use them, like so:  
e.double 2 #=> 4  
e.triple 2 #=> 6
</pre>

To understand how this works, look to *method\_missing*, as it does all
the heavy lifting:

<pre>
def method_missing(symbol, &block)  
    if block_given?  
        self.class.send :define_method, symbol, &block  
    else  
        bdy = proc {|*x| symbol}  
        self.class.send :define_method, symbol, bdy  
    end  
    @dynamic_methods << symbol  
    symbol  
end
</pre>

With that, here’s the basic idea:

1.  The ruby interpreter attempts to evaluate a statement (e.g.
    “e.double {\|x\| 2\*x}”)
2.  On method lookup, no *double* method is present for e or its
    ancestors, so the interpreter passes *double* (as a symbol) and its
    block to *method_missing*.
3.  Normally, *method_missing* would return an error, but we’ve
    overridden it for the FStore class. Instead, it creates a new
    instance method named *double*. The body of this method is the same
    block that we initially passed e.double.

So to construct methods dynamically you can change the inherited
behavior of *method_missing*. But what’s the deal with send? In
*method_missing*, we use it to declare a new instance method:

<pre>
# This is what we did
self.class.send :define_method, symbol, &block
# This, although seemingly equivalent, would not work
# because define_method is private
define_method symbol, &block
# Another example of using send
[1,2,3].first # is equivalent to
[1,2,3].send(:first)
</pre>

This isn’t complicated. The *send* method provides another way to call a
method on an object. Why then did we use it instead of calling
*define\_method* directly? Well, with *send* we can call an object’s
**private** methods.

Now, let’s move on to some other interesting abilities of FStore:

<pre>
# Mix a few methods
e.mix(:plus, :double, :triple)
    # => create: def plus_double_triple a,b ; plus (double a) (triple b) ; end
# We can call the new method
e.plus_double_triple 2, 3 #=> (plus (double 2) (triple 3)) => 13
</pre>

Here, we call *mix* to generate a new instance method (prefix style) out
of e.plus, e.double, and e.triple. Mix will call this
*plus\_double\_triple*, and we can use it just like any other method.
Let’s look back to the definition of mix.

<pre>
def mix(s1, s2, s3, &block) 
  name = "#{s1.to_s}_#{s2.to_s}_#{s3.to_s}".to_sym
  self.send(name) {|a,b| send(s1, send(s2,a), send(s3,b))}
end
</pre>

Mix creates a new name out of the three method names that we pass it,
and defines a new method with that name using a hierarchy of *sends*.
The method definition itself is delegated once to *method\_missing*, as
the outermost send passes a block to *plus\_double\_triple*, which
doesn’t initially exist for our FStore instance.

A complete gist (with all the referenced code) is [available
here](https://gist.github.com/758608).
