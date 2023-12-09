



[![](/images/content-public/ann/autumn/read.svg?id=0d119719d4d53f2e62fc6535cb544b74){loading="lazy"
style="width: 32px; height:32px;vertical-align: middle;"}
![](/images/content-public/ann/autumn/tea-cup.svg?id=f95aba0fef52083e2dd0a8a64068e37f){loading="lazy"
style="width: 32px; height:32px;vertical-align: middle;"} [Autumn
SALE]{.announcement-link-text}
![](/images/content-public/ann/autumn/mulled-wine.svg?id=ad4bec48a83ede3e72766d40a6a837ed){loading="lazy"
style="width: 32px; height:32px;vertical-align: middle;"}
![](/images/content-public/ann/autumn/maple-leaf.svg?id=63cdc79ea962a2657a57f44a22d092b9){loading="lazy"
style="width: 32px; height:32px;vertical-align: middle;"}](/store)





[[]{.cart-text} ](#checkout){.btn .cart .open-checkout} [
[]{.btn-text-span .d-none .d-sm-inline-block .d-lg-none
.d-hg-inline-block}](#checkout){.btn .btn-secondary .checkout
.open-checkout}








[](/){.home} / [Design Patterns](/design-patterns){.type} / [Behavioral
Patterns](/design-patterns/behavioral-patterns){.type}


# Mediator {#mediator .title}


Also known as:
[Intermediary, ]{style="display:inline-block"}[Controller]{style="display:inline-block"}



##  Intent

**Mediator** is a behavioral design pattern that lets you reduce chaotic
dependencies between objects. The pattern restricts direct
communications between the objects and forces them to collaborate only
via a mediator object.

<figure class="image">
<img
src="/images/patterns/content/mediator/mediator.png?id=0264bd857a231b6ea2d0c537c092e698"
srcset="/images/patterns/content/mediator/mediator-2x.png?id=250c2bf72ca1fdee2e6d97ed5a4765f2 2x"
width="640" alt="Mediator design pattern" />
</figure>



##  Problem

Say you have a dialog for creating and editing customer profiles. It
consists of various form controls such as text fields, checkboxes,
buttons, etc.

<figure class="image">
<img
src="/images/patterns/diagrams/mediator/problem1-en.png?id=86f99055b3e60bb8834dcc7222922bdf"
srcset="/images/patterns/diagrams/mediator/problem1-en-2x.png?id=e868165bd04a9438857d6ad41528024c 2x"
loading="lazy" width="600"
alt="Chaotic relations between elements of the user interface" />
<figcaption><p>Relations between elements of the user interface can
become chaotic as the application evolves.</p></figcaption>
</figure>

Some of the form elements may interact with others. For instance,
selecting the "I have a dog" checkbox may reveal a hidden text field for
entering the dog's name. Another example is the submit button that has
to validate values of all fields before saving the data.

<figure class="image">
<img
src="/images/patterns/diagrams/mediator/problem2.png?id=072c51eee4dd90c0972866440c87c1c3"
srcset="/images/patterns/diagrams/mediator/problem2-2x.png?id=d298ec82a47fa2938ed6cf64b7da78c1 2x"
loading="lazy" width="360"
alt="Elements of the UI are interdependent" />
<figcaption><p>Elements can have lots of relations with other elements.
Hence, changes to some elements may affect the others.</p></figcaption>
</figure>

By having this logic implemented directly inside the code of the form
elements you make these elements' classes much harder to reuse in other
forms of the app. For example, you won't be able to use that checkbox
class inside another form, because it's coupled to the dog's text field.
You can use either all the classes involved in rendering the profile
form, or none at all.



##  Solution

The Mediator pattern suggests that you should cease all direct
communication between the components which you want to make independent
of each other. Instead, these components must collaborate indirectly, by
calling a special mediator object that redirects the calls to
appropriate components. As a result, the components depend only on a
single mediator class instead of being coupled to dozens of their
colleagues.

In our example with the profile editing form, the dialog class itself
may act as the mediator. Most likely, the dialog class is already aware
of all of its sub-elements, so you won't even need to introduce new
dependencies into this class.

<figure class="image">
<img
src="/images/patterns/diagrams/mediator/solution1-en.png?id=dd991a5b7830de8d43f82b084e021713"
srcset="/images/patterns/diagrams/mediator/solution1-en-2x.png?id=0a1280789a5d7b1567c9d98e5fcd1125 2x"
loading="lazy" width="600"
alt="UI elements should communicate via the mediator." />
<figcaption><p>UI elements should communicate indirectly, via the
mediator object.</p></figcaption>
</figure>

