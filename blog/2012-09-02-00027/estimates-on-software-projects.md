# Estimates on Software Projects
Estimates is one of the most controversial topics on software development, including the process to calculate them and the value that they add to the software development process.

Every team that I have worked with needs to provide estimates on how long it's going to take to complete a specific feature of a system. Yet, most teams seem to struggle with this activity. Developers enjoy attending a meeting to provide estimates as much as they enjoy visiting the dentist. Project owners typically complain how unreliable estimates on software projects are, to them is unbelievable that even that developers have been writing software for many years cannot give accurate estimates.

In my experience there are several reasons why providing estimates is so hard:

* Poor specifications/Lack of domain knowledge
* Technology challenges
* Developers are optimistic
* Software development is tough


## Poor specifications

Poor specifications is the most commonly voiced reason for inaccurate estimates. And for a good reason. It is typical for developers to be asked to estimate features that they don't fully understand. The client requests a new screen to do X but there is a lot of unwritten expectations for this new feature that users will demand once they start using it but that developers don't know about. This is usually due to lack of business domain knowledge. Developers are trained on software development and very little (or nothing) in the specific business domain. If the software that is being written is for insurance billing is very unlikely that the developers will have enough education and training on insurance and/or accounting. They might have been working many years in software development but this might be the first time they are faced with a screen for insurance billing purposes.

Even when a decent amount of conversation between developers, business analysts, and product owners take place to explore what the requested feature will entail, there is inevitable a lot of things that are left unsaid that will be find out when the feature is developed and presented to the user. I've worked on companies where we received reams of paper with specifications that looked like they covered every possible detail about the feature to be built just to find out that (1) they are still incomplete or (2) they don't really represent what the customer wants. I've produced my fair share of specs that I thought were enough to provide accurate estimates just to find out that nope, there is still a lot left unsaid that will not be discovered until the software is written and presented to the users for feedback.


## Technology challenges

Most software development groups try to stay up to date on technology and upgrade to new versions of compilers, databases, development environments, and such. This is usually a good thing since these new tools are meant to speed up the development process and make better use of existing hardware. But there is a cost associated with these upgrades. Developers need to spend time performing upgrades, learning new tools and ways of doing things, and this might not be cheap. Plus this happens on a regular basis. For example, since 2000 Microsoft has released three versions of C# (C# in 2000, C# 2.0 in 2005, and C# 3.0 in 2007) during the same time Microsoft has released three versions of SQL Server (SQL 2000, SQL 2005, and SQL 2008.)

You may be tempted to say 'the heck with it, we are not going to update anymore' but there is also a cost associated with this. For once, your system might not run on new computers or just look ugly (e.g. imagine a DOS application running on Windows.) Secondly, developers tend to be technology driven and you may lose some of your best developers if they see that they are falling behind in technology and their skills are not up to date.


## Developers are optimistic

Most developers that I've met (myself included) are optimistic by nature. We are optimistic people and we like to please our customers. This has an impact on the estimates that we provide. We tend to provide estimates for the best case scenario even when experience tells us that the best case scenario hardly ever materializes in software development. Even when we try to account for the unexpected we do it in an optimistic way. Or as Brooks will say in the Mythical Man-Month [p. 15] "the assumption that all will go well has a probabilistic effect on the schedule."


## Software development is tough

Software development is a tough activity. It requires dealing with abstractions, a lot of unknowns, on a tight schedule, and with new tools and technologies. Most activities in a business environments deal with physical limitations like size, weight, cost, counts, and other well understood constrains. Software on the other hand deals with "almost pure thought-stuff" [Brooks, p. 7] Estimates on an unconstrained environment like this are not trivial.


## Do we need estimates?

Yes, we definitively do. Despite the grim picture that I might have painted so far, I strongly believe that estimates are valuable in software projects. Estimates are like price tags in the sense that they allow product owners make better decisions when it comes to deciding priorities for a software project. If there are four new features being requested by the users and three of them will take one week each but the fourth one looks like it is going to take two months alone, the product owner will be better able to decide what is best for the product. She might decide to complete the three one-week features and delay the large one for a better time, or vice-versa. But she will be able to make this decision having an idea on the size of the features.

In my experience there are two things that you can do to get the most out of estimates for software projects *even when* they are not accurate.

