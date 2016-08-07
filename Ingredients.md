## Ackee apps ingredients
🍚 For cooking the best apps in town we use the finest ingredients. 🍳

* 👪  3rd party libraries 
* 🏛   Solid architecture design 
* 🤗  Libraries we wrote ourselves (you can find some of them on our GitHub)
* 💩 Templates & Snippets which makes cooking easier. 

Result? Consistent code across various projects, quality codebase and happiness on all sides. 😍

## Libraries
Set of Libraries we use during development
### Networking
### CoreData
### AutoLayout

### Reactive Cocoa and MVVM

We love streams. Streams are good for you, and for your app.
[ReactiveCocoa](https://github.com/ReactiveCocoa/ReactiveCocoa) has served us well since 2014 and we believe
it outperforms the [RxAnyLanguage family of frameworks](https://github.com/ReactiveX)
by making better use of swift's features. 
Learn the basics of ReactiveCocoa on [their github](https://github.com/ReactiveCocoa/ReactiveCocoa),
then come back to see how we do [MVVM](https://en.wikipedia.org/wiki/Model–view–viewmodel).

#### Model-View-ViewModel

Reactive streams (or signals) hold our apps together.
They are the few lines of code which do most of the logic.
They transform the Model data and deliver it into the View layer.
And swift's strong typing combined with ReactiveCocoa's well chosen,
limited set of functional transformations make it nearly impossible to make a simple mistake.
But by using ReactiveCocoa, you are placing a lot of requirements on your code.
It needs to react to any event, at any time, with many signals running in parallel.
How do you not get lost and create deadlocks, memory leaks and more?

The answer is unidirectional dataflow.
The [MVVM](https://en.wikipedia.org/wiki/Model–view–viewmodel) pattern enables
us to structure the app in such a way, that all of the streams are flowing in the same direction.
The Model layer is owned by the ViewModels, which publish the data in a view-friendly and observable way.
The Views own the ViewModels and always update to their latest state.
User input handling in the View layer is very light.
The View usually just calls a Void method or an Action on the ViewModel and that's it.
The ViewModel has full control over what happens next.
No waiting for a result, no `updateView(model:)` calls,
just knowing that if some ViewModel data changes as a result of this or any other action, it will be observed. 

[See an example of MVVM here](https://github.com/richeterre/SwiftGoal/tree/master/SwiftGoal)

#### How to be a great reactive programmer

- Now that you've finished learning [ReactiveCocoa](https://github.com/ReactiveCocoa/ReactiveCocoa)
a little, **learn it a lot**.

- **Always prefer `<~` bindings to `start`/`observe`.**
The reactive extensions that you or others write on classic objects
are meant to rid your code of uninteresting and error prone responsibilities, like lifecycle management.
If you've `start`ed/`observe`d a signal, use `takeUntil(_:)` to explicitly stop it. Don't assume the ViewModel won't outlive it's View.
- **Always prefer `<~` bindings to everything.**
If you like the time and lines of code saved by the convenience of reactive code,
you will love what it does to debugging.
You come to a codebase you've never seen, and a label is not showing the proper text.
You open up the ViewController to get familiar with the code and see this line `label.rac_text <~ foo`.
Well, its probably this `foo`king fella not sending the correct values.

- **Use sideffects sparingly.** You have this signal and its bound to the View just nicely,
but you also have to let this other guy know that something is happening on the signal. 
You should pause and convince youself that your design is good.
Sometimes, the answer will be *"It's not, but I have no idea how to write this better"*.
That's ok, at least you know to be careful when writing this code
or discuss with a colleague if the problem seems serious.

- **Ask the right questions (and lots of them).**
ReactiveCocoa is a consise way to define the behavior of a program, but it can't match the human language.
**Ask questions like:** *"I have this data. How do I transform it into this other data?"*,
*"Is there an operator which basically does this thing?"*
**Don't ask questions like:** *"So I have these 3 signals, right? And somehow it's not flatMappin' for me."*    

- **Practise your flatMappin'**.
So, you like reactive code, but the compiler doesn't? Chances are it's a simple mistake.
Xcode shows an error like *`ambiguous use of flatMap(_:, trasform:)`*,
but what the compiler is really saying is:
![Alt Text](http://img.pandawhale.com/post-21975-Jerry-Maguire-help-me-help-you-tj9G.gif)

    When writing a `flatMap`:
    1. Ensure that the Error types match between the outer (input) signal and the inner (output) signals. Use `promoteErrors(_:)`, `mapError(_:)` or `flatMapError(_:)` if they don't. 
    2. Annotate the transform block with a return type (input type should not be needed).
    3. Write `return .empty` on the first line.
    4. Build you signal in a local variable until you can verify by *alt+clicking* that it matches the return type.
    5. Generally, try to keep the compilation error as local as possible.
    6. **Clean up**. Noone cares how much you've struggled writing this code,
    erase all the unnecessary type annotations and some of the local variables when you're done.

    Steps 2-5 are optional, but don't expect the compiler's help unless you can get it right on the first try.

- **Don't be shy and [play with the balls](http://neilpa.me/rac-marbles/).**

- **Write tons of extensions**.
A reactive app is a clever structure made up of small building blocks at the core
and sometimes ugly hooks on the outside (when connecting the streams to UI elements or other non-reactive API's).
Don't pollute you codebase, push all the sideeffect's into well-defined extensions on (or wrappers of) existing objects. 
If you can't find an excuse why an API shouldn't be wrapped reactively, **do it**.       

- **[ReactiveCocoa source](https://github.com/ReactiveCocoa/ReactiveCocoa/tree/master/ReactiveCocoa/Swift) is documentation**.
So you've read them all, the ReactiveCocoa best practices and tutorials are great.
But when you really need to know what an operator does, the source is actually pretty simple and understandable.
Maybe because its written in ReactiveCocoa ;).
- **Extend SignalProducerType with protocol extensions**
When you have a good reactive app architecture, you write very little code.
This gives you time to figure out how to write even less code.
Improve your own reactive flow with convenience extensions that work on signals with specific Value and Error types.    
## Templates & Snippets