The most significant change happens to the actual form elements. Let's
consider the submit button. Previously, each time a user clicked the
button, it had to validate the values of all individual form elements.
Now its single job is to notify the dialog about the click. Upon
receiving this notification, the dialog itself performs the validations
or passes the task to the individual elements. Thus, instead of being
tied to a dozen form elements, the button is only dependent on the
dialog class.

You can go further and make the dependency even looser by extracting the
common interface for all types of dialogs. The interface would declare
the notification method which all form elements can use to notify the
dialog about events happening to those elements. Thus, our submit button
should now be able to work with any dialog that implements that
interface.

This way, the Mediator pattern lets you encapsulate a complex web of
relations between various objects inside a single mediator object. The
fewer dependencies a class has, the easier it becomes to modify, extend
or reuse that class.



##  Real-World Analogy {#analogy}

<figure class="image">
<img
src="/images/patterns/diagrams/mediator/live-example.png?id=aa1de3cb7b63aa623e63578a1e43399a"
srcset="/images/patterns/diagrams/mediator/live-example-2x.png?id=fd55a9f9d8cf49effa223555c7369504 2x"
loading="lazy" width="370" alt="Air traffic control tower" />
<figcaption><p>Aircraft pilots don’t talk to each other directly when
deciding who gets to land their plane next. All communication goes
through the control tower.</p></figcaption>
</figure>

Pilots of aircraft that approach or depart the airport control area
don't communicate directly with each other. Instead, they speak to an
air traffic controller, who sits in a tall tower somewhere near the
airstrip. Without the air traffic controller, pilots would need to be
aware of every plane in the vicinity of the airport, discussing landing
priorities with a committee of dozens of other pilots. That would
probably skyrocket the airplane crash statistics.

The tower doesn't need to control the whole flight. It exists only to
enforce constraints in the terminal area because the number of involved
actors there might be overwhelming to a pilot.



##  Structure



<figure class="image">
<img
src="/images/patterns/diagrams/mediator/structure.png?id=1f2accc7820ecfe9665b6d30cbc0bc61"
class="structure-img-non-indexed d-none d-xl-block"
srcset="/images/patterns/diagrams/mediator/structure-2x.png?id=5191daa1c9d4caa36e38af3c5b7d1522 2x"
loading="lazy" width="520"
alt="Structure of the Mediator design pattern" /><img
src="/images/patterns/diagrams/mediator/structure-indexed.png?id=a82d4cf1b92a4f72af32f231ffd21131"
class="structure-img-indexed d-xl-none"
srcset="/images/patterns/diagrams/mediator/structure-indexed-2x.png?id=88722da01a5c82b0452078c9339ca497 2x"
loading="lazy" width="520"
alt="Structure of the Mediator design pattern" />
</figure>


1.  **Components** are various classes that contain some business logic.
    Each component has a reference to a mediator, declared with the type
    of the mediator interface. The component isn't aware of the actual
    class of the mediator, so you can reuse the component in other
    programs by linking it to a different mediator.

2.  The **Mediator** interface declares methods of communication with
    components, which usually include just a single notification method.
    Components may pass any context as arguments of this method,
    including their own objects, but only in such a way that no coupling
    occurs between a receiving component and the sender's class.

3.  **Concrete Mediators** encapsulate relations between various
    components. Concrete mediators often keep references to all
    components they manage and sometimes even manage their lifecycle.

4.  Components must not be aware of other components. If something
    important happens within or to a component, it must only notify the
    mediator. When the mediator receives the notification, it can easily
    identify the sender, which might be just enough to decide what
    component should be triggered in return.

    From a component's perspective, it all looks like a total black box.
    The sender doesn't know who'll end up handling its request, and the
    receiver doesn't know who sent the request in the first place.




##  Pseudocode

In this example, the **Mediator** pattern helps you eliminate mutual
dependencies between various UI classes: buttons, checkboxes and text
labels.

<figure class="image">
<img
src="/images/patterns/diagrams/mediator/example.png?id=3151c153533e816e226be0ef977211e8"
srcset="/images/patterns/diagrams/mediator/example-2x.png?id=02064e5a7c4f065f806747e1b04ac1b0 2x"
loading="lazy" width="560"
alt="Structure of the Mediator pattern example" />
<figcaption><p>Structure of the UI dialog classes.</p></figcaption>
</figure>

An element, triggered by a user, doesn't communicate with other elements
directly, even if it looks like it's supposed to. Instead, the element
only needs to let its mediator know about the event, passing any
contextual info along with that notification.

