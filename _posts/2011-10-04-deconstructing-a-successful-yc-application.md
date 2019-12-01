---
layout: post
title: Deconstructing a Successful YC Application
post_date: 4 October, 2011 -- Menlo Park, CA
---

The next YC application deadline approaches, and I thought it would be
fun to look at the successful application Muzzammil and I wrote in the
summer of 2010. At the time, we were both undergraduates, and we hadn’t
yet built our product. I’ll go through our responses one by one.

### What is your company going to make?

We described exactly what our product would do.

> Taazr detects bugs in live web applications through statistical
inference.

> Think of a web application as a black box, with its inputs as HTTP
requests and its outputs as HTTP response data. After a client
instruments her web app with our javascript, Taazr will collect
request/response data to build a model of expected behavior. When an
“anomalous” response is detected, we notify our client, sending along
details about the potentially faulty request/response pair.

Don’t be vague. Going into detail may seem to leave out the “bigger
picture,” but I suspect this matters little to the readers at YC. You
have the rest of your application to impart a broader vision; for this
question talk specifically about what you are going to build.

### Please tell us in one or two sentences about the most impressive thing other than this startup that each founder has built or achieved.

It’s often said that YC is all about the founders. Our answer:

> Ethan was admitted to CS PhD programs at Stanford, Berkeley, and
MIT for research on automatic software development (e.g. automatically
finding bugs, fixing bugs, generating test suites).

> Muzzammil is a member of the core development team for GuardRails, a
secure web application framework, which will be published at USENIX 2011
and presented at RubyNation. He is also the founder of Wahoobooks, a
site where U.Va. students can list used textbooks.

We mentioned specific and verifiable achievements, the substance of
which implied that we are determined people. You should try to avoid
generalities.

### Please tell us about the time you most successfully hacked some (non-computer) system to your advantage.

A great answer here can really help you, but it was perhaps our weakest
response. Judge for yourself:

> A Computer Science degree from U.Va. typically requires that you
> complete many courses within a variety of unrelated disciplines. Most
> of our peers must take classes in Physics, Chemistry, and a “fake”
> humanities listing called Science, Technology and Society. We escaped
> such requirements through a little-known option to pursue a BA in
> Computer Science, in place of the Engineering School’s BS. With this
> degree, we completed the core CS curriculum and any other classes that
> caught our interest, but we avoided the rigidly defined ABET
> requirements of the Engineering school. This left us more time to
> pursue research and hack on web applications.

While Muzzammil and I aren’t totally straight-laced, we couldn’t think
of much to say. And that was a strategic error, for a sufficiently
devious answer has a great opportunity to stand out. While I like to
think that the most clever subversives are the overtly boring ones,
that’s not correct so far as this question is concerned. Give a better
answer than we did!

### Please tell us about an interesting project, preferably outside of class or work, that two or more of you created together. Include urls if possible.

I’d rate our answer here as about average. We’d worked together before,
but not on anything terribly impressive.

> For a mobile development class, we created a Barefoot Running
application\[1\] for the iPhone. The app allows users to report and view
the location of glass shards — centralized in an off-site database — and
keeps track of speed and distance data throughout a run.

> We also jointly created BijectKarma, a community connecting designers
and developers\[2\]. We had trouble attracting initial users, however,
and the site was taken offline.

Perhaps I should give a plug to barefoot running, as clearly that’s the
reason we were accepted. Go work on cool things.

### How long have the founders known one another and how did you meet? Have any of the founders not met in person?

This one is easy to interpret. Come application time, there’s nothing
much you can do to improve your answer.

> 1.5 years. Ethan was Muzzammil’s TA.

> While working on a problem set, Muzzammil mentioned his interest in
startups. Ethan asked if he had heard of Y Combinator, which of course
Muzzammil had. As it turned out, we were both fishing for potential
co-founders.

So yes, you should meet people earlier rather than later. It’s better if
you can convey that your founders know each other well.

### Why did you pick this idea to work on? Do you have domain expertise in this area? How do you know people need what you’re making?

I like our answer to this one, but with a few caveats.

> Finding and fixing software bugs is expensive. Taazr will save
companies time and money by identifying bugs and potential fixes in web
applications. We chose to work on Taazr primarily due to our familiarly
with related research fields, but also because it represents a
challenging problem.

> Ethan has two years of experience hacking with the Automatic Program
Repair (APR) research group at U.Va, where he’s worked with
state-of-the-art techniques in program analysis, testing, and
statistical debugging. He has published work increasing the efficiency
and scalability of APR.

> Muzzammil has a year of experience with the GuardRails research group at
UVA, where he helped create a secure web framework for Ruby on Rails.
His work is published in USENIX 2011 and will also be presented at
RubyNation.

