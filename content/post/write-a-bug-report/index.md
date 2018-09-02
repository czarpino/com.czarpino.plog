---
title: "Writing a bug report"
description: "Programmers not mind readers"
date: "2018-08-29"
tags: ["project management"]
---

Ever seen bug reports that would pass off as riddles? Yeah, I'm pretty sure you have. Maybe, you even wrote one yourself. After a few weeks, you come back to a ticket you wrote and you just can't make sense of it anymore. It is possibly because you wrote a crappy bug report. Yep. Sorry, its true.

Fortunately, this is easily fixed by putting yourself in a programmer's shoes. Specifically, you must put yourself in the shoes of the programmer commissioned to fix the bug. Luckily, we know exactly what details a programmer needs from a bug report:

1. What happened
2. What was expected
3. How to reproduce

Whether explicitly written or implied, a useful report should convey all these three.

#### What happened

Isn't it funny how we like focus on the least important stuff. Bug reports almost always describe what happened. Don't get me wrong. Knowing what actually happened is important in debugging (e.g. it becomes a criteria for determining whether a bug has been fixed) but it is also the least important because it merely informs the programmer of what the reporter observed.

#### What was expected

So what happened happened. What exactly of it? Knowing the expected (correct) behavior is the single most important information to correctly address a bug regardless of complexity. It is how things should be which is in contrast to what actually happened. It is worth noting however that for trivial bugs, simply knowing what happened can be enough to deduce what is expected (you must still know it though hence you deduce). For example, a bug report indicating a piece of text was misspelled is, in most cases, enough since the correct (expected) spelling can be easily looked up on the web.

#### How to reproduce the bug

What this wall of text is actually about: knowing how to reproduce a frickin bug. Reporters love to leave this out so much so it makes you wonder whether they really want the bug fixed or they, perhaps, enjoy wasting other people's time. Being able to consistently reproduce a bug is necessary to both trace the root cause as well as validate a solution. During investigation, it also allows the programmer to confirm the bug's existence.

And, those were the 3 important information you must convey in a bug report. I hope you stop writing crappy tickets! Don't be a jerk and always detail what happened, what was expected, and how to reproduce what happened. Your programmers will love you for it.