In this example, the whole authentication dialog acts as the mediator.
It knows how concrete elements are supposed to collaborate and
facilitates their indirect communication. Upon receiving a notification
about an event, the dialog decides what element should address the event
and redirects the call accordingly.

<figure class="code">
<pre class="code" lang="pseudocode"><code>// The mediator interface declares a method used by components
// to notify the mediator about various events. The mediator may
// react to these events and pass the execution to other
// components.
interface Mediator is
    method notify(sender: Component, event: string)


// The concrete mediator class. The intertwined web of
// connections between individual components has been untangled
// and moved into the mediator.
class AuthenticationDialog implements Mediator is
    private field title: string
    private field loginOrRegisterChkBx: Checkbox
    private field loginUsername, loginPassword: Textbox
    private field registrationUsername, registrationPassword,
                  registrationEmail: Textbox
    private field okBtn, cancelBtn: Button

    constructor AuthenticationDialog() is
        // Create all component objects by passing the current
        // mediator into their constructors to establish links.

    // When something happens with a component, it notifies the
    // mediator. Upon receiving a notification, the mediator may
    // do something on its own or pass the request to another
    // component.
    method notify(sender, event) is
        if (sender == loginOrRegisterChkBx and event == &quot;check&quot;)
            if (loginOrRegisterChkBx.checked)
                title = &quot;Log in&quot;
                // 1. Show login form components.
                // 2. Hide registration form components.
            else
                title = &quot;Register&quot;
                // 1. Show registration form components.
                // 2. Hide login form components

        if (sender == okBtn &amp;&amp; event == &quot;click&quot;)
            if (loginOrRegister.checked)
                // Try to find a user using login credentials.
                if (!found)
                    // Show an error message above the login
                    // field.
            else
                // 1. Create a user account using data from the
                // registration fields.
                // 2. Log that user in.
                // ...


// Components communicate with a mediator using the mediator
// interface. Thanks to that, you can use the same components in
// other contexts by linking them with different mediator
// objects.
class Component is
    field dialog: Mediator

    constructor Component(dialog) is
        this.dialog = dialog

    method click() is
        dialog.notify(this, &quot;click&quot;)

    method keypress() is
        dialog.notify(this, &quot;keypress&quot;)

// Concrete components don&#39;t talk to each other. They have only
// one communication channel, which is sending notifications to
// the mediator.
class Button extends Component is
    // ...

class Textbox extends Component is
    // ...

class Checkbox extends Component is
    method check() is
        dialog.notify(this, &quot;check&quot;)
    // ...</code></pre>
</figure>



##  Applicability



Use the Mediator pattern when it's hard to change some of the classes
because they are tightly coupled to a bunch of other classes.



The pattern lets you extract all the relationships between classes into
a separate class, isolating any changes to a specific component from the
rest of the components.



Use the pattern when you can't reuse a component in a different program
because it's too dependent on other components.



After you apply the Mediator, individual components become unaware of
the other components. They could still communicate with each other,
albeit indirectly, through a mediator object. To reuse a component in a
different app, you need to provide it with a new mediator class.



Use the Mediator when you find yourself creating tons of component
subclasses just to reuse some basic behavior in various contexts.



Since all relations between components are contained within the
mediator, it's easy to define entirely new ways for these components to
collaborate by introducing new mediator classes, without having to
change the components themselves.





##  How to Implement {#checklist}

1.  Identify a group of tightly coupled classes which would benefit from
    being more independent (e.g., for easier maintenance or simpler
    reuse of these classes).

2.  Declare the mediator interface and describe the desired
    communication protocol between mediators and various components. In
    most cases, a single method for receiving notifications from
    components is sufficient.

    This interface is crucial when you want to reuse component classes
    in different contexts. As long as the component works with its
    mediator via the generic interface, you can link the component with
    a different implementation of the mediator.

3.  Implement the concrete mediator class. Consider storing references
    to all components inside the mediator. This way, you could call any
    component from the mediator's methods.

4.  You can go even further and make the mediator responsible for the
    creation and destruction of component objects. After this, the
    mediator may resemble a [factory](/design-patterns/abstract-factory)
    or a [facade](/design-patterns/facade).

5.  Components should store a reference to the mediator object. The
    connection is usually established in the component's constructor,
    where a mediator object is passed as an argument.

6.  Change the components' code so that they call the mediator's
    notification method instead of methods on other components. Extract
    the code that involves calling other components into the mediator
    class. Execute this code whenever the mediator receives
    notifications from that component.



##  Pros and Cons {#pros-cons}



-    *Single Responsibility Principle*. You can extract the
    communications between various components into a single place,
    making it easier to comprehend and maintain.
