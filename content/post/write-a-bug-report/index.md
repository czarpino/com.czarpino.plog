---
title: "Writing a bug report"
description: "Programmers not mind readers"
date: "2018-10-21"
tags: ["project management"]
---

Despite being at the receiving end of bug reports, programmers are generally poor authors of bug reports as well. This came as a surprise to me as I worked with programmers of varying experiences. How could programmers themselves not know how to author an effective bug report? If anyone, they should best know what a good bug report looks like. This is kind of true and not true at the same time.

It does seem like most programmers can deliberately tell apart a good bug report from a bad one. When authoring, however, they seem to be at a loss. They sometimes put in unnecessary information or leave out important ones. Oftentimes, they get lazy and just put in whatever first comes to mind and sticks. What you get is an empty ticket with the title: "Cannot upload". A dozen of these and a few weeks later, you get a substantial backlog of tickets no one understands.

This seeming paradox of a programmer's inability to author good bug reports can be attributed to a problem solving mindset. Programmers typically care far more about procuring the solution than the problem needing solving. It is not quite uncommon to see programmers (especially juniors or immature ones) take pride in being able to decipher completely unhelpful bug reports. It probably seems like piecing together a puzzle. You get to pat yourself on the back when you get it right. But get it wrong and you waste not just your time and resources.

In a company, a team, or any worthwhile group endeavor, it is less about individual prowess than it is about teamwork and collective productivity. Deciphering a poorly written bug report and realizing you got it wrong 3 days later is a huge waste of everyone's time.

As those who have studied the computer sciences may have learned, how a problem is framed also influences its solutions. That is, a well framed problem can also make the optimal solution obvious. Similarly, a well written bug report makes it easier to correctly understand and address a bug.

For the past half decade, I have followed a simple yet effective 3-step template for reporting bugs. While I only got it somewhere on the internet a few years back, all the teams I have shared it with have decided to adopt it. I privately call it the Reality-Expectation-Reproduction (RER) template and it basically asserts that a good bug report must at minimum have the 3 following information:

 - What happened - Reality
 - What was expected - Expectation
 - and How to reproduce - Reproduction

Together, these three convey to the reader all the actionable information they need to verify a bug. Even better, this template is also useful for user testing and verifying the bug actually no longer exists.

Sample RER bug report:

> ### [What happened]
> Uploading large png image file fails.
>
> ### [What was expected]
> A valid png image file less than 30MB should be uploaded without errors. 
>
> ### [How to reproduce]
> 1. Go to user profile `/me/user/profile`
> 2. Click on edit profile > update photo
> 3. Upload the attached 25MB png file
> 4. Notice the upload fails and returns error
>
> ### [Screenshots]
> ![Screenshot1.png](#)
> ![Screenshot2.png](#)

I have found, however, that even better than the RER template are bug reports with annotated screenshots or [screencasts](/creating-a-gif-screencast/). When applicable, I believe screenshots and screen casts are the most effective way to convey information.

In practice however, leveraging both the RER template and well picked screenshots or screen casts seem to result in the most helpful tickets. They are simple to write, easier to estimate during sprint planning, easier to understand, and easier to verify when testing.

If you have a more efficient approach I would be delighted to know. How do you report bug tickets in your team?
