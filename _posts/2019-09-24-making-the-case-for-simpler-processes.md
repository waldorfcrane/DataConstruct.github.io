---
layout: post
title:  "Making The Case For Simpler Processes"
splash: "/assets/img/samantha-gades-BlIhVfXbi9s-unsplash.jpg"
excerpt_separator: <!--more-->
---

Code is only valuable when it's in production. Until then, it's a liability. It is essential that we focus both on quickly delivering high quality software to our users and improving our processes to make that delivery easier.

High performing IT organizations recognize that software development is a process that begins with an idea, and finishes with code in the hands of their users, and tries to optimize the complete process, not just parts. 
<!--more-->

###  What is a High Performing IT Organization?
High performing IT Organizations are surpassing their competition in leaps and bounds. They ship product and change dramatically in a 6 month period. Facebook's Employee Handbook has an interesting quote on the subject[0]:

<p class="testi">The Quick Shall Inherit the Earth. Fast is better than slow. While slow is adding unnecessary embellishments, fast is out in the world. And that means fast can learn from experience while slow can only theorize. Those who ship quickly can improve quickly. So fast doesn't just win the race. It gets a head start for the next one.</p>
These organizations do everything in their power to unlock the velocity of the developer. They are committed to breaking down the non-value add barriers that traditionally separate a dev from production. One of their prime directives is velocity, and they pursue it with complete commitment.

### Why be a High Performing IT Organization?
Shipping code fast isn't the goal of being a high performing IT organization, it's just one of the ways we get to the place we want to be.

If you look at the statistics, High performing IT organizations:

- Have a failure rate less than 15%
- Spend 20% more time on planned work
- Spend 22% less on unplanned work
- Have a Mean Time To Recovery (recovering from an issue in Production) of less then an hour
- Ship product 24 times more often.

By contrast, lower performing IT Organizations have a failure rate of 30~45% and will have a Mean Time To Recovery of a day or more [1].

High performing IT organizations spend more of their time on value producing work, and less time firefighting.

### How do they do it?

One of the most fundamental principles is to simplify processes that get in the way of providing value to our customer.

There are some key practices that separate these high performing IT Organizations from others. They heavily invest in:

- Continuous Integration so that new code is always tested against the latest version
- Continuous Deployment so that they are used to releasing software quickly to let it realize its value
- Test Automation rather than manual gates so that developers receive rapid feedback and quality is assured.

By contrast some common industry practices have been not shown to correlate with being a high performing IT organization, and in some cases, are negatively correlated: 

- Having the Quality Assurance Teams creating tests instead of having developers own them
- On demand test environments rather than automated unit tests that run locally and without external dependencies.

These organizations have invested in processes that allow them to ship product with the least amount of friction with quick feedback loops while sharing the responsibility of stability [1]. The result is twofold: One, the developer feels a bigger sense of responsibility for production stability. Secondly, the developer gets faster feedback about code changes, and has a greater ability to understand the problem and fix it quickly, even before production.

### Why do these practices create High Performance?
This starts to make sense when we look at the total cost of fixing bugs during various stages of the SDLC.

<p class="testi">The cost of bugs increases by orders of magnitude the longer it takes to discover [2].</p>
NASA had found there was a 7X increase in cost when a bug was found at the Integration testing phase (systems talking to other systems) and a 100X increase in cost when found in production [3]. Organizations have also found that humans are typically bad at identifying issues at code review time [4].

High performing IT Organizations are able to ship more product because they attain massive savings through tight feedback loops that run as close as possible to the developer at the time of coding, directly on their workstation. They are also able to change the purpose of the code review from "does this code work?" to "does it provide value to the end customer?" [4].

### How to do Tight Feedback Loops right
Having fast and reliable feedback loops that run close to the developer is possible. Etsy invested heavily in analyzing their testing methods. They approached it with a divide and conquer strategy. Etsy's core test suite runs 4500 checks within a minute. Their integration tests stub out dependent services. Their smoke tests are basic CURL checks against a deployed application. They only rely on their End to End tests to check a few of their core use cases [5].

Github has built a test suite that runs in 2-3 minutes and validates their entire application [6]. Many high traffic teams (Maps as an example) at Google don't rely on any End to End testing, and in certain cases where they did have End to End tests, it was only to validate basic configuration of the application and did not validate functionality. They also found that having separate "QA" teams or "QA" environments disincentivized their teams from thinking about Quality as they could defer the cost [7] [8].

AirBNB started to use stubbed downstream services within their testing strategy while building out their microservice architecture [9]. These types of approaches to simplifying their processes to have quick feedback loops have allowed these Organizations to ship software faster and with higher stability.