-    *Open/Closed Principle*. You can introduce new mediators without
    having to change the actual components.
-    You can reduce coupling between various components of a program.
-    You can reuse individual components more easily.



-    Over time a mediator can evolve into a [God
    Object](/antipatterns/god-object).





##  Relations with Other Patterns {#relations}

-   [Chain of Responsibility](/design-patterns/chain-of-responsibility),
    [Command](/design-patterns/command),
    [Mediator](/design-patterns/mediator) and
    [Observer](/design-patterns/observer) address various ways of
    connecting senders and receivers of requests:

    -   *Chain of Responsibility* passes a request sequentially along a
        dynamic chain of potential receivers until one of them handles
        it.
    -   *Command* establishes unidirectional connections between senders
        and receivers.
    -   *Mediator* eliminates direct connections between senders and
        receivers, forcing them to communicate indirectly via a mediator
        object.
    -   *Observer* lets receivers dynamically subscribe to and
        unsubscribe from receiving requests.

-   [Facade](/design-patterns/facade) and
    [Mediator](/design-patterns/mediator) have similar jobs: they try to
    organize collaboration between lots of tightly coupled classes.

    -   *Facade* defines a simplified interface to a subsystem of
        objects, but it doesn't introduce any new functionality. The
        subsystem itself is unaware of the facade. Objects within the
        subsystem can communicate directly.
    -   *Mediator* centralizes communication between components of the
        system. The components only know about the mediator object and
        don't communicate directly.

-   The difference between [Mediator](/design-patterns/mediator) and
    [Observer](/design-patterns/observer) is often elusive. In most
    cases, you can implement either of these patterns; but sometimes you
    can apply both simultaneously. Let's see how we can do that.

    The primary goal of *Mediator* is to eliminate mutual dependencies
    among a set of system components. Instead, these components become
    dependent on a single mediator object. The goal of *Observer* is to
    establish dynamic one-way connections between objects, where some
    objects act as subordinates of others.

    There's a popular implementation of the *Mediator* pattern that
    relies on *Observer*. The mediator object plays the role of
    publisher, and the components act as subscribers which subscribe to
    and unsubscribe from the mediator's events. When *Mediator* is
    implemented this way, it may look very similar to *Observer*.

    When you're confused, remember that you can implement the Mediator
    pattern in other ways. For example, you can permanently link all the
    components to the same mediator object. This implementation won't
    resemble *Observer* but will still be an instance of the Mediator
    pattern.

    Now imagine a program where all components have become publishers,
    allowing dynamic connections between each other. There won't be a
    centralized mediator object, only a distributed set of observers.



##  Code Examples {#implementations}

[![Mediator in
C#](/images/patterns/icons/csharp.svg?id=da64592defc6e86d57c39c66e9de3e58){width="53"
height="53"
loading="lazy"}](/design-patterns/mediator/csharp/example "Mediator in C#"){.prog-lang-link}
[![Mediator in
C++](/images/patterns/icons/cpp.svg?id=f7782ed8b8666246bfcc3f8fefc3b858){width="53"
height="53"
loading="lazy"}](/design-patterns/mediator/cpp/example "Mediator in C++"){.prog-lang-link}
[![Mediator in
Go](/images/patterns/icons/go.svg?id=1a89927eb99b1ea3fde7701d97970aca){width="53"
height="53"
loading="lazy"}](/design-patterns/mediator/go/example "Mediator in Go"){.prog-lang-link}
[![Mediator in
Java](/images/patterns/icons/java.svg?id=e6d87e2dca08c953fe3acd1275ed4f4e){width="53"
height="53"
loading="lazy"}](/design-patterns/mediator/java/example "Mediator in Java"){.prog-lang-link}
[![Mediator in
PHP](/images/patterns/icons/php.svg?id=be1906eb26b71ec1d3b93720d6156618){width="53"
height="53"
loading="lazy"}](/design-patterns/mediator/php/example "Mediator in PHP"){.prog-lang-link}
[![Mediator in
Python](/images/patterns/icons/python.svg?id=6d815d43c0f7050a1151b43e51569c9f){width="53"
height="53"
loading="lazy"}](/design-patterns/mediator/python/example "Mediator in Python"){.prog-lang-link}
[![Mediator in
Ruby](/images/patterns/icons/ruby.svg?id=b065b718c914bf8e960ef731600be1eb){width="53"
height="53"
loading="lazy"}](/design-patterns/mediator/ruby/example "Mediator in Ruby"){.prog-lang-link}
[![Mediator in
Rust](/images/patterns/icons/rust.svg?id=1f5698a4b5ae23fe79413511747e4a87){width="53"
height="53"
loading="lazy"}](/design-patterns/mediator/rust/example "Mediator in Rust"){.prog-lang-link}
[![Mediator in
Swift](/images/patterns/icons/swift.svg?id=0b716c2d52ec3a48fbe91ac031070c1d){width="53"
height="53"
loading="lazy"}](/design-patterns/mediator/swift/example "Mediator in Swift"){.prog-lang-link}
[![Mediator in
TypeScript](/images/patterns/icons/typescript.svg?id=2239d0f16cb703540c205dd8cb0c0cb7){width="53"
height="53"
loading="lazy"}](/design-patterns/mediator/typescript/example "Mediator in TypeScript"){.prog-lang-link}





