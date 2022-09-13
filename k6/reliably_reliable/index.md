---
title: Reliably Reliable
summary: | 
  When are you reliable enough? How hungry are you?
author: Vince Huang
socialImage: croc_eating_a_big_mac.png
cover: croc_eating_a_big_mac.png
language: en
tableOfContent: false
---
I Google’d the word “reliable” the other day.

At the top of the results page was a definition from the Oxford Languages dictionary.

adjective
consistently good in quality or performance; able to be trusted.
"a reliable source of information"
noun
a person or thing with trustworthy qualities.
"the supporting cast includes old reliables like Mitchell"

I started thinking, what’s “reliable”? I glanced at my mobile phone. I felt it was pretty reliable. I can make and receive calls, I play games, battery life is pretty decent, photos are amazing… But it’s kind of new, so maybe that doesn’t count. It’s not really reliable, the jury’s still out. It’s just new.

Then I started thinking about other things, and even people. My parents are reliable, at least to me and my family… My car… sometimes. What else was reliable? It had to be consistent to a point where you can inherently trust it would almost always be the same way you’ve always known it to be. It didn’t even have to be reliably good! Then I overheard the local TV channel mention something that made total sense.

A McDonald’s Big Mac.

A marketing “Jingle” from 1975:
Two All Beef Patties, Special Sauce, Lettuce, Cheese, Pickles, Onions on a Sesame Seed Bun”


Image from https://en.wikipedia.org/wiki/Big_Mac


If you’ve ever ordered a Big Mac from McDonald’s, you’ve probably experienced the reliability of the burger. It’s been around since 1967! That’s a 55 year old product. There have been various spin-offs, but for the most part, the Big Mac today is almost identical to the Big Mac of the 1960’s. In fact, the ingredients and product have been so consistent for such a long time that global economists now use “The Big Mac Index” to measure purchasing power among the different countries. 

But it wasn’t always reliable. In fact, there were a few failures along the way. But eventually, they got it right. In a way, software development isn’t much different.

Step
McDonald’s
Software Dev, Inc.
1.
Put a sandwich together
Build a product/feature
2.
Eat it yourself (or get others to eat it)
Test (in Prod?) for success and failures
3.
Improve and perfect the special sauce
Implement changes based on feedback
4.
Be consistent when making them
Automate all the things


