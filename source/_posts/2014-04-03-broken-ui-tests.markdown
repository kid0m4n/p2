---
layout: post
title: We hate your broken UI tests!
subtitle: 
permalink: /issue09/broken-ui-tests
byline: Chirag Doshi and Raxchel Laycock
category: issue10
authors:
    - name: Chirag Doshi
      twitter: chiragsdoshi
      avatar: Chirag-Doshi.jpg
    - name: Rachel Laycock
      twitter: rachellaycock
      avatar: rachel-avatar.jpg
---
I have been on too many projects where the promise of automated end-to-end functional tests doesn't pay back enough or sometimes, any positive results. When you have a  legacy codebase that has no tests it is common to begin by writing end-to-end functional tests.  This is likely to be the highest test coverage you have. 

>> “You can spend weeks chasing down the failures, because ...  the functional tests don’t tell you what is broken... They just tell you something is broken.”

Writing unit and integration tests after the fact is hard, whereas functional tests run through a browser can be added at any time. It’s common for those tests to break. A lot. You can spend weeks chasing down the failures, because, unlike unit tests,  the functional tests don’t tell you what is broken or where to locate the failure in the code base. They just tell you something is broken. That something could be the test, the browser, or a race condition.  There is no way to tell because functional tests, by definition of being end-to-end, test everything.

So sometimes I hate them. 

Martin Fowler refers to these tests that break indeterminately as “test cancer”. A cancer that should be eradicated. If a test always breaks and you don’t trust it then your best course of action is to simply delete it.   As Martin says - “they are worse than useless”.

A legacy codebase is not the only occasion where you end up with too many brittle end-to-end UI tests. Let’s take a look at another scenario. 

You start a greenfield project. You’re in a mature agile team that does XP practices like TDD. So the devs do TDD on their code. They drive out the design with tests and the result is you get code with high unit test coverage. Yay. Perhaps you have such great devs they also write a couple of integration tests to examine integration points like database access, or communication with a file system.  Even better, your devs pair with your QAs and write automated end-to-end functional tests as part of their story.

Let’s fast forward six months. Development is still ongoing. You now have 501 unit tests. You have a 10 to 20 integration tests. Finally, you have 106 automated end-to-end tests.

To be very clear: this is not a good place to be. 

Our end-to-end tests are hard to maintain. They take too long to run. They fail randomly which can generate false alarms. This causes us to waste time debugging and maintaining these tests. They make us rip our hair out.  They are our test cancer. What is the alternative? How do you avoid breaking the test pyramid and having too many brittle end-to-end tests?

On our team we now get the devs to TDD their code, just like before. They also write integration tests, just like before. The difference now is that the devs also write view level tests to check the presence of key data in the html output (as much as possible based on the MVC framework in use). They also write controller level tests. Finally, they write javascript tests to test significant UI logic. 

>> “The driving question we ask is, if a piece of functionality in our app breaks will we break a test?”

They are pushing the testing down the stack. Rather than test UI logic, data, integration, views through the browser we try and test at the lowest level we can. The driving question we ask is, if a piece of functionality in our app breaks will we break a test? If the answer is yes for a lower level test than the UI then we write that test and not the UI test.

Our devs and QAs still write a few end-to-end minus UI tests for every story. I believe this has a positive impact on the architecture of the system. It results in creation of an API for your app. It doesn’t matter whether it is deployed separately or not. The point is by driving out lower level tests you create an API that your web front end can consume and you test any UI logic in your web front end where possible through JavaScript.  

QAs write very few end-to-end tests using tools like selenium. The aim of these tests is to do a quick sanity check of the integration of the UI with the rest of the application. I believe these should be max 10-20 in number and should mimic the most commonly used user journeys in the system.

What this provides is less brittle UI tests, and also gives us other added benefits.

-> ⁂ <-

We still have the level of confidence required to release frequently, since the overall coverage of the different parts of the system is as high as before.
QAs need to write and maintain fewer end-to-end tests, ~10 instead of ~100. It is easier to keep these tests green and they run faster. Finally, QA has the time to focus on other kinds of testing like manual testing, exploratory testing, cross browser look and feel testing, performance testing etc.


