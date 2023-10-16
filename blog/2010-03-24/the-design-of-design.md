# The Design of Design
<img width="100" height="144" align="left" src="https://hectorcorrea.com/images/designofdesign.jpg" />Earlier this month I received a draft manuscript of Frederick Brook’s latest book [The Design of Design – essays from a computer scientist](http://www.amazon.com/Design-Essays-Computer-Scientist/dp/0201362988) <sup>[1]</sup> in which he reviews both what is design and how the design process works.

Although there is plenty literature on the concept of design and the design process Brooks feels there are several good reason to write another book on the subject.

The first reason that he mentions is that **the design process** has changed a lot since World War II and the new challenges have rarely been discussed. The new challenges that he mentions is that design is now a **team activity** rather than an individual one. Another challenge is that unlike designers of previous generations nowadays designers cannot longer built with their own hands what they design. Instead designs are captured in computer models and build by somebody else [p. xi]

The second reason why Brooks consider worthwhile writing a book on design is that “much mystery remains” on the subject and that this becomes “evident when we try to teach students how to design well” [p. xi] In this book Brooks uses his six decades of design experience to help expand the knowledge of how the design process works and how we teach it. In his book Brooks does not attempt to find or describe “a science of design” in fact he considers such a goal both impossible and misleading. Instead, the tone of the book is in the form of a few opinionated essays [p. xii]

The book is divided in six sections as follow:

* Section I: Models of Design
* Section  II: Collaboration and Telecollaboration
* Section  III: Design Perspectives
* Section  IV: A Computer Scientist’s Dream System for Designing Houses
* Section  V: Great Designers
* Section  VI: Trips through Design Spaces Case Studies

I found the first three sections of the book fascinating but was not as thrilled with the last three sections. In this review I am going to focus mostly on some selected chapters from the first three sections.


## Section I – Models of Design

### Chapter 1 - What is design?

<img width="120" height="179" align="left" src="https://hectorcorrea.com/images/notredame.jpg" />On the first chapter Brooks addresses both the basic question of what is design and how the design process works. Brooks starts with the following definition of **the verb design** from the Oxford Dictionary:

> "To form a plan or scheme of, to arrange or conceive in the mind … for later execution” [p. 4]

Brook uses a proposal from Dorothy Sayers to describe **the design process** as a three steps process in which an idea is conceived mentally outside time and space, then it’s implemented in time and space, and finally the implementation is used by someone else.

In the case of a musical composition the mental formulation (the idea) is first conceived in the composers mind then implemented in paper and ink, and finally the implementation is used by a conductor to execute it with an orchestra.

In a software project the same process happens when its designer conceives the idea of how the software will work, this idea is then implemented in source code, and finally the software is executed and consumed by users.

One of questions that Brooks tries to address in this book is whether there are invariant properties of the design process itself across multiple disciplines like the construction of buildings, software development, and other media. It’s evident that Brooks researched a wide variety of other authors and sources that have addressed the concept of design throughout history including philosophers, designers, and scientists


### Chapter 2 – How Engineers Think of Design – The Rational Model

In the second chapter Brooks describes what he calls the **Rational Model** for the design process. This model refers to an orderly and systematic step-by-step process to the design of things. He cites several sources that have proposed this design process including German mechanical engineers and people from the software engineering field. It’s important to highlight that **Brooks does not support this model** but considers useful to present it for several reasons that he discusses throughout the book.

In the Rational Model the designer starts with a primary goal and a series of secondary goals. After the goals have been defined we proceed to define utility functions (the weight of each goal against the entire design), constraints and resources so that the designer can proceed with a simple and systematic approach. This is how Brooks puts it:

> "Now, so the Rational Model goes, the designer makes a design decision. Then within the design space narrowed by that decision he makes another decision. At each node he could have taken one or more other paths, so one can think of the process of design as the systematic exploration of a design tree” [p15]

In software engineering the Waterfall Model is the representation of the Rational Model in which different steps of the design process happen orderly and sequentially.

Although in software development the Waterfall Model has fallen out of fashion among developers as we have realized how it does not fit with the realities of software development, **the Rational Model is still enticing to many people outside of the design process**. Proof of this is how, in general as an industry, we still work on contracts that require a clear requirements definition upfront, accurate estimates and timelines, and fixed bid contracts. These steps are only possible in the Rational Model where the requirements are completed ahead of time, they accurate, and the developers know exactly how these requirements are going to be implemented.

Brooks make an interesting observation when he notes that the Rational Model is actually a very “natural” model and evidence of this is the fact that people in multiple disciplines going from mechanical engineering to software development have arrived to it [pp. 29-30]


### Chapter 3 – What’s Wrong with the Rational Model?

<img width="100" height="150" align="left" src="https://hectorcorrea.com/images/whatswrong.jpg" />Although the Rational Model is the first model presented in the book Brooks quickly discredits it in Chapter 3 as he explains that this is just an ideal process that although somehow describes how we think the design process ought to work it is not how it works in real life [p. 22]

Brooks dedicates this chapter of the book to highlight why the Rational Model (or the Waterfall Model as we know if in software development) does not work.

Brooks states that **we don’t always know the goal at the onset**. Most of the times the goal itself changes as the design evolve and new ideas are explored. Brooks indicates that “the hardest part of the design is deciding what to design” [p. 22]. He points out that not only the design process is iterative but also the design-goal-setting process is iterative. To anyone that has worked on software development this is probably obvious and we all have stories to tell on how we typically go back and forth with the customer to decide what they really need once the software product starts to take shape. Most of the times the end goal is different than the initial goal as both the designer and the customer learn more about the problem and re-evaluate the goals, constraints, and resources.

Another thing that works against the Rational Model is that it is very typical that **the constraints and resources change** as the design process evolves and we know more about the problem and the end solution that we are developing.

In the Rational Model it is assumed that we can easily evaluate in the design tree how much value a design decision adds to the entire design (“the goodness of a decision” so to speak.) In practice this is hardly the case as most decisions are interconnected to one another. For example, in software development a particular design decision might affect significantly performance, cost, and integration. Evaluating objectively how a particular decision affects the whole design can be close to impossible.

Finally, although the Rational Model has been proposed by people from multiple disciplines, the reality is that **designers just don’t work this way**. Designers go back and forth and change their own designs as they go. On page 257 when talking about his own experiences as a designer, Brooks states

> "The boldest design decisions, whoever made them, have accounted for much of the goodness of the outcome. These bold decisions were due sometimes to vision, sometimes to desperation. They were always gambles, requiring extra investment in the hopes of getting a much better result."

Brooks closes the third chapter with this sentence:

> "The Waterfall Model is wrong and harmful; we must outgrow it"



### Chapter 5 – What are Better Design Process Models?

<img width="150" height="100" align="left" src="https://hectorcorrea.com/images/spiral.jpg" />After describing what’s wrong with the Rational Model, in Chapter 5 Brooks argues the need to have a dominant model to replace it. His reasoning for advocating a particular dominant model as opposed to just let one surface organically is that he is afraid that if we don’t push for one model in particular we risk having another inappropriate model surface and dominate the landscape as the Waterfall Model did in software development.

In particular, Brooks suggest that we use **Barry Boehm’s Spiral Model** for building software as the dominant model. The Spiral Model suggests an iterative process that more closely resembles the way designers really work. In addition this model is easy to memorize, visualize, and should help with the eradication of the Waterfall Model.

If you are interested in a quick summary of the Spiral Model you can find one in [Wikipedia](http://en.wikipedia.org/wiki/Spiral_model). The original 1988 paper by Barry Boehm can be found at the [IEEE web site](http://www.computer.org/portal/web/csdl/doi/10.1109/2.59).

Although Brooks does not reference newer development process model like the [Unified Software Development Process](http://en.wikipedia.org/wiki/Unified_Process") and [Scrum](http://www.controlchaos.com/about/) these are variations on the Spiral Model originally proposed by Boehm.


## Section II - Collaboration and Telecollaboration

<img width="120" height="80" align="left" src="https://hectorcorrea.com/images/train.jpg" />In the second section of the book, Brooks addresses two changes in design that have taken since 1900. In particular Brooks discusses the challenges of doing design work in teams (as opposed to solo designs) and collaboration in distributed teams via telecommunication tools (as opposed to collocated teams.)

Although most people would agree that collaboration is a good thing, Brooks points out that **collaboration in design is not a self-evident truth and certainly not universally true**. [p 64] Brooks points out that “most of the great works of the human kind have been made by one mind, or two working closely.” [p. 64]

In chapter 6 Brooks addresses the obvious question: If design by a single mind is so good why have we shifted to team design? Brooks attribute this shift first and foremost to the technology sophistication that has taken place in engineering (whether is construction or software engineering) in the last hundred years. With the level of specialization needed in most engineering areas people have been forced to become experts in certain areas and therefore we need to bring together experts from multiple areas to get the whole picture on any given project (say a new bridge, a new cell phone, or a new large software system.) The second reason Brooks talks about is that “team design becomes a necessity when it can accelerate delivery of a new product in a competitive environment” [p. 65] and this is paramount in this day and age when (right or wrong) being first to market is a driving force behind companies working on new designs.

Brooks points out that collaboration does not come without a cost. In chapter 6 he talks about the costs that one incurs when a team (rather than a single person) works on a problem. In particular he talks about the cost of partitioning the job among multiple people, teach teammates and learning from them, communication cost, and change control.

When it comes to design work however, Brooks things that biggest challenge is that the **conceptual integrity of a design** is much harder to maintain when a team works on the design. He talks about how solo designers keep design integrity subconsciously and how this can easily be affected when the design is split among multiple minds. 

Since the reality is that nowadays team design is the norm rather than the exception, Brooks proceeds to give ideas and steps that can be used to help teams to achieve good designs. In particular he talks about having a system architect that is in charge of making sure the integrity of the design is achieved even though multiple members of the design team might have different ideas. In Brooks words “The architect serves during the entire design process as the agent, approver, and advocate for the user as well as for all the other stakeholders” [pp. 71-72].

Brooks considers **the two-person team** a special case that is a very good approach to design as it forces the designers to have to state why their decisions are taken and this in turn forces a quick validation among the team [pp. 81-82] The reason for this is that two people can easily work together and maintain design integrity but somehow this does not scale well with more than two people on the team.

Brooks points two aspects of the design process that benefit from team collaboration. He highlights the value that a team with multiple points of view brings forth it when it comes time comes to decide what to design (the needs of the customer) and also during design review sessions.

In Chapter 7 Brooks addresses the challenges that a **distributed design team** faces. Brooks is very much aware that “distributed design will only increase” [p. 93] and provides several ideas to help distributed team work. In particular he talks about the value that face to face time at the beginning of a project is crucial even when a team will eventually work distributed.


## Section III – Design Perspectives

<img width="120" height="179" align="left" src="https://hectorcorrea.com/images/designperspective.jpg" />On Chapter 8 Brooks reviews the two different schools of thoughts of the Rationalists (like Rene Descartes) and Empiricists (like Galileo Galilei) and how they apply to design.

On Chapter 9 Brooks talks that team design makes **the need of explicit models** on what’s being designed more important than with solo designs. This is because designers in a team tend to assume that they are all sharing the same assumptions and in fact they might not. Brooks puts it like this: “If the team does not draft a common set of explicit assumptions, each designer will work with a distinct set of implicit ones” [p. 115] and then he adds “as soon as the designer starts to make explicit use models, trouble strikes: he is rudely confronted with how much he does not know. The very effort forces him to ask questions he might not otherwise have asked until much later. This is an unmitigated good” [p. 115]

On chapter 10 Brooks talks about resources and, on page 119, he summarizes the chapter rather succinctly:

> "If a design, particularly a team design, is to have conceptual integrity, one should name the scare resource explicitly, track it publicly, control it firmly.”

There is far more insight and good advice for designers throughout the rest of the rest of the chapters of Section III of the book than I could cover on this blog post.


## Section IV, V and VI

<img width="150" height="100" align="left" alt="" src="https://hectorcorrea.com/images/punishment.jpg" />As I mentioned at beginning of this blog entry, I did not find the last three sections of the book as interesting as the first three sections.

In Section IV of the book (A Computer Scientist’s Dream System) Brooks describes his vision for “an ideal computer system for the architectural design of houses and other buildings. “ [p. 204] Chapter 17 presents a vision on how a person could convey a design to a machine (mind to machine) where as Chapter 18 presents the opposite, how a machine could convey to a person a design by using not only visual clues but also audio and tactile feedback.

In Section V Brooks addresses two different problems. In Chapter 18 he addresses the difficult question on how people and processes related to each other and the role of a process in design. This is a good chapter where Brooks describes the opposing views between the need of a design process to aim at predictability and how predictability is hardly a friend to great designs [p. 233] In Chapter 20 Brooks talks about his experience on how to developer great designers.

The last section of the book (Trips through Design Spaces: Case Studies) is dedicated to seven case studies in which Brook participated. This whole section was a big disappointment to me. I am not sure what Brook had in mind when he wrote this part of the book and what value he meant to add to the study of design when he included it on the book. This section includes case studies for the famous System/360 Architecture and the IBM Operating System/360 projects that Brooks managed in the 1960s and also some other personal projects including three personal constructions projects (!) to his own house as well as the design of a book on computer architectures.


## Summary

All in all I think the first three sections of the book make the book a great reading and would recommend it to all software developers interested in improving and understanding the design process used to create software solutions.


### References
[1] *The Design of Design – Essays from a computer scientist*; Frederick P. Brooks; Pearson Education; 2010 (Draft Manuscript as of 1/24/2010)