---
layout: post
title: "Research Methodology"
date: 2018-07-18
tags: research
description:  My methodology when approaching a project
---
## What
Research is a task like any other.  It is a byproduct of asking a question and seeking an answer.  Sometimes you get the answer you are looking for.  Sometimes you learn a lot of things besides the answer to the question.

There are ways to make research more efficient and maximize your chance of success.  In this post I will go over how I approach research in my field.  This methodology works for me in the type of research I find myself doing.  As with anything of this nature what works for me may not work for you, so take what you can from this and make it your own.

### Step One:  Formalize the Question
Imagine that we are going to do some research on a software application.  How you pose your question has an impact on what kind of decisions you make about your research.  Lets consider some questions.

* Question 1: Is there a vulnerability?
* Question 2: Is there a memory corruption vulnerability?
* Question 3: Is there a buffer overflow vulnerability that is exploitable via a remote connection?

To answer question 1 we would need to go through the entire application and get as much code coverage as possible.  We would want to check for every type of applicable vulnerability for that code base.  Even then we may not be able to guarantee there are no vulnerabilities in the code 100%.  (There is some notion of proving 100% vulnerability free code but I'm not aware of the specifics enough to claim it here.)

To answer question 2 we restrict ourselves to a certain class of vulnerability.  Once we find our answer for that class of vulnerability our job is done.  We don't care about if other vulnerabilities exist outside of that scope for our research.

Question 3 is a very specific question.  The easiest answer would come if our application has no remote connections possible.  If we could prove that is the case no further research is needed.  Question answered.

As you can see the question asked determines the course of action taken later in the researching phases.  A properly defined question will make the scope of the research clear.  An improperly defined question will make the scope unfortunate and may wind up being an example for others not to emulate.

### Step Two:  Information Gathering
Once you have a clear question it's time to go find out as much as you possibly can about the subject of the question.  Some of the information will be helpful some will not.

In this phase the purpose is to discover what I am actually working with.  For example if I have a piece of software that I'm unfamiliar with and I want to do vulnerability research I will focus my search on areas relating to that.  I would want to answer some preliminary questions.  For example:

* What are common ways that type of software is put together?
* What are common vulnerabilities that type of software contains?
* Is that vendor prone to making certain types of programming mistakes?
* Are there manuals listing out the complete functionality of the software and its components? (Or any of it?)

This stage depends a lot on how much previous experience is brought to the research.  For example, if you have done development on the type of software you are researching you would alredy have an idea of how the software is constructed.

### Step Three: Plan Your Approach
To proceed we need to have a plan.  That plan needs to map out or approach but also be flexible enough to adapt to changes.  My goal is to have a guide to make sure that I stay on task and make progress, not to have a step by step process that I can use in any scenario.

This stage should keep the queestion in sight as the ultimate goal of the research.  You can start choosing tools that will fit your research scenario most effectively.  You can also start narrowing down vectors that you believe will lead you to results.

Experience will be valuable but it is not a requirement.  You gain experience by doing.  If you are not sure where to start you can pick a task you believe will get you results and evaluate that approach when you start the research phase.

You can also rely on other researchers experience in this phase.  In our software example we could fall back on texts like [The Art of Software Security Assesment](https://www.amazon.com/Art-Software-Security-Assessment-Vulnerabilities-ebook/dp/B004XVIWU2/ref=sr_1_1?ie=UTF8&qid=1532024648&sr=8-1&keywords=the+art+for+software+security){:target="_blank"}.  In the information gathering phase you may have come accross blog posts or technical write ups of similar research engagements.  If that is the case you can model after approaches that worked for those engagements.  I would not dismiss appraoches that did not yield results unless you can see why they would not yield results for your research though.

### Step Four: Start Researching
Once you have a plan in place you can start on carrying out the research.  Following your plan and adjusting where necessary.

While I am doing the actual research, and even during the previous stages I take a lot of notes.  I always have a notebook where I write down what I try and what happens.  I also try to include what I am thinking at the time.  Then when I am done I convert that paper copy into a digital copy so that I can do an after action review to reinforce what I learn.

### Conclusion
I have tried to keep this methodology as general as possible.  There are books that have been written on this subject that I have never read.  I have developed this way of doing things by seeing what others have done and what has worked well for me in the past.  I still keep an open mind in aletering any of the steps based on what the current scenario is.  Hopefully this has been helpful to you.