### What Can We Do To Get There?
We need to incentivize fast testing that is close to the dev, and disincentivize processes that slow us down. Google had good success using this concept. They had teams build client libraries to their microservice APIs with built in support for testing. This allowed Front End and Mobile teams to easily test their own applications against the libraries without the need to do HTTP calls into the actual API endpoints.

The client library model is an example of a method that incentivized fast consistent tests that ran close to the developer while giving high feedback and less bugs all while disincentivizing reliance on additional environments for testing [10]. Also note that reliance on additional environments for validation disincentivizes teams from shipping product as it's more cumbersome to validate the product which leads to risky big bang deployments.

### The Hidden Costs Of Validation Environments
We also need to consider the costs involved in supporting our validation methods. Google has invested many resources in building tooling that analyzes their end to end "on demand testing" in order to automatically classify and remove tests that consistently fail for no reason [11]. They then realized that the costs involved in supporting these validation methods became overly costly due to the infrastructure and tooling required for it's "on demand" nature and moved towards speedier and more reliable validation methods [12]. It also becomes increasingly costly to get Production like environments as we need to support tooling and configuration to do things like share data, mock services etc [13].

It can also be costly at the human level. The core use-case for a microservices architecture is to make our software modular to drop the cost of communication as each team can operate individually and ship product whenever they want. Communication costs increase at a rate of n^2, where n is the amount of people involved within the conversation [14]. As we add more environments and additional layers of process, we inherently force in more required communication for a change to be pushed out. Teams have to manage those environments and ensure their code gets into those environments and then communicate those changes.

Github realized that they needed to remove all friction from their process to ensure they could continue shipping product at a high rate [15]. Initially they had multiple environments with ad-hoc options to deploy any code to any of those subset of environments. They then moved to only Staging or Production deployments as it simplified communication, incentivized good practices and was less complex to manage [16]. They viewed it as making the steps in their process wider, giving faster feedback loops, instead of adding additional layers to the process [17].

### In Closing
There are many techniques that can also aid us in shipping product to production as fast as possible. Techniques like feature flagging allow us to ship unfinished code to production and only allow certain users to see that functionality. Many Organizations like Facebook use this technique to ship new Products so that when the actual launch occurs it is as simple as turning a light switch on. This gives us the benefit of ensuring that new features works with the current product and also gets real world load. We can also use libraries that allow us to run multiple code paths in a single call to validate functionality and performance concerns with production load. Github was able to use this technique to rewrite their entire GIT backend in real time on Production servers [18].

We need to continue to invest in techniques and processes that allow use to continue our rapid rate of shipping product. It will allow us to produce more value to our end customers and have less unplanned work. We also have to realize that at the end of the day we are human and we will make mistakes which will lead to failure. No amount of process will avoid issues in Production. This means we need to adopt techniques and procedures that allow us to ship fixes to Production as fast as possible with high confidence.

#### References
- [0]http://gizmodo.com/heres-facebooks-little-red-book-a-guide-to-zuckerbergi-1706298694
- [1]http://www.slideshare.net/nicolefv/does-2016-sciencing-the-crap-out-of-devops
- [2]https://www.nist.gov/sites/default/files/documents/director/planning/report02-3.pdf
- [3]https://www.nist.gov/sites/default/files/documents/director/planning/report02-3.pdf
- [4]https://blog.fullstory.com/what-we-learned-from-google-code-reviews-arent-just-for-catching-bugs-b125a13aa292#.xkh303re1
- [5]https://codeascraft.com/2011/04/20/divide-and-concur/
- [6]https://zachholman.com/posts/deploying-software
- [7]http://businessofsoftware.org/2016/06/rock-solid-software-testing-without-hiring-an-army-trish-khoo-google-bos2015/
- [8]https://testing.googleblog.com/2016/11/what-test-engineers-do-at-google.html
- [9]http://nerds.airbnb.com/testing-at-airbnb/
- [10]https://testing.googleblog.com/2017/02/discomfort-as-tool-for-change.html
- [11]https://testing.googleblog.com/2016/05/flaky-tests-at-google-and-how-we.html
- [12]https://testing.googleblog.com/2016/11/what-test-engineers-do-at-google.html
- [13]https://blog.acolyer.org/2016/09/12/on-designing-and-deploying-internet-scale-services/
- [14]https://research.fb.com/wp-content/uploads/2017/01/paper_icse-savor-2016.pdf
- [15]https://zachholman.com/posts/how-github-works/
- [16]https://zachholman.com/talk/how-github-no-longer-works/
- [17]https://zachholman.com/talk/move-fast-break-nothing/
- [18]https://githubengineering.com/move-fast/

Thanks to Sean Walberg and Cian Whalley for editing this document. This would have been a jumbled mess without their help!