[![](/images/patterns/banners/patterns-book-banner-3.png?id=7d445df13c80287beaab234b4f3b698c){width="200"
height="200" loading="lazy"
srcset="/images/patterns/banners/patterns-book-banner-3-2x.png?id=0cc3f77ab421d1a5c02ee46488231c3a 2x"}](/design-patterns/book)



### Support our free website and own the eBook! {#support-our-free-website-and-own-the-ebook .title}

-   22 design patterns and 8 principles explained in depth.
-   409 well-structured, easy to read, jargon-free pages.
-   225 clear and helpful illustrations and diagrams.
-   An archive with code examples in 11 languages.
-   All devices supported: PDF/EPUB/MOBI/KFX formats.

[ Learn more...](/design-patterns/book){.btn .btn-secondary}





#### Read next

[Memento []{.fa .fa-arrow-right}](/design-patterns/memento){.btn
.btn-primary rel="next"}



#### Return

[[]{.fa .fa-arrow-left} Iterator](/design-patterns/iterator){.btn
.btn-default rel="prev"}







[![](/images/patterns/book/web-cover-en.png?id=328861769fd11617674e3b8a7e2dd9e7){width="250"
height="375" loading="lazy"
srcset="/images/patterns/book/web-cover-en-2x.png?id=02940141c5652ed5a426d87390b16366 2x"}](/design-patterns/book)




This article is a part of our eBook\
**Dive Into Design Patterns**.

[ Learn more...](/design-patterns/book){.btn .btn-secondary .btn-block}











[![Refactoring.Guru](/images/content-public/logos/logo-new.png?id=97d554614702483f31e38b32e82d8e34){width="200"
height="241" loading="lazy"
srcset="/images/content-public/logos/logo-new-2x.png?id=3bc33294e095bab1d6fe9ae421d07837 2x"}](/){.menu-brand}


-   [ Premium Content](/store)
    -   [ Design Patterns eBook](/design-patterns/book)
    -   [ Refactoring Course](/refactoring/course)