> More generally, Taazr was inspired by the Cooperative Bug Isolation
Project [2], in combination with ideas gleaned from our respective
research groups at U.Va.

We describe our domain expertise, and slip in evidence that we can get
things done. However, we do come off as a bit researchy, which I think
is a bit of a risk. Convey expertise through specific accomplishments.
You should be perceived as people who know what they are getting into.

### What’s new about what you’re making? What substitutes do people resort to because it doesn’t exist yet (or they don’t know about it)?

For us, this was almost a continuation of the previous question.

> Uncaught program bugs are expensive, and for this reason, good
developers take care in testing their code. However, even the best test
suites will not catch all program bugs. Taazr will identify such bugs
earlier in the development cycle, and companies will save money that
otherwise might have been spent on code maintenance and customer
support.

> We believe that statistical debugging is uniquely suited to web
applications, due to the relative ease with which web apps can be
instrumented through lightweight and unobtrusive javascript. While
statistical debugging has succeeded in a research context on desktop
software, automatically finding bugs in live web applications remains an
open industrial problem.

> However, our ultimate aim is not just to find bugs in web applications,
but also to fix them. This will likely require tighter integration —
server-side — between our tools and a developer’s code.

I’d once more levy the “researchy” criticism against our response. An
answer to this question will depend upon your product, and I doubt it
matters whether your idea is truly novel. As always, clarity is
important.

### Who are your competitors, and who might become competitors? Who do you fear most?

Another straightforward one.

> Coverity and Klocwork also find program bugs, but they don’t target
> web applications. Moreover, engineers use their products throughout
> the development process, whereas Taazr operates, automatically, on
> live production code.

It’s worth noting that we didn’t fully answer this question. I suppose
that’s because we are fearless, but I’d recommend a different approach.

### What do you understand about your business that other companies in it just don’t get?

Our answer here was weird.

> Writing code is much like putting words to paper, an act of creation.
> When you write, it is important to spell things correctly, but few
> writers spend much time on this task, for they have spellcheckers. We
> think that testing should be just as straightforward. It is quite
> important, but should not monopolize your attention.

Our response is both wrong — I now disagree with it — and confusing.
Testing is a bit of a non-sequitur. You should give a real reason why
you have insight over your competitors.

### How do or will you make money? How much could you make? (We realize you can’t know precisely, but give your best estimate.)

We had no idea how much we could make.

> Taazr will charge clients monthly. We see a market opportunity in the
> tens of millions.

I’m not sure this question matters much, as it’s pretty easy to see how
most products might become profitable. If your idea is particularly
eccentric, then perhaps a good answer matters more.

### Please tell us something surprising or amusing that one of you has discovered. (The answer need not be related to your project.)

This is a fun question to answer, but I don’t think it heavily impacts
your application.

> You can start small word-memes among family and friends. Choose a
word that is fairly obscure (but not obviously so), something like
pedantic, sycophant or obsequious. Over a few days, casually inject it
into conversation.

> Listen throughout the next week. The word will come up with surprising
frequency. You can also do this with unique inflections, and distinct
rhythms of speech.

You should try to be interesting and clever, I suppose.

### The rest of the questions?

Our responses were one-liners which suggested that we had begun market
research, but didn’t have any customers. Nothing insightful. But we did
receive a follow up question from Robert Morris…

### Robert Morris: Why should I believe that this will work?

We gave him a well-grounded but complicated answer, as suits an MIT
Professor.

> The best evidence probably comes from recent web security research.
For instance, Vigna et al. has successfully used anomaly detection to
identify security vulnerabilities in web applications. While we are
attacking a different goal (identifying bugs, not vulnerabilities), our
current work borrows heavily from techniques used successfully in
anomaly detection systems.

> Since our models will be trained on more detailed user metrics than has
traditionally been attempted (e.g. user mouse movements and clicks, as
opposed to just HTTP request strings), we see the real question as
whether we can distinguish between anomalous user activity (which may
signify a bug, or some other issue) and the noise which you would expect
in user-based data.

We didn’t receive a follow up question, although it’s unclear whether
that’s a good thing.

### Concluding thoughts

I hope you found this useful. It was fun to dig through our old
application, particularly as we have since gone through a full pivot:
Taazr became Proxino. Things change; such is the nature of time, and
confidant YC applications.

As final advice, I would focus on brevity and concision in your answers.
The people at YC read through quite a lot of these, after all. I’d also
keep in mind that ideas are fungible, and people are not. YC cares about
the founders. And if you take away anything from this post, it should be
that groups with imperfect applications can get into Y Combinator. So be
inspired. Best of luck to applicants for the winter batch.
