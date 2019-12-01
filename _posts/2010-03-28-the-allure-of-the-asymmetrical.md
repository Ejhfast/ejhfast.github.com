---
layout: post
title: The Allure of the Asymmetrical
post_date: 28 March, 2010 -- Charlottesville, VA
---

Though I’ve lived in Charlottesville for two years, I haven’t taken
enough advantage of the local farms. I obsess over health, and grass-fed
animal products abound in the area. But when I finally patronized a farm
last week, I noticed something obvious[^1]. Local eggs look nicer
than their industrial-farm begotten counterparts.

The local eggs appeal to my eye not due to differences in color or
lighting, but through asymmetry. If you look at them closely, you see a
deviation in size across the carton, a variance in color, and a
sprinkling of freckles across shell exteriors. They are skewed, chaotic.
In contrast, it looks like someone bleached the industrial eggs, which
vary little in size across the carton.

A slight asymmetry plays nice with human perception. It draws our eyes
to important details, yet makes it easier for us to perceive the whole.
Asymmetrical perception may have implications for how we write code[^2].

Consider this comparison of a C function (taken sort-of randomly from
Git) and a Clojure function (taken from Gajure). First let’s look at
*add\_files\_to\_cache*:

<pre>
int add_files_to_cache(const char **prefix, const char **pathspec, int flags)  
{  
    struct update_callback_data data;  
    struct rev_info rev;  
    init_revisions(&rev, prefix);  
    setup_revisions(0, NULL, &rev, NULL);  
    rev.prune_data = pathspec;  
    rev.diffopt.output_format = DIFF_FORMAT_CALLBACK;  
    rev.diffopt.format_callback = update_callback;  
    data.flags = flags;  
    data.add_errors = 0;  
    rev.diffopt.format_callback_data = &data;  
    run_diff_files(&rev, DIFF_RACY_IS_MODIFIED);  
    return !!data.add_errors;  
}
</pre>

Reading from the left, this function is symmetrical. It doesn’t draw the
eye to any particular bit of code within the curly braces, and it
doesn’t convey anything through it’s structure. Much of this has to do
with the imperative nature of C and *add\_files\_to cache*. Now consider
a second function, *list-crossover*:

<pre>
(defn list-crossover  
    “A generic crossover function for simple lists. 
    You may need to write your own.”  
    [[s1 s2]]  
        (let [point (rand-int  
                        (min (count s1)  
                        (count s2)))]  
            (concat 
                (take point s1)  
                (drop point s2))))
</pre>

Here you see a nesting of sorts, as indentation conveys properties in
the code (e.g. that *take* and *drop* are arguments to *concat*). The
functional nature of Clojure lends itself well to this kind of visual
deconstruction, and *list-crossover* imparts semantic meaning through
asymmetrical structure.

I don’t suggest that one language is better than another at conveying
meaning through syntax and symmetry, but rather that the way you write
code has implications upon how easily it’s understood. Symmetry, or a
lack thereof, plays an important role.

[^1]: Sometimes the most obvious things are the hardest to notice.

[^2]: Also for how we structure writing (sentence length, paragraph length, etc.). Novelists speak of things like “rhythm” and “cadence,” where this is an important issue.