-   [ Refactoring](/refactoring)
    -   [What is Refactoring](/refactoring/what-is-refactoring)
        -   [Clean code](/refactoring/what-is-refactoring)
        -   [Technical debt](/refactoring/technical-debt)
        -   [When to refactor](/refactoring/when)
        -   [How to refactor](/refactoring/how-to)
    -   [Catalog](/refactoring/catalog)
    -   [Code Smells](/refactoring/smells)
        -   [Bloaters](/refactoring/smells/bloaters)
            -   [Long Method](/smells/long-method)
            -   [Large Class](/smells/large-class)
            -   [Primitive Obsession](/smells/primitive-obsession)
            -   [Long Parameter List](/smells/long-parameter-list)
            -   [Data Clumps](/smells/data-clumps)
        -   [Object-Orientation Abusers](/refactoring/smells/oo-abusers)
            -   [Switch Statements](/smells/switch-statements)
            -   [Temporary Field](/smells/temporary-field)
            -   [Refused Bequest](/smells/refused-bequest)
            -   [Alternative Classes with Different
                Interfaces](/smells/alternative-classes-with-different-interfaces)
        -   [Change Preventers](/refactoring/smells/change-preventers)
            -   [Divergent Change](/smells/divergent-change)
            -   [Shotgun Surgery](/smells/shotgun-surgery)
            -   [Parallel Inheritance
                Hierarchies](/smells/parallel-inheritance-hierarchies)
        -   [Dispensables](/refactoring/smells/dispensables)
            -   [Comments](/smells/comments)
            -   [Duplicate Code](/smells/duplicate-code)
            -   [Lazy Class](/smells/lazy-class)
            -   [Data Class](/smells/data-class)
            -   [Dead Code](/smells/dead-code)
            -   [Speculative Generality](/smells/speculative-generality)
        -   [Couplers](/refactoring/smells/couplers)
            -   [Feature Envy](/smells/feature-envy)
            -   [Inappropriate Intimacy](/smells/inappropriate-intimacy)
            -   [Message Chains](/smells/message-chains)
            -   [Middle Man](/smells/middle-man)
        -   [Other Smells](/refactoring/smells/other)
            -   [Incomplete Library
                Class](/smells/incomplete-library-class)
    -   [Refactorings](/refactoring/techniques)
        -   [Composing
            Methods](/refactoring/techniques/composing-methods)
            -   [Extract Method](/extract-method)
            -   [Inline Method](/inline-method)
            -   [Extract Variable](/extract-variable)
            -   [Inline Temp](/inline-temp)
            -   [Replace Temp with Query](/replace-temp-with-query)
            -   [Split Temporary Variable](/split-temporary-variable)
            -   [Remove Assignments to
                Parameters](/remove-assignments-to-parameters)
            -   [Replace Method with Method
                Object](/replace-method-with-method-object)
            -   [Substitute Algorithm](/substitute-algorithm)
        -   [Moving Features between
            Objects](/refactoring/techniques/moving-features-between-objects)
            -   [Move Method](/move-method)
            -   [Move Field](/move-field)
            -   [Extract Class](/extract-class)
            -   [Inline Class](/inline-class)
            -   [Hide Delegate](/hide-delegate)
            -   [Remove Middle Man](/remove-middle-man)
            -   [Introduce Foreign Method](/introduce-foreign-method)
            -   [Introduce Local Extension](/introduce-local-extension)
        -   [Organizing Data](/refactoring/techniques/organizing-data)
            -   [Self Encapsulate Field](/self-encapsulate-field)
            -   [Replace Data Value with
                Object](/replace-data-value-with-object)
            -   [Change Value to Reference](/change-value-to-reference)
            -   [Change Reference to Value](/change-reference-to-value)
            -   [Replace Array with Object](/replace-array-with-object)
            -   [Duplicate Observed Data](/duplicate-observed-data)
            -   [Change Unidirectional Association to
                Bidirectional](/change-unidirectional-association-to-bidirectional)
            -   [Change Bidirectional Association to
                Unidirectional](/change-bidirectional-association-to-unidirectional)
            -   [Replace Magic Number with Symbolic
                Constant](/replace-magic-number-with-symbolic-constant)
            -   [Encapsulate Field](/encapsulate-field)
            -   [Encapsulate Collection](/encapsulate-collection)
            -   [Replace Type Code with
                Class](/replace-type-code-with-class)
            -   [Replace Type Code with
                Subclasses](/replace-type-code-with-subclasses)
            -   [Replace Type Code with
                State/Strategy](/replace-type-code-with-state-strategy)
            -   [Replace Subclass with
                Fields](/replace-subclass-with-fields)
        -   [Simplifying Conditional
            Expressions](/refactoring/techniques/simplifying-conditional-expressions)
            -   [Decompose Conditional](/decompose-conditional)
            -   [Consolidate Conditional
                Expression](/consolidate-conditional-expression)
            -   [Consolidate Duplicate Conditional
                Fragments](/consolidate-duplicate-conditional-fragments)
            -   [Remove Control Flag](/remove-control-flag)
            -   [Replace Nested Conditional with Guard
                Clauses](/replace-nested-conditional-with-guard-clauses)
            -   [Replace Conditional with
                Polymorphism](/replace-conditional-with-polymorphism)
            -   [Introduce Null Object](/introduce-null-object)
            -   [Introduce Assertion](/introduce-assertion)
        -   [Simplifying Method
            Calls](/refactoring/techniques/simplifying-method-calls)
            -   [Rename Method](/rename-method)
            -   [Add Parameter](/add-parameter)
            -   [Remove Parameter](/remove-parameter)
            -   [Separate Query from
                Modifier](/separate-query-from-modifier)
            -   [Parameterize Method](/parameterize-method)
            -   [Replace Parameter with Explicit
                Methods](/replace-parameter-with-explicit-methods)
            -   [Preserve Whole Object](/preserve-whole-object)
            -   [Replace Parameter with Method
                Call](/replace-parameter-with-method-call)
            -   [Introduce Parameter
                Object](/introduce-parameter-object)
            -   [Remove Setting Method](/remove-setting-method)
            -   [Hide Method](/hide-method)
            -   [Replace Constructor with Factory
                Method](/replace-constructor-with-factory-method)
            -   [Replace Error Code with
                Exception](/replace-error-code-with-exception)
            -   [Replace Exception with
                Test](/replace-exception-with-test)
        -   [Dealing with
            Generalization](/refactoring/techniques/dealing-with-generalization)
            -   [Pull Up Field](/pull-up-field)
            -   [Pull Up Method](/pull-up-method)
            -   [Pull Up Constructor Body](/pull-up-constructor-body)
            -   [Push Down Method](/push-down-method)
            -   [Push Down Field](/push-down-field)
            -   [Extract Subclass](/extract-subclass)
            -   [Extract Superclass](/extract-superclass)
            -   [Extract Interface](/extract-interface)
            -   [Collapse Hierarchy](/collapse-hierarchy)
            -   [Form Template Method](/form-template-method)
            -   [Replace Inheritance with
                Delegation](/replace-inheritance-with-delegation)
            -   [Replace Delegation with
                Inheritance](/replace-delegation-with-inheritance)
