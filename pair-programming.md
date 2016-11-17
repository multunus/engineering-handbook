## Pair Programming

This post is mostly about how we do pair programming and things that we've learnt in the last few years about effectively doing it. We've tried to focus less on the what and more on the how.

We follow pair programming for most our work. It helps us maintain a high quality of code and an extremely low defect rate. It can also be a great way for a new programmer to be inducted into the team as it accelerates learning.

Pair programming involves two programmers working on the same piece of code at the same work station. One programmer (called the **driver**) writes the code, while the other(called the **navigator**) reviews the code being written. And these roles have to switch frequently. So, the two practical aspects of pair programming are **code review** and **frequent role switching**.

### Code review
Pair programming, like many other practices of extreme programming, is a software engineering practice taken to the extreme - in this case code review. The driver writes the code while the navigator sleeps. The two programmers switch roles frequently so that both of them get enough sleep.

Just kidding! The driver writes the code and takes care of the low level implementation details while the navigator reviews the driver’s work from a higher level of abstraction.

If you are only beginning to pair program, it might be beneficial to have a checklist written down on a piece of card and stuck somewhere near your monitor. This is what we call a navigator checklist. This checklist contains questions that a navigator needs to keep asking himself (and sometimes the driver) during development. Here’s a sample checklist -

- Are naming conventions being followed?
- What is the next test to write?
- Is this test valuable?
- What is the next task to work on?
- How does this fit in the overall design of the application?
- Is this task taking longer than expected? If yes, what should be the time box?
- Can this part of the code be designed better?
- Is there scope to improve existing parts of the code with the available time?
- Is there an edge case that needs to be considered?
- Is it time to switch roles?
- Is it time for a break?
- Why are we writing this code?
- Have we been debating for more than 10 minutes without writing code?

It is highly recommended that you modify this checklist as you learn more about your pair and from action items that you get from cause effect analysis of bugs. Also based on the experience levels of the programmers, some of these will make sense while others won’t.

### Frequent role switching
There are two common styles followed to switch roles during pair programming.
First one is to use the [Pomodoro technique](https://en.wikipedia.org/wiki/Pomodoro_Technique). This basically breaks down the work into 30 minute long intervals (25 minutes of coding + 5 minutes of short break). After each interval the pair switches roles. This can work great when role switching is followed religiously. But more often than not, it might be hard to unglue programmers from their keyboards at the end of a Pomodoro and when this happens frequently, the navigator might lose focus / interest.

The other style is called the Ping-Pong pairing developed by [Corey Haines](http://articles.coreyhaines.com/posts/thoughts-on-pair-programming/). In its simplest form, one programmer writes the test and the other takes care of getting the test to pass. This is a very powerful style as this drastically improves the involvement of the programmers and also clears doubts as to when to switch roles.

### Other things to be considered
- Pair programming when done right can be very tiring and hence it is very important to take frequent breaks and to make sure you don’t pair for more than 6 - 7 hours a day.
- As with any great practice, a pragmatic rather than dogmatic approach is absolutely essential. Pairing for 100% of the time is never an objective. Based on the experience levels of the programmers and the kind of task at hand, you might want to choose not to pair.
- If a pair has been working together for a long time, then a strange phenomenon called **Pair marriage** can happen - both start to think alike and code alike. This will defeat the whole idea of two people with different perspectives working together. So it is essential to plan for switching pairs at an appropriate frequency.

Do you have questions / disagreements? Go ahead and [raise an issue](https://github.com/multunus/engineering-handbook/issues/new), let's have a discussion there!
