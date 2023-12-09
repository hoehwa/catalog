



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


# State {#state .title}


##  Intent

**State** is a behavioral design pattern that lets an object alter its
behavior when its internal state changes. It appears as if the object
changed its class.

<figure class="image">
<img
src="/images/patterns/content/state/state-en.png?id=c323fb8c54e2d57bebf4806c087afb07"
srcset="/images/patterns/content/state/state-en-2x.png?id=dfd427a938223ae880291c2850f3e34a 2x"
width="640" alt="State Design Pattern" />
</figure>



##  Problem

The State pattern is closely related to the concept of a *Finite-State
Machine* []{.pop-i}[Finite-State Machine:
<https://refactoring.guru/fsm>]{.pop-content}.

<figure class="image">
<img
src="/images/patterns/diagrams/state/problem1.png?id=503968745461a0970d1fbb4362dc186f"
srcset="/images/patterns/diagrams/state/problem1-2x.png?id=ae03c2233939eace11d44925ddeb912d 2x"
loading="lazy" width="320" alt="Finite-State Machine" />
<figcaption><p>Finite-State Machine.</p></figcaption>
</figure>

The main idea is that, at any given moment, there's a *finite* number of
*states* which a program can be in. Within any unique state, the program
behaves differently, and the program can be switched from one state to
another instantaneously. However, depending on a current state, the
program may or may not switch to certain other states. These switching
rules, called *transitions*, are also finite and predetermined.

You can also apply this approach to objects. Imagine that we have a
`Document` class. A document can be in one of three states: `Draft`,
`Moderation` and `Published`. The `publish` method of the document works
a little bit differently in each state:

-   In `Draft`, it moves the document to moderation.
-   In `Moderation`, it makes the document public, but only if the
    current user is an administrator.
-   In `Published`, it doesn't do anything at all.

<figure class="image">
<img
src="/images/patterns/diagrams/state/problem2-en.png?id=8a3cb79b309a9d83276278244cdcb610"
srcset="/images/patterns/diagrams/state/problem2-en-2x.png?id=916d1d80335d02b94bec972db93fd94b 2x"
loading="lazy" width="560" alt="Possible states of a document object" />
<figcaption><p>Possible states and transitions of a
document object.</p></figcaption>
</figure>

State machines are usually implemented with lots of conditional
statements (`if` or `switch`) that select the appropriate behavior
depending on the current state of the object. Usually, this "state" is
just a set of values of the object's fields. Even if you've never heard
about finite-state machines before, you've probably implemented a state
at least once. Does the following code structure ring a bell?

<figure class="code">
<pre class="code" lang="pseudocode"><code>class Document is
    field state: string
    // ...
    method publish() is
        switch (state)
            &quot;draft&quot;:
                state = &quot;moderation&quot;
                break
            &quot;moderation&quot;:
                if (currentUser.role == &quot;admin&quot;)
                    state = &quot;published&quot;
                break
            &quot;published&quot;:
                // Do nothing.
                break
    // ...</code></pre>
</figure>

The biggest weakness of a state machine based on conditionals reveals
itself once we start adding more and more states and state-dependent
behaviors to the `Document` class. Most methods will contain monstrous
conditionals that pick the proper behavior of a method according to the
current state. Code like this is very difficult to maintain because any
change to the transition logic may require changing state conditionals
in every method.

The problem tends to get bigger as a project evolves. It's quite
difficult to predict all possible states and transitions at the design
stage. Hence, a lean state machine built with a limited set of
conditionals can grow into a bloated mess over time.



##  Solution

The State pattern suggests that you create new classes for all possible
states of an object and extract all state-specific behaviors into these
classes.

Instead of implementing all behaviors on its own, the original object,
called *context*, stores a reference to one of the state objects that
represents its current state, and delegates all the state-related work
to that object.

<figure class="image">
<img
src="/images/patterns/diagrams/state/solution-en.png?id=2db312e603c026421063dddef065b170"
srcset="/images/patterns/diagrams/state/solution-en-2x.png?id=73ae9e51f65b2ee61d4abe481dcfc430 2x"
loading="lazy" width="490"
alt="Document delegates the work to a state object" />
<figcaption><p>Document delegates the work to a
state object.</p></figcaption>
</figure>

To transition the context into another state, replace the active state
object with another object that represents that new state. This is
possible only if all state classes follow the same interface and the
context itself works with these objects through that interface.

This structure may look similar to the
[Strategy](/design-patterns/strategy) pattern, but there's one key
difference. In the State pattern, the particular states may be aware of
each other and initiate transitions from one state to another, whereas
strategies almost never know about each other.



##  Real-World Analogy {#analogy}

The buttons and switches in your smartphone behave differently depending
on the current state of the device:

-   When the phone is unlocked, pressing buttons leads to executing
    various functions.
-   When the phone is locked, pressing any button leads to the unlock
    screen.
-   When the phone's charge is low, pressing any button shows the
    charging screen.



##  Structure



<figure class="image">
<img
src="/images/patterns/diagrams/state/structure-en.png?id=38c5cc3a610a201e5bc26a441c63d327"
class="structure-img-non-indexed d-none d-xl-block"
srcset="/images/patterns/diagrams/state/structure-en-2x.png?id=69d9c6da31574e2aeafcf39abdd6b74d 2x"
loading="lazy" width="540"
alt="Structure of the State design pattern" /><img
src="/images/patterns/diagrams/state/structure-en-indexed.png?id=303874f78151b9aebdc585080e98d773"
class="structure-img-indexed d-xl-none"
srcset="/images/patterns/diagrams/state/structure-en-indexed-2x.png?id=d9b987cad93ddb1dfa48e1abe85b0971 2x"
loading="lazy" width="540"
alt="Structure of the State design pattern" />
</figure>


1.  **Context** stores a reference to one of the concrete state objects
    and delegates to it all state-specific work. The context
    communicates with the state object via the state interface. The
    context exposes a setter for passing it a new state object.

2.  The **State** interface declares the state-specific methods. These
    methods should make sense for all concrete states because you don't
    want some of your states to have useless methods that will never be
    called.

3.  **Concrete States** provide their own implementations for the
    state-specific methods. To avoid duplication of similar code across
    multiple states, you may provide intermediate abstract classes that
    encapsulate some common behavior.

    State objects may store a backreference to the context object.
    Through this reference, the state can fetch any required info from
    the context object, as well as initiate state transitions.

4.  Both context and concrete states can set the next state of the
    context and perform the actual state transition by replacing the
    state object linked to the context.




##  Pseudocode

In this example, the **State** pattern lets the same controls of the
media player behave differently, depending on the current playback
state.

<figure class="image">
<img
src="/images/patterns/diagrams/state/example.png?id=1ffdb109b3ebb85d223b9d1651d2034c"
srcset="/images/patterns/diagrams/state/example-2x.png?id=cd81e3ffb8aba5883983a59c111b805f 2x"
loading="lazy" width="590"
alt="Structure of the State pattern example" />
<figcaption><p>Example of changing object behavior with
state objects.</p></figcaption>
</figure>

The main object of the player is always linked to a state object that
performs most of the work for the player. Some actions replace the
current state object of the player with another, which changes the way
the player reacts to user interactions.

<figure class="code">
<pre class="code" lang="pseudocode"><code>// The AudioPlayer class acts as a context. It also maintains a
// reference to an instance of one of the state classes that
// represents the current state of the audio player.
class AudioPlayer is
    field state: State
    field UI, volume, playlist, currentSong

    constructor AudioPlayer() is
        this.state = new ReadyState(this)

        // Context delegates handling user input to a state
        // object. Naturally, the outcome depends on what state
        // is currently active, since each state can handle the
        // input differently.
        UI = new UserInterface()
        UI.lockButton.onClick(this.clickLock)
        UI.playButton.onClick(this.clickPlay)
        UI.nextButton.onClick(this.clickNext)
        UI.prevButton.onClick(this.clickPrevious)

    // Other objects must be able to switch the audio player&#39;s
    // active state.
    method changeState(state: State) is
        this.state = state

    // UI methods delegate execution to the active state.
    method clickLock() is
        state.clickLock()
    method clickPlay() is
        state.clickPlay()
    method clickNext() is
        state.clickNext()
    method clickPrevious() is
        state.clickPrevious()

    // A state may call some service methods on the context.
    method startPlayback() is
        // ...
    method stopPlayback() is
        // ...
    method nextSong() is
        // ...
    method previousSong() is
        // ...
    method fastForward(time) is
        // ...
    method rewind(time) is
        // ...


// The base state class declares methods that all concrete
// states should implement and also provides a backreference to
// the context object associated with the state. States can use
// the backreference to transition the context to another state.
abstract class State is
    protected field player: AudioPlayer

    // Context passes itself through the state constructor. This
    // may help a state fetch some useful context data if it&#39;s
    // needed.
    constructor State(player) is
        this.player = player

    abstract method clickLock()
    abstract method clickPlay()
    abstract method clickNext()
    abstract method clickPrevious()


// Concrete states implement various behaviors associated with a
// state of the context.
class LockedState extends State is

    // When you unlock a locked player, it may assume one of two
    // states.
    method clickLock() is
        if (player.playing)
            player.changeState(new PlayingState(player))
        else
            player.changeState(new ReadyState(player))

    method clickPlay() is
        // Locked, so do nothing.

    method clickNext() is
        // Locked, so do nothing.

    method clickPrevious() is
        // Locked, so do nothing.


// They can also trigger state transitions in the context.
class ReadyState extends State is
    method clickLock() is
        player.changeState(new LockedState(player))

    method clickPlay() is
        player.startPlayback()
        player.changeState(new PlayingState(player))

    method clickNext() is
        player.nextSong()

    method clickPrevious() is
        player.previousSong()


class PlayingState extends State is
    method clickLock() is
        player.changeState(new LockedState(player))

    method clickPlay() is
        player.stopPlayback()
        player.changeState(new ReadyState(player))

    method clickNext() is
        if (event.doubleclick)
            player.nextSong()
        else
            player.fastForward(5)

    method clickPrevious() is
        if (event.doubleclick)
            player.previous()
        else
            player.rewind(5)</code></pre>
</figure>



##  Applicability



Use the State pattern when you have an object that behaves differently
depending on its current state, the number of states is enormous, and
the state-specific code changes frequently.



The pattern suggests that you extract all state-specific code into a set
of distinct classes. As a result, you can add new states or change
existing ones independently of each other, reducing the maintenance
cost.



Use the pattern when you have a class polluted with massive conditionals
that alter how the class behaves according to the current values of the
class's fields.



The State pattern lets you extract branches of these conditionals into
methods of corresponding state classes. While doing so, you can also
clean temporary fields and helper methods involved in state-specific
code out of your main class.



Use State when you have a lot of duplicate code across similar states
and transitions of a condition-based state machine.



The State pattern lets you compose hierarchies of state classes and
reduce duplication by extracting common code into abstract base classes.





##  How to Implement {#checklist}

1.  Decide what class will act as the context. It could be an existing
    class which already has the state-dependent code; or a new class, if
    the state-specific code is distributed across multiple classes.

2.  Declare the state interface. Although it may mirror all the methods
    declared in the context, aim only for those that may contain
    state-specific behavior.

3.  For every actual state, create a class that derives from the state
    interface. Then go over the methods of the context and extract all
    code related to that state into your newly created class.

    While moving the code to the state class, you might discover that it
    depends on private members of the context. There are several
    workarounds:

    -   Make these fields or methods public.
    -   Turn the behavior you're extracting into a public method in the
        context and call it from the state class. This way is ugly but
        quick, and you can always fix it later.
    -   Nest the state classes into the context class, but only if your
        programming language supports nesting classes.

4.  In the context class, add a reference field of the state interface
    type and a public setter that allows overriding the value of that
    field.

5.  Go over the method of the context again and replace empty state
    conditionals with calls to corresponding methods of the state
    object.

6.  To switch the state of the context, create an instance of one of the
    state classes and pass it to the context. You can do this within the
    context itself, or in various states, or in the client. Wherever
    this is done, the class becomes dependent on the concrete state
    class that it instantiates.



##  Pros and Cons {#pros-cons}



-    *Single Responsibility Principle*. Organize the code related to
    particular states into separate classes.
-    *Open/Closed Principle*. Introduce new states without changing
    existing state classes or the context.
-    Simplify the code of the context by eliminating bulky state machine
    conditionals.



-    Applying the pattern can be overkill if a state machine has only a
    few states or rarely changes.





##  Relations with Other Patterns {#relations}

-   [Bridge](/design-patterns/bridge), [State](/design-patterns/state),
    [Strategy](/design-patterns/strategy) (and to some degree
    [Adapter](/design-patterns/adapter)) have very similar structures.
    Indeed, all of these patterns are based on composition, which is
    delegating work to other objects. However, they all solve different
    problems. A pattern isn't just a recipe for structuring your code in
    a specific way. It can also communicate to other developers the
    problem the pattern solves.

-   [State](/design-patterns/state) can be considered as an extension of
    [Strategy](/design-patterns/strategy). Both patterns are based on
    composition: they change the behavior of the context by delegating
    some work to helper objects. *Strategy* makes these objects
    completely independent and unaware of each other. However, *State*
    doesn't restrict dependencies between concrete states, letting them
    alter the state of the context at will.



##  Code Examples {#implementations}

[![State in
C#](/images/patterns/icons/csharp.svg?id=da64592defc6e86d57c39c66e9de3e58){width="53"
height="53"
loading="lazy"}](/design-patterns/state/csharp/example "State in C#"){.prog-lang-link}
[![State in
C++](/images/patterns/icons/cpp.svg?id=f7782ed8b8666246bfcc3f8fefc3b858){width="53"
height="53"
loading="lazy"}](/design-patterns/state/cpp/example "State in C++"){.prog-lang-link}
[![State in
Go](/images/patterns/icons/go.svg?id=1a89927eb99b1ea3fde7701d97970aca){width="53"
height="53"
loading="lazy"}](/design-patterns/state/go/example "State in Go"){.prog-lang-link}
[![State in
Java](/images/patterns/icons/java.svg?id=e6d87e2dca08c953fe3acd1275ed4f4e){width="53"
height="53"
loading="lazy"}](/design-patterns/state/java/example "State in Java"){.prog-lang-link}
[![State in
PHP](/images/patterns/icons/php.svg?id=be1906eb26b71ec1d3b93720d6156618){width="53"
height="53"
loading="lazy"}](/design-patterns/state/php/example "State in PHP"){.prog-lang-link}
[![State in
Python](/images/patterns/icons/python.svg?id=6d815d43c0f7050a1151b43e51569c9f){width="53"
height="53"
loading="lazy"}](/design-patterns/state/python/example "State in Python"){.prog-lang-link}
[![State in
Ruby](/images/patterns/icons/ruby.svg?id=b065b718c914bf8e960ef731600be1eb){width="53"
height="53"
loading="lazy"}](/design-patterns/state/ruby/example "State in Ruby"){.prog-lang-link}
[![State in
Rust](/images/patterns/icons/rust.svg?id=1f5698a4b5ae23fe79413511747e4a87){width="53"
height="53"
loading="lazy"}](/design-patterns/state/rust/example "State in Rust"){.prog-lang-link}
[![State in
Swift](/images/patterns/icons/swift.svg?id=0b716c2d52ec3a48fbe91ac031070c1d){width="53"
height="53"
loading="lazy"}](/design-patterns/state/swift/example "State in Swift"){.prog-lang-link}
[![State in
TypeScript](/images/patterns/icons/typescript.svg?id=2239d0f16cb703540c205dd8cb0c0cb7){width="53"
height="53"
loading="lazy"}](/design-patterns/state/typescript/example "State in TypeScript"){.prog-lang-link}





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

[Strategy []{.fa .fa-arrow-right}](/design-patterns/strategy){.btn
.btn-primary rel="next"}



#### Return

[[]{.fa .fa-arrow-left} Observer](/design-patterns/observer){.btn
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

    
    [English](https://refactoring.guru/design-patterns/state "English"){.dropdown-item
    .locale-link .active locale="en"}
    [Español](https://refactoring.guru/es/design-patterns/state "Español"){.dropdown-item
    .locale-link locale="es"}
    [Français](https://refactoring.guru/fr/design-patterns/state "Français"){.dropdown-item
    .locale-link locale="fr"}
    [日本語](https://refactoring.guru/ja/design-patterns/state "日本語"){.dropdown-item
    .locale-link locale="ja"}
    [한국어](https://refactoring.guru/ko/design-patterns/state "한국어"){.dropdown-item
    .locale-link locale="ko"}
    [Polski](https://refactoring.guru/pl/design-patterns/state "Polski"){.dropdown-item
    .locale-link locale="pl"} [Português
    Brasileiro](https://refactoring.guru/pt-br/design-patterns/state "Português Brasileiro"){.dropdown-item
    .locale-link locale="pt-br"}
    [Русский](https://refactoring.guru/ru/design-patterns/state "Русский"){.dropdown-item
    .locale-link locale="ru"}
    [Українська](https://refactoring.guru/uk/design-patterns/state "Українська"){.dropdown-item
    .locale-link locale="uk"}
    [中文](https://refactoringguru.cn/design-patterns/state "中文"){.dropdown-item
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






