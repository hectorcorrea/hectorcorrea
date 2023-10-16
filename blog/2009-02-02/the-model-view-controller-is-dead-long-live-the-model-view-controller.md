# The Model View Controller is dead, long live the Model View Controller
The last few days I've been reading [Microsoft .NET: Architecting Applications for the Enterprise](http://www.amazon.com/Microsoft-NET-Architecting-Applications-PRO-Developer/dp/073562609X) by Dino Esposito and Andrea Saltarello. On Chapter 7 Dino and Andrea talk about the Presentation Layer and in particular they touch on the Model View Controller (MVC), Model View Presenter (MVP), and Presentation Model (PM) design patterns. I really like how they demystify MVC and MVP and put them in context. Dino and Andrea start describing how these design patterns have evolved over time and state that:

> the definition of MVC that worked in the 1980s and even the 1990s might not work for today. 
> As a result, probably nobody uses MVC today as its authors originally devised it.

I completely agree with this statement and as a matter of fact this quote is the reason I stopped on the Presentation Layer chapter as I was browsing through the book even though I didn’t have an immediate need for Presentation Layer patterns. I was actually looking for Business Layer and Service Layer Patterns but that’s a topic for a future blog entry.

Another interesting observation that Dino and Andrea make is that “when MVC was initially developed it was intended to be used on the whole application and not just in the presentation layer”. However, since these days most developers intuitively design applications in layers as opposed to building monolithic applications as it might have been the norm in the 1980s, the role of the MVC pattern has shifted to a presentation layer pattern more than application level pattern.

Dino and Andrea do a great job of explaining the MVC pattern with a simple sequence diagram rather than using the quintessential chart with three circles and the words model, view and controller inside them. Below is a drawing of the sequence diagram that they use in the book:

![Model View Controller pattern](https://hectorcorrea.com/images/mvc.jpg)

From this diagram is easy to see that upon a user action (e.g. click of a button) the view talks to a controller, and the controller in turn talks to the model. It makes me wonder if this pattern should have been called View Controller Model pattern instead. The model notifies the view that changes have occurred in the model and the view in turn reads the new model. Another observation that Dino and Andrea make is that the *model* in MVC is what we call these days *the business logic layer*.

**The View in MVC** represents the controls that are drawn on the screen. In a .NET application they might represent Windows Forms controls or Web Controls. *Ideally* the view should be as simple as possible. The view should just draw the controls, intercept user actions, and forward them to a controller. In *practice* the view typically has some logic inside of it for handle things related to the presentation layer (e.g. data binding and sometimes even simple data validation.) There is a trade-off between having the simplest of the views (one with no logic) and one with some logic on it. If the view has no logic the controller tends to be more involved but there is only one place with code logic on it. If the view has some logic on it the controller tens to be simpler but now you have logic in two places. This is neither right nor wrong. It’s just a decision that you as a developer will face and need to choose what is best for you given the particular application that you are building.

From the sequence diagram above you can also see how the **Controller** talks to the model (business layer) to take care of the request made by the user through the view. One of the main jobs of the controller is to script the required calls to the model. If the user’s action requires a new view the controller is also responsible for creating a new view, model, and controller and passing the control to this new MVC triad. If the user’s action does not require a new view then the controller just scripts the calls to the existing model. Something to keep in mind is that selecting which view to go to next can be a complex job in a real application. There is nothing intrinsic in MVC to make this simpler.

A common misunderstanding is that the controller in MVC separates the view from the model. However, as Dino and Andrea point out, and as you can see from the aforementioned sequence diagram, in MVC “the view knows the model directly and the model knows the view through the Observer relationship” Newer patterns (some of them derived from MVC) have addressed this issue and made other improvements to MVC to produce design patterns more suitable for today's applications. To put it in the words of Dino and Andrea:

> It is a sharp and bold statement, but we have to make it: today classic MVC is gone. 
> However, some of its variations are healthy and thrive. 
> They are Model2 for the Web and MVP for both Web and Windows. 
> In turn, and only more recently, MVP has undergone a facelift. 
> In July 2006, Martin Fowler proposed to retire MVP entirely and replace it with two variations 
> Passive View (PV) and Supervising Controller (SVC).


## Model 2: MVC for the web

Model2 is a new pattern derived from Model View Controller. Again, to quote Dino and Andrea “Model2 is just MVC adapted to a new medium – the Web – that just wasn’t around at the time MVC was first devised” Model2 was originally created for Java Server Pages but is now also used in the [Microsoft’s ASP.NET MVC Framework](http://www.asp.net/mvc/) which makes it the more relevant for .NET developers.

To review the differences between Model2 and the classic MVC let's look at a sequence diagram of the Model2:

![Model2 pattern](https://hectorcorrea.com/images/model2.jpg)

There are a couple of things that become evident as soon as you compare this diagram with the classic MVC diagram that we reviewed first. The first thing is that the Model2 diagram is a little bit more complicated than MVC since there are more components involved. Secondly there is still a view, a model, and a controller embedded on it.

Another two of things that are also shown in this diagram that might not very evident at first are that (1) the view is rather passive in this pattern as it does not talk to anything and (2) in Model2 the controller (and not the view) is the one that talks to both the model and the view which is quite different from classic MVC.

The fact that the view becomes passive in Model2 means that is very much just a set of controls that are drawn based on some information (the “viewModel”) passed from the controller. ViewModel is a class with data like a dataset or a custom data class that the view uses to render HTML controls (remember that Model2 is targeted to the web.) *The view in this case receives data through the viewModel but does not have access to the business layer (Model.)* Although this is a subtle difference it makes the view in Model2 simpler than in MVC which is one of the goals on some frameworks like the Microsoft ASP.NET MVC framework.

So what about the new elements introduced in Model2 like Browser and Front Controller? Browser represents the users’ browser and, as the diagram indicates, its job is to submit HTTP POST requests and render HTML.

The Front Controller in ASP.NET Front Controller is implemented via an HTTP module that captures the requests, analyzes them and decides what controller should handle them. Scott Gu has a very good post on [how this works](http://weblogs.asp.net/scottgu/archive/2007/12/03/asp-net-mvc-framework-part-2-url-routing.aspx) in ASP.NET MVC. 


## Model View Presenter

As I mentioned before, another variation of the MVC design pattern is the  Model View Presenter (MVP) pattern. MVP has in turn been superseded by two other patterns (Passive View and Supervising Controller) that are worth exploring but are beyond the scope of this blog entry. Dino and Andrea do a great job of explaining the differences between these three patterns on their book.

I highly recommend [Dino and Andrea's book](http://www.amazon.com/Microsoft-NET-Architecting-Applications-PRO-Developer/dp/073562609X) to anyone doing applications with .NET and that has not reviewed design patterns in a while. Dino and Andrea do a great good job describing well known design patterns for business, service, data access, and presentation layers in a modern perspective and targeted for .NET development.

In addition to their book, Dino has a very good MSDN article on [ASP.NET Presentation Patterns](http://msdn.microsoft.com/en-us/magazine/dd252940.aspx) that is worth checking out.