One is to divide and conquer. Estimate small blocks of functionality so that even if estimates are not accurate they are not off by a lot either. If a task is estimated to take 2 days and it takes twice as much you can deal with it 2 days later and adjust your planning. However, if a task is estimated to take 2 months and it takes twice as much, four months later is probably too late to address the problem. Even more, if developers in a team can blow a 2 days estimated (for whatever reasons) imagine the likelihood of blowing a 2 months estimate.

The second thing that we can do is to constantly calibrate project expectations. To put it bluntly be realistic and use history as a guidance on how long stuff takes to be completed rather than be guided by hope. It is very common for people to say &quot;this time it took me 2 weeks to complete X but with what I know now it would take me only 1 week next time.&quot; This hardly ever works out. For once, remember that developers are optimistic. We are bound to take this posture. If it took 2 weeks to do something there is probably a very good reason for it. You should use that number as your baseline in the future and only reduce the estimate once you have proven than it can be done in half as much. Koskela and Howell have a great [paper](http://www.leanconstruction.org/pdf/ObsoleteTheory.pdf) in which they propose moving away from the thermostat model (in which an arbitrary productivity goal is set at the onset) into a scientific experimentation model in which we adjust based on previous results.


## How to calculate estimates?

Since estimates are approximations, not promises, I prefer a light weight approach to calculate them rather than spending a whole lot of time on them. By light weight I mean the team getting together for no more than 3 hours to estimate what we think will be able to accomplish in the next two weeks. In my experience teams can come up with "good enough" estimates in relatively short term. David Anderson has a tongue-in-cheek post where he calls for people to [stop estimating](http://www.agilemanagement.net/Articles/Weblog/StopEstimating.html). In reality he calls for [agile estimating](http://www.agilemanagement.net/Articles/Weblog/AgileEstimating.html) rather than no estimates at all. In agile methods not a lot of time is spent calculating something that we cannot guarantee. It's better to spend that time producing software and delivering features to the user rather than promises.

Mike Cohn's book on [Agile Estimating and Planning](http://www.amazon.com/Agile-Estimating-Planning/dp/0131479415) is a very good book on the subject. He does a great way of describing the use of story points and velocity to do long term planning on projects. Highly recommended if you are doing agile software development.

Joel Spolsky has an article on [Evidence-Based Scheduling](http://www.stickyminds.com/BetterSoftware/magazine.asp?fn=cifea&amp;id=94) (EBS) in which he uses a Monte Carlo simulation to calculate the likelihood that a particular estimate will be met. Spolsky's approach sounds interesting but I have not tried it myself. The fact that uses historic values to calculate probabilities sounds promising. Still, I am afraid that it requires more time and effort than the value that it provides but I don't have any experience with it.


## What to do about missed estimates?

Of the things that are controversial about estimates the one about missed estimates is probably the worst. It's almost taboo. Although everybody misses estimates but nobody wants to talk about it.

If you (or your team) misses an estimate, get over it. It happens. Don't let it bring you down. Review why you missed it and act on your findings. Perhaps the task is just more complicated than you thought -- it is perfectly OK to admit this. Maybe you need to break the task down in smaller chunks next time, or you need less distractions. What ever you do however, make sure to use the knowledge that it took longer than you expected next time you estimate a similar task. Don't tell yourself that &quot;next time will be better because I've been there before.&quot; Remember: use history as a guidance rather than hope.

If somebody else misses an estimate see the previous paragraph. Talk with them to see why it was missed and act on it. Don't expect that because somebody thought something would take 5 days that is the time it will take. Remember that it is an estimate, a forecast.

There might be instances where a team or an individual developer *constantly misses estimates by a long shot*. If that is the case, there are perhaps larger issues that need to be addressed. Does the team/developer has the right tools for the job? Is the team/developer qualified for the job? Are the expectations for the team/developer realistic? Is it always the same team/individual? These are perfectly valid questions on a team/individual that is not performing at the pace that the business expects. The problem might be the team, the expectations, or both.


## The role of the product owner

In my experience most product owners learn the effectiveness of their team's estimates in a few cycles. Product owners are not necessarily as optimistic as developers and they can provide valuable feedback to the team after just a few rounds of estimates. This is great feedback that a lot of teams don't use. Product owners bring different experiences, business knowledge, and personality styles to the team that can be very useful when estimating and setting expectations.