Everyone has their own way of doing step 1, and step 3 is always optional (depending on whether or not you intend to build the “perfect product”. But steps 2 and 4 have a lot of flexibility and haven’t always been as consistent as they should be.

Test for Success and Failures

This sounds obvious, but there’s some caveats to remember - namely around discovering potential failures, and how to properly handle them.

Standard functional testing such as unit testing, integration testing, and acceptance testing all help to ensure the various moving parts are all connected to each other as designed. Individually, we know what lettuce, cheese, and pickles taste like. Once you’ve put them together with the other ingredients, though, it’s a totally different experience. 

Non-functional tests such as Performance tests validate the operational aspects of your software.Tests such as load testing, stress testing, soak testing, and endurance testing help to prove out that your application can behave at the user scale and duration that you’re hoping to have. At the very least, performance tests help your team to understand the upper bounds limitations and capacity your systems can handle before things start to fail.

Which leads us to the next phase - addressing the failures and how to handle them.

While load testing, you discover your application’s response is sluggish after a certain number of requests per second. The response time is still under the service level thresholds you’ve defined for the duration of your test, so there’s nothing failing or causing alarms. Everything on your checklist passes, and QA validation is complete, right?

But perhaps your test environment is ever so slightly different than your production environment. Perhaps a power fluctuation in the data center that hosts your hardware caused a server rack to become slightly unstable. Maybe a server or cloud administrator accidentally pushed the wrong update to a region, or even to just your production kubernetes cluster. No matter the event that caused an outage, the fact remains that an outage has happened. 

In our previous tests, we were able to identify and define what the upper bound capacity of our systems and software was. On the other end of the spectrum, we should also make the effort to understand the lower bounds of our software and systems. What are the absolute minimum resources necessary to properly handle an outage? If I don’t have those resources available, how does my software handle itself? Does it sit idle and wait? Does it crash and attempt to restart? Maybe it’s designed to retry, but exponentially back off?

Testing for these scenarios and how your systems react is sometimes referred to as Chaos or Reliability testing. In Chaos testing, we methodically and systematically introduce failures of varying degrees to discover different characteristics about our software and the systems that support them. Note that “systems” doesn’t just include the hardware where your software is deployed. Systems also includes the on-call and incident management “people systems” that we rely on when things take a turn for the worse. Understanding how your systems respond to adverse events helps you properly plan and ultimately become more reliable. 


Automate ALL the things

It's important to remember that with so much testing that needs to be done, there are no shortcuts around any of them. All of the functional tests should be performed, and most tests should not be replaced or substituted for another. This is true for chaos testing as well. In fact, in my experience, the teams that execute functional, non-functional, and chaos tests understand more about their systems and software (and have a more pleasant on-call experience) than teams that exclude any one of them - especially chaos tests.

As you can likely imagine, though, that’s a lot of testing. How can someone possibly test for every possible failure, and then also design and implement the solutions necessary to mitigate the impact from those failures?

The answer is you can’t. At least not by yourself.

Involve other teams and people 
You (and your team) are only one perspective. In the world of statistics, your sample size (effectively of 1) is too small. History has plenty of examples of products that were originally intended for some other purpose. Listerine was originally a surgical antiseptic. Coca-Cola was a cure for morphine addiction (and included a narcotic, cocaine). Microsoft Windows games, Minesweeper and Freecell, were designed to actually help train people to properly navigate “drag-and-drop”, and right and left-click more naturally. Without additional user input, McDonald’s Special Sauce wouldn’t need to be capitalized when written out.

The point is your experiences and interpretations are limited to your own, and therefore your expectations around user experience, performance, and failures are likely going to be just as limited. Expanding your inputs to include experiences and interpretations of other teams will ensure you have a more complete representation of actual user experiences. What might be tolerable for you may not be tolerable for others, and vice versa as well. 

Script your failures
Very few people enjoy doing any task more than once. Lots of folks I know dislike saying things multiple times. Instead, they’ll write instructions out so the steps can be executed without having to be repeatedly explained. These written instructions can also be shared easily, too. This limits the potential duplication of artifacts, and can mitigate “snowflake”-like instructions that may slightly differ from version to version.On that note, if someone needed to build or modify the instructions, they would be able to do so relatively easily. 

The same concept applies to failure testing efforts. Scripting your failures not only automates the actual execution with a certain consistency, but also allows you to be able to share your scripts and tests with other teams that may also be testing for similar failures and limits. If teams want to modify the scripts to adjust to their own particular needs, they are able to and can then maintain those versions for their particular teams. A Big Mac (and McDonalds as a brand) is generally recognized for some amount of consistency, regardless of which restaurant you visit. The more automation and consistency of your tests, the more reliable your expected results should be.

80/20 rule
Perhaps you’ve heard of the Pareto Principle (the 80/20 rule), but if you’re not familiar with it, that’s ok. In a reliability computing environment, we believe that 80% of errors and failures are caused by the top 20% of bugs. 

Nobody is perfect, and no code or system will ever be flawless. Flawless code and systems result in an uptime calculation of 100%, and if you do the math, that’s no easy achievement. You can improve your reliability and expectations by addressing the top 20% of your issues. Once those are addressed, re-examine your issues and prioritize the next top 20%. 

Conclusion
At the end of the day, we’ve still made our hamburger, and people recognize our hamburger. It has grown a reputation for being reliable because we’ve tested it, made improvements, and automated our efforts for consistency. With the right practices and processes behind us, our hamburger can be reliably reliable.