-   [ Design Patterns](/design-patterns)
    -   [What is a Pattern](/design-patterns/what-is-pattern)
        -   [What\'s a design
            pattern?](/design-patterns/what-is-pattern)
        -   [History of patterns](/design-patterns/history)
        -   [Why should I learn
            patterns?](/design-patterns/why-learn-patterns)
        -   [Criticism of patterns](/design-patterns/criticism)
        -   [Classification of
            patterns](/design-patterns/classification)
    -   [Catalog](/design-patterns/catalog)
    -   [Creational Patterns](/design-patterns/creational-patterns)
        -   [Factory Method](/design-patterns/factory-method)
        -   [Abstract Factory](/design-patterns/abstract-factory)
        -   [Builder](/design-patterns/builder)
        -   [Prototype](/design-patterns/prototype)
        -   [Singleton](/design-patterns/singleton)
    -   [Structural Patterns](/design-patterns/structural-patterns)
        -   [Adapter](/design-patterns/adapter)
        -   [Bridge](/design-patterns/bridge)
        -   [Composite](/design-patterns/composite)
        -   [Decorator](/design-patterns/decorator)
        -   [Facade](/design-patterns/facade)
        -   [Flyweight](/design-patterns/flyweight)
        -   [Proxy](/design-patterns/proxy)
    -   [Behavioral Patterns](/design-patterns/behavioral-patterns)
        -   [Chain of
            Responsibility](/design-patterns/chain-of-responsibility)
        -   [Command](/design-patterns/command)
        -   [Iterator](/design-patterns/iterator)
        -   [Mediator](/design-patterns/mediator)
        -   [Memento](/design-patterns/memento)
        -   [Observer](/design-patterns/observer)
        -   [State](/design-patterns/state)
        -   [Strategy](/design-patterns/strategy)
        -   [Template Method](/design-patterns/template-method)
        -   [Visitor](/design-patterns/visitor)
    -   [Code Examples](/design-patterns/examples)
        -   [C#](/design-patterns/csharp)
        -   [C++](/design-patterns/cpp)
        -   [Go](/design-patterns/go)
        -   [Java](/design-patterns/java)
        -   [PHP](/design-patterns/php)
        -   [Python](/design-patterns/python)
        -   [Ruby](/design-patterns/ruby)
        -   [Rust](/design-patterns/rust)
        -   [Swift](/design-patterns/swift)
        -   [TypeScript](/design-patterns/typescript)



[ Log in](https://refactoring.guru/login "Log in") [ Contact
us](https://feedback.refactoring.guru/ "Contact us"){.userecho-public
rel="nofollow"}





[![Refactoring.Guru](/images/content-public/logos/logo-new-mobile.png?id=ea18aa9b032eaa92835ed6d472b03b4a){srcset="/images/content-public/logos/logo-new-mobile-2x.png?id=7ad5648bfd86ae2e8524147a72877c64 2x"}](/){.navigation-brand}


[![](data:image/svg+xml;base64,PHN2ZyBzdHlsZT0id2lkdGg6IDI4cHg7IGhlaWdodDogMjhweDsgZmlsbDogY3VycmVudENvbG9yOyBkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IG1hcmdpbi10b3A6IC0xNHB4OyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIiB2aWV3Ym94PSIwIDAgNTEyIDUxMiI+PCEtLSEgRm9udCBBd2Vzb21lIFBybyA2LjMuMCBieSBAZm9udGF3ZXNvbWUgLSBodHRwczovL2ZvbnRhd2Vzb21lLmNvbSBMaWNlbnNlIC0gaHR0cHM6Ly9mb250YXdlc29tZS5jb20vbGljZW5zZSAoQ29tbWVyY2lhbCBMaWNlbnNlKSBDb3B5cmlnaHQgMjAyMyBGb250aWNvbnMsIEluYy4gLS0+PHBhdGggZD0iTTM1NiA2MGw2MCAyMC02MCAyMC0yMCA2MC0yMC02MEwyNTYgODBsNjAtMjBMMzM2IDBsMjAgNjB6TTQ2NCAyMDhsNDggMTYtNDggMTYtMTYgNDgtMTYtNDgtNDgtMTYgNDgtMTYgMTYtNDggMTYgNDh6bS0yNDMuOC05LjhsMzMgNjYuOSA3My44IDEwLjcgNTkuOCA4LjctNDMuMyA0Mi4yLTUzLjQgNTIuMSAxMi42IDczLjVMMzEzIDUxMmwtNTMuNS0yOC4xLTY2LTM0LjctNjYgMzQuN0w3My45IDUxMmwxMC4yLTU5LjYgMTIuNi03My41TDQzLjMgMzI2LjggMCAyODQuNmw1OS44LTguNyA3My44LTEwLjcgMzMtNjYuOUwxOTMuNSAxNDRsMjYuOCA1NC4yem0yNi4xIDExNC40bC0yNS0zLjYtMTEuMi0yMi42LTE2LjctMzMuOS0xNi43IDMzLjlMMTY1LjYgMzA5bC0yNSAzLjYtMzcuNCA1LjQgMjcuMSAyNi40IDE4LjEgMTcuNkwxNDQgMzg3bC02LjQgMzcuMyAzMy41LTE3LjYgMjIuMy0xMS43IDIyLjMgMTEuNyAzMy41IDE3LjZMMjQyLjkgMzg3bC00LjMtMjQuOSAxOC4xLTE3LjYgMjcuMS0yNi40LTM3LjQtNS40eiI+PC9wYXRoPjwvc3ZnPg==)
Shop Now!](/store){.btn .btn-md .btn-primary .btn-featured}


-    [English]{.caption .d-none .d-lg-inline-block}

    
    [English](https://refactoring.guru/design-patterns/mediator "English"){.dropdown-item
    .locale-link .active locale="en"}
    [Español](https://refactoring.guru/es/design-patterns/mediator "Español"){.dropdown-item
    .locale-link locale="es"}
    [Français](https://refactoring.guru/fr/design-patterns/mediator "Français"){.dropdown-item
    .locale-link locale="fr"}
    [日本語](https://refactoring.guru/ja/design-patterns/mediator "日本語"){.dropdown-item
    .locale-link locale="ja"}
    [한국어](https://refactoring.guru/ko/design-patterns/mediator "한국어"){.dropdown-item
    .locale-link locale="ko"}
    [Polski](https://refactoring.guru/pl/design-patterns/mediator "Polski"){.dropdown-item
    .locale-link locale="pl"} [Português
    Brasileiro](https://refactoring.guru/pt-br/design-patterns/mediator "Português Brasileiro"){.dropdown-item
    .locale-link locale="pt-br"}
    [Русский](https://refactoring.guru/ru/design-patterns/mediator "Русский"){.dropdown-item
    .locale-link locale="ru"}
    [Українська](https://refactoring.guru/uk/design-patterns/mediator "Українська"){.dropdown-item
    .locale-link locale="uk"}
    [中文](https://refactoringguru.cn/design-patterns/mediator "中文"){.dropdown-item
    .locale-link locale="zh"}
    
-   [ [Contact us]{.caption .d-none
    .d-xl-inline-block}](https://feedback.refactoring.guru/?show_feedback_form_private=true "Contact us"){.userecho-private
    rel="nofollow"}
-   [ [Log in]{.caption .d-none
    .d-xl-inline-block}](https://refactoring.guru/login "Log in")
-   






-   [Home](/)
-   [Refactoring](/refactoring)
-   [Design Patterns](/design-patterns)
-   [Premium Content](/store)
-   [Forum](https://refactoring.userecho.com/){.userecho-public
    rel="nofollow"}
-   [Contact us](https://refactoring.userecho.com/){.userecho-private
    rel="nofollow"}



-   [](https://www.facebook.com/refactoring.guru)
-   [](/sendy/form){rel="nofollow"}
-   [](https://github.com/RefactoringGuru)










2014-2023 [Refactoring.Guru](/). [All rights
reserved.]{style="white-space: nowrap"}\
Illustrations by [[Dmitry
Zhart]{style="white-space: nowrap"}](http://zhart.us/){rel="nofollow"}



-   [Terms & Conditions](/terms)
-   [Privacy Policy](/privacy-policy)
-   [Content Usage Policy](/content-usage-policy)
-   [About us](/site-about)






