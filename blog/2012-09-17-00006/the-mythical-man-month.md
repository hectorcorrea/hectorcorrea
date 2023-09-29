# The Mythical Man-Month
Last week I finished reading [The Mythical Man-Month](http://www.amazon.com/Mythical-Man-Month-Software-Engineering-Anniversary/dp/0201835959) by Frederick Brooks for the third (or so) time. Although this book was originally published in 1975 it is still a great reading for anyone involved in software development. The edition that I read is the 20th anniversary edition and has a few extra chapters with updated information.

There are two chapters that I particularly like in this book: The Mythical Man-Month and No Silver Bullet - Essence and Accident.


## The Mythical Man-Month

In this chapter Brooks explains why using

> "man-month as a unit for measuring the size of a job is a dangerous and deceptive myth. 
> It implies that men and months are interchangeable."

He goes on to explain that

> "men and months are interchangeable commodities only 
> when a task can be partitioned among many workers 
> with no communication among them. 
> This is true for reaping wheat or picking cotton; 
> it's not even approximately true for systems programming"

This myth is a typical problem in our industry. I cannot enumerate how many times we've estimated a job to take X number of months by Y number of developers (say 6 months by 2 developers) and then somebody come and say "but if I give you twice as many people you'll finish in half the time, right?" (say 3 months with 4 developers.) This hardly ever works out. Having more people in the team is not bad, but comes with a price to the team's productivity mainly due to the communication and work allocation that has to happen among team members. There is a logical tendency to underestimate this burden because we tend to see men/women interchangeable with months.

In most projects that I work the team size is rather small (5-10 members) compared with the size of the team that Brooks worked on (with hundreds of members) when he managed the IBM's OS/360 software group back in the sixties. Yet, the Brooks' Law (adding manpower to a late software project makes it later) still applies to smaller projects.


## No Silver Bullet - Essence and Accident

This chapter is actually a reprint from an article that Brooks wrote in 1986 (ten years after the original book was published) and has been added to the 20th anniversary edition. In this chapter Brooks declares that in the next decade (1986-1996) there will be no major technological or managerial development that will improve our productivity by one order of magnitude.

A-la Aristotle, Brooks divides the difficulties that we face when we develop software in essence and accidents:

> "Essence- the difficulties inherent in the nature of software 
> -and accidents- those difficulties that today attend its production 
> but that are no inherent."

With this in mind, Brooks explains that there are two kinds of tasks involved in software development: essential tasks and accidental tasks. Essential tasks are the ones by which we develop abstract software constructs for the problem that we are trying to solve in our programs. Accidental tasks are ones that we do in order to implement these abstract constructs in programming languages and machine code.

The advances that have happened in software development that have helped us improve our performance address only the accidental tasks (e.g. higher level programming languages, faster and smarter compilers, and better IDEs.) However, little has been done to improve how we carry on the essential tasks and hence our productivity has not improved by an order of magnitude. Building software is (still) inherently difficult.

If you've been in the software industry for a while you've probably have seen no shortage of silver bullets wannabes. Who can forget about CASE tools? How about artificial intelligence and expert systems? Let's not forget UML and the Unified Software Development process.

This blog entry (and Brooks article) does not try to diminish the progress that we have had in software development over the years. Our tools have improved incredibly over time. Nowadays it takes a few lines of code to do what it used to take hundreds (if not thousands) of code just a few decades ago. Yet, they have only addressed the accidental part of the equation.

There are more gems in Brooks' book and as I said at the beginning, I highly recommend it to anyone that works on software projects.

If you like Brook's writings, I also recommend his other book [The Design of Design](https://hectorcorrea.com/blog/the-design-of-design/40).