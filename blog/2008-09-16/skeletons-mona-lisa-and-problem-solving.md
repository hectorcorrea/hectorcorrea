# Skeletons, Mona Lisa, and Problem Solving
One of the best practices when building applications that I've learned over the years is the value of always having a running version of the application available to show end-to-end progress on the system being developed. Although this is common sense it's easy to get caught on the day-to-day activities and lose track of these things.

A typical situation in which teams seem to forget the value of always having a running version of the application is when writing a brand new application. In this scenario is common to have a bunch of components half-way written and not ready for production and most development teams tend to be OK with this. I am OK with this *as long as they all compile and can be run successfully to show the functionality implemented so far*. It does not matter the system can only perform a sub-set of features that the final system will have. It should always run so that people can experience first hand how each of the modules interact with each other.


## Walking Skeleton

<img alt="Walking Skeleton" align="left" src="https://hectorcorrea.com/images/skeleton.jpg"/>In trying to explain this concept to a friend of mine I found that there is even a pattern that explains this idea when it comes to building new applications. Cockburn<sup>[1]</sup> calls it a [Walking Skeleton](http://alistair.cockburn.us/index.php/Walking_skeleton):

> "A Walking Skeleton is a tiny implementation of the system 
> that performs a small end-to-end function. 
> It need not use the final architecture, 
> but it should link together the main architectural components. 
> The architecture and the functionality can then evolve in parallel."

As Cockburn points out a Walking Skeleton is different from a proof of concept (or spike) in the sense that the later is meant to be throw away code while the Walking Skeleton is meant to evolve over time. 

This approach relies heavily on having a procedure in place to support the evolution of the code as the skeleton is fleshed out (pun intended.) Cockburn calls this strategy Incremental Rearchitecture.

I recommend that teams use unit testing to make sure the code that performs some basic features today remains fully functional tomorrow as new few features are implemented and the architecture of the system updated to accommodate new features and new ideas.


## Mona Lisa

<img alt="Mona Lisa" align="left" src="https://hectorcorrea.com/images/monalisa.jpg"/>On his article [The Neglected Practice of Iteration](https://www.stickyminds.com/article/neglected-practice-iteration) Jeff Patton talks about the difference between iterating and incrementing (no, they are not synonyms) and touches on the idea of a Walking Skeleton from a different angle.

Jeff uses a Mona Lisa drawing to describe the differences between an iterative and an incremental approach to software development. If we were to use a *pure incremental* approach to drawing the Mona Lisa we would start by drawing to perfection a section of this painting (say her hands), then we'll draw completely her arms, then her face, and so on and so forth. Using an iterative approach we would start by drawing a sketch of the Mona Lisa in pencil (that's our first iteration), then we'll do a second iteration in which we increment the detail and perhaps give some coloring to the drawing, then we'll do a third iteration and put the final touches (keep incrementing the detail) on the painting. His article has great images that show this graphically.

The point of Jeff's article is that you need both (iterations and increments) in software development. A lot of people thing these two words are synonyms and use a pure incremental approach in which they work one a single module of the software to perfection before moving to the next module. The pure incremental approach has the disadvantage that neither the user nor the developers get to see the complete picture until the system is complete...and by then is usually too late. By using an iterative and incremental approach both the users and the developers get a rough idea of the whole system early on and how each module relates to each other.


## Depth-First versus Breadth-First Problem Solving

On their book Lean Software Development the Poppendiecks<sup>[2]</sup> talk about two different ways to solve problems: Depth-First versus Breadth-First.

> "Breadth-first problem solving might be thought of as funnel, 
> while depth-first problem solving is more like a tunnel. 
> Breadth-first involves delaying commitments, 
> while depth-first invokes making early commitments."

The breadth-first approach is similar to the Walking Skeleton in the sense that aim first to get an application running end-to-end and then incrementally update its architecture as more is known about the problem domain.

I think both approaches are complimentary, just like incremental and iterative are. There are times where breadth-first is preferred over depth-first and vice-versa. The Poppendiecks put it in these words:

> "Notice that both breadth-first and depth-first approaches require expertise in the domain. 
> A depth-first approach will work only if there was a correct selection of the area to zero in on. 
> Getting this selection right requires two things: 
> someone with the expertise to make the early decisions correctly and 
> assurance that there will not be any changes that render these decisions obsolete. 
> Lacking these two conditions, a breadth-first approach will lead to better results."

One of the observations that the Poppendiecks made on their book is that "most novice designers are biased toward the depth-first approach." The irony on this is that depth-first requires people to get the decision right early on, something that a novice designer (by definition) probably won't do. Further more, I believe this bias on novice designers is the reason they tend to apply a pure incremental approach instead of an iterative and incremental approach.

Breadth-first work better than depth-first when the knowledge of the business domain is expected to evolve (as it typically does in software development) and it is also very effective when the domain is stable (e.g. you have strong knowledge about the problem domain.) Again, in the words of the Poppendiecks:

> "A breadth-first approach requires someone with expertise to understand 
> how the details will most likely emerge and the savvy to know when the time to make commitments has arrived. 
> However, the breadth-first approach does not need a stable domain; 
> it is the approach of choice when the business domain is expected to evolve. 
> It is also an effective approach when the domain is stable."

Personality types play a big factor in the way people use breadth-first or depth-first approach. This is an important consideration since there are probably people in your team that would favor one approach over the other. This is OK. Remember that these approaches are complimentary. When you are not sure about the domain use a breadth-first approach, once you know enough and are ready to make a commitment go deep.

### References
[1] Cockburn, Alistar. *Crystal Clear A Human-Powered Methodology for Small Teams*. 2005. Addison Wesley. Pages 49-53.
[2] Poppendieck, Mary et al. *Lean Software Development An Agile Toolkit*. 2003. Addison Wesley. Pages 60-62.