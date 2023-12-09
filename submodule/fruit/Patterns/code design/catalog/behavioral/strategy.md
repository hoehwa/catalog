



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


# Strategy {#strategy .title}


##  Intent

**Strategy** is a behavioral design pattern that lets you define a
family of algorithms, put each of them into a separate class, and make
their objects interchangeable.

<figure class="image">
<img
src="/images/patterns/content/strategy/strategy.png?id=379bfba335380500375881a3da6507e0"
srcset="/images/patterns/content/strategy/strategy-2x.png?id=1cee47d05a76fddf07dce9c67b700748 2x"
width="640" alt="Strategy design pattern" />
</figure>



##  Problem

One day you decided to create a navigation app for casual travelers. The
app was centered around a beautiful map which helped users quickly
orient themselves in any city.

One of the most requested features for the app was automatic route
planning. A user should be able to enter an address and see the fastest
route to that destination displayed on the map.

The first version of the app could only build the routes over roads.
People who traveled by car were bursting with joy. But apparently, not
everybody likes to drive on their vacation. So with the next update, you
added an option to build walking routes. Right after that, you added
another option to let people use public transport in their routes.

However, that was only the beginning. Later you planned to add route
building for cyclists. And even later, another option for building
routes through all of a city's tourist attractions.

<figure class="image">
<img
src="/images/patterns/diagrams/strategy/problem.png?id=e5ca943e559a979bd31d20e232dc22b6"
srcset="/images/patterns/diagrams/strategy/problem-2x.png?id=3974fb99c97aec525dd0ffcff2e48e78 2x"
loading="lazy" width="330"
alt="The code of the navigator became very bloated" />
<figcaption><p>The code of the navigator
became bloated.</p></figcaption>
</figure>

While from a business perspective the app was a success, the technical
part caused you many headaches. Each time you added a new routing
algorithm, the main class of the navigator doubled in size. At some
point, the beast became too hard to maintain.

Any change to one of the algorithms, whether it was a simple bug fix or
a slight adjustment of the street score, affected the whole class,
increasing the chance of creating an error in already-working code.

In addition, teamwork became inefficient. Your teammates, who had been
hired right after the successful release, complain that they spend too
much time resolving merge conflicts. Implementing a new feature requires
you to change the same huge class, conflicting with the code produced by
other people.



##  Solution

The Strategy pattern suggests that you take a class that does something
specific in a lot of different ways and extract all of these algorithms
into separate classes called *strategies*.

The original class, called *context*, must have a field for storing a
reference to one of the strategies. The context delegates the work to a
linked strategy object instead of executing it on its own.

The context isn't responsible for selecting an appropriate algorithm for
the job. Instead, the client passes the desired strategy to the context.
In fact, the context doesn't know much about strategies. It works with
all strategies through the same generic interface, which only exposes a
single method for triggering the algorithm encapsulated within the
selected strategy.

This way the context becomes independent of concrete strategies, so you
can add new algorithms or modify existing ones without changing the code
of the context or other strategies.

<figure class="image">
<img
src="/images/patterns/diagrams/strategy/solution.png?id=0813a174b29a2ed5902d321aba28e5fc"
srcset="/images/patterns/diagrams/strategy/solution-2x.png?id=66b5ee048ea2ad25c4b20f180ebf94d7 2x"
loading="lazy" width="570" alt="Route planning strategies" />
<figcaption><p>Route planning strategies.</p></figcaption>
</figure>

In our navigation app, each routing algorithm can be extracted to its
own class with a single `buildRoute` method. The method accepts an
origin and destination and returns a collection of the route's
checkpoints.

Even though given the same arguments, each routing class might build a
different route, the main navigator class doesn't really care which
algorithm is selected since its primary job is to render a set of
checkpoints on the map. The class has a method for switching the active
routing strategy, so its clients, such as the buttons in the user
interface, can replace the currently selected routing behavior with
another one.



##  Real-World Analogy {#analogy}

<figure class="image">
<img
src="/images/patterns/content/strategy/strategy-comic-1-en.png?id=f64d7d8e6f83a7792a769039a66007c1"
srcset="/images/patterns/content/strategy/strategy-comic-1-en-2x.png?id=7eb14bd7920ad630c1ecf448d40602df 2x"
loading="lazy" width="640" alt="Various transportation strategies" />
<figcaption><p>Various strategies for getting to
the airport.</p></figcaption>
</figure>

Imagine that you have to get to the airport. You can catch a bus, order
a cab, or get on your bicycle. These are your transportation strategies.
You can pick one of the strategies depending on factors such as budget
or time constraints.



##  Structure



<figure class="image">
<img
src="/images/patterns/diagrams/strategy/structure.png?id=c6aa910c94960f35d100bfca02810ea1"
class="structure-img-non-indexed d-none d-xl-block"
srcset="/images/patterns/diagrams/strategy/structure-2x.png?id=5bd791857c3bab419bcf4fa86877439d 2x"
loading="lazy" width="440"
alt="Structure of the Strategy design pattern" /><img
src="/images/patterns/diagrams/strategy/structure-indexed.png?id=ff55c5a6273cf82a5667f3cab5b605c7"
class="structure-img-indexed d-xl-none"
srcset="/images/patterns/diagrams/strategy/structure-indexed-2x.png?id=9f8e2f838f16705775411e2b4616820e 2x"
loading="lazy" width="450"
alt="Structure of the Strategy design pattern" />
</figure>


1.  The **Context** maintains a reference to one of the concrete
    strategies and communicates with this object only via the strategy
    interface.

2.  The **Strategy** interface is common to all concrete strategies. It
    declares a method the context uses to execute a strategy.

3.  **Concrete Strategies** implement different variations of an
    algorithm the context uses.

4.  The context calls the execution method on the linked strategy object
    each time it needs to run the algorithm. The context doesn't know
    what type of strategy it works with or how the algorithm is
    executed.

5.  The **Client** creates a specific strategy object and passes it to
    the context. The context exposes a setter which lets clients replace
    the strategy associated with the context at runtime.




##  Pseudocode

In this example, the context uses multiple **strategies** to execute
various arithmetic operations.

<figure class="code">
<pre class="code" lang="pseudocode"><code>// The strategy interface declares operations common to all
// supported versions of some algorithm. The context uses this
// interface to call the algorithm defined by the concrete
// strategies.
interface Strategy is
    method execute(a, b)

// Concrete strategies implement the algorithm while following
// the base strategy interface. The interface makes them
// interchangeable in the context.
class ConcreteStrategyAdd implements Strategy is
    method execute(a, b) is
        return a + b

class ConcreteStrategySubtract implements Strategy is
    method execute(a, b) is
        return a - b

class ConcreteStrategyMultiply implements Strategy is
    method execute(a, b) is
        return a * b

// The context defines the interface of interest to clients.
class Context is
    // The context maintains a reference to one of the strategy
    // objects. The context doesn&#39;t know the concrete class of a
    // strategy. It should work with all strategies via the
    // strategy interface.
    private strategy: Strategy

    // Usually the context accepts a strategy through the
    // constructor, and also provides a setter so that the
    // strategy can be switched at runtime.
    method setStrategy(Strategy strategy) is
        this.strategy = strategy

    // The context delegates some work to the strategy object
    // instead of implementing multiple versions of the
    // algorithm on its own.
    method executeStrategy(int a, int b) is
        return strategy.execute(a, b)


// The client code picks a concrete strategy and passes it to
// the context. The client should be aware of the differences
// between strategies in order to make the right choice.
class ExampleApplication is
    method main() is
        Create context object.

        Read first number.
        Read last number.
        Read the desired action from user input.

        if (action == addition) then
            context.setStrategy(new ConcreteStrategyAdd())

        if (action == subtraction) then
            context.setStrategy(new ConcreteStrategySubtract())

        if (action == multiplication) then
            context.setStrategy(new ConcreteStrategyMultiply())

        result = context.executeStrategy(First number, Second number)

        Print result.</code></pre>
</figure>



##  Applicability



Use the Strategy pattern when you want to use different variants of an
algorithm within an object and be able to switch from one algorithm to
another during runtime.



The Strategy pattern lets you indirectly alter the object's behavior at
runtime by associating it with different sub-objects which can perform
specific sub-tasks in different ways.



Use the Strategy when you have a lot of similar classes that only differ
in the way they execute some behavior.



The Strategy pattern lets you extract the varying behavior into a
separate class hierarchy and combine the original classes into one,
thereby reducing duplicate code.



Use the pattern to isolate the business logic of a class from the
implementation details of algorithms that may not be as important in the
context of that logic.



The Strategy pattern lets you isolate the code, internal data, and
dependencies of various algorithms from the rest of the code. Various
clients get a simple interface to execute the algorithms and switch them
at runtime.



Use the pattern when your class has a massive conditional statement that
switches between different variants of the same algorithm.



The Strategy pattern lets you do away with such a conditional by
extracting all algorithms into separate classes, all of which implement
the same interface. The original object delegates execution to one of
these objects, instead of implementing all variants of the algorithm.





##  How to Implement {#checklist}

1.  In the context class, identify an algorithm that's prone to frequent
    changes. It may also be a massive conditional that selects and
    executes a variant of the same algorithm at runtime.

2.  Declare the strategy interface common to all variants of the
    algorithm.

3.  One by one, extract all algorithms into their own classes. They
    should all implement the strategy interface.

4.  In the context class, add a field for storing a reference to a
    strategy object. Provide a setter for replacing values of that
    field. The context should work with the strategy object only via the
    strategy interface. The context may define an interface which lets
    the strategy access its data.

5.  Clients of the context must associate it with a suitable strategy
    that matches the way they expect the context to perform its primary
    job.



##  Pros and Cons {#pros-cons}



-    You can swap algorithms used inside an object at runtime.
-    You can isolate the implementation details of an algorithm from the
    code that uses it.
-    You can replace inheritance with composition.
-    *Open/Closed Principle*. You can introduce new strategies without
    having to change the context.



-    If you only have a couple of algorithms and they rarely change,
    there's no real reason to overcomplicate the program with new
    classes and interfaces that come along with the pattern.
-    Clients must be aware of the differences between strategies to be
    able to select a proper one.
-    A lot of modern programming languages have functional type support
    that lets you implement different versions of an algorithm inside a
    set of anonymous functions. Then you could use these functions
    exactly as you'd have used the strategy objects, but without
    bloating your code with extra classes and interfaces.





##  Relations with Other Patterns {#relations}

-   [Bridge](/design-patterns/bridge), [State](/design-patterns/state),
    [Strategy](/design-patterns/strategy) (and to some degree
    [Adapter](/design-patterns/adapter)) have very similar structures.
    Indeed, all of these patterns are based on composition, which is
    delegating work to other objects. However, they all solve different
    problems. A pattern isn't just a recipe for structuring your code in
    a specific way. It can also communicate to other developers the
    problem the pattern solves.

-   [Command](/design-patterns/command) and
    [Strategy](/design-patterns/strategy) may look similar because you
    can use both to parameterize an object with some action. However,
    they have very different intents.

    -   You can use *Command* to convert any operation into an object.
        The operation's parameters become fields of that object. The
        conversion lets you defer execution of the operation, queue it,
        store the history of commands, send commands to remote
        services, etc.

    -   On the other hand, *Strategy* usually describes different ways
        of doing the same thing, letting you swap these algorithms
        within a single context class.

-   [Decorator](/design-patterns/decorator) lets you change the skin of
    an object, while [Strategy](/design-patterns/strategy) lets you
    change the guts.

-   [Template Method](/design-patterns/template-method) is based on
    inheritance: it lets you alter parts of an algorithm by extending
    those parts in subclasses. [Strategy](/design-patterns/strategy) is
    based on composition: you can alter parts of the object's behavior
    by supplying it with different strategies that correspond to that
    behavior. *Template Method* works at the class level, so it's
    static. *Strategy* works on the object level, letting you switch
    behaviors at runtime.

-   [State](/design-patterns/state) can be considered as an extension of
    [Strategy](/design-patterns/strategy). Both patterns are based on
    composition: they change the behavior of the context by delegating
    some work to helper objects. *Strategy* makes these objects
    completely independent and unaware of each other. However, *State*
    doesn't restrict dependencies between concrete states, letting them
    alter the state of the context at will.



##  Code Examples {#implementations}

[![Strategy in
C#](/images/patterns/icons/csharp.svg?id=da64592defc6e86d57c39c66e9de3e58){width="53"
height="53"
loading="lazy"}](/design-patterns/strategy/csharp/example "Strategy in C#"){.prog-lang-link}
[![Strategy in
C++](/images/patterns/icons/cpp.svg?id=f7782ed8b8666246bfcc3f8fefc3b858){width="53"
height="53"
loading="lazy"}](/design-patterns/strategy/cpp/example "Strategy in C++"){.prog-lang-link}
[![Strategy in
Go](/images/patterns/icons/go.svg?id=1a89927eb99b1ea3fde7701d97970aca){width="53"
height="53"
loading="lazy"}](/design-patterns/strategy/go/example "Strategy in Go"){.prog-lang-link}
[![Strategy in
Java](/images/patterns/icons/java.svg?id=e6d87e2dca08c953fe3acd1275ed4f4e){width="53"
height="53"
loading="lazy"}](/design-patterns/strategy/java/example "Strategy in Java"){.prog-lang-link}
[![Strategy in
PHP](/images/patterns/icons/php.svg?id=be1906eb26b71ec1d3b93720d6156618){width="53"
height="53"
loading="lazy"}](/design-patterns/strategy/php/example "Strategy in PHP"){.prog-lang-link}
[![Strategy in
Python](/images/patterns/icons/python.svg?id=6d815d43c0f7050a1151b43e51569c9f){width="53"
height="53"
loading="lazy"}](/design-patterns/strategy/python/example "Strategy in Python"){.prog-lang-link}
[![Strategy in
Ruby](/images/patterns/icons/ruby.svg?id=b065b718c914bf8e960ef731600be1eb){width="53"
height="53"
loading="lazy"}](/design-patterns/strategy/ruby/example "Strategy in Ruby"){.prog-lang-link}
[![Strategy in
Rust](/images/patterns/icons/rust.svg?id=1f5698a4b5ae23fe79413511747e4a87){width="53"
height="53"
loading="lazy"}](/design-patterns/strategy/rust/example "Strategy in Rust"){.prog-lang-link}
[![Strategy in
Swift](/images/patterns/icons/swift.svg?id=0b716c2d52ec3a48fbe91ac031070c1d){width="53"
height="53"
loading="lazy"}](/design-patterns/strategy/swift/example "Strategy in Swift"){.prog-lang-link}
[![Strategy in
TypeScript](/images/patterns/icons/typescript.svg?id=2239d0f16cb703540c205dd8cb0c0cb7){width="53"
height="53"
loading="lazy"}](/design-patterns/strategy/typescript/example "Strategy in TypeScript"){.prog-lang-link}





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

[Template Method []{.fa
.fa-arrow-right}](/design-patterns/template-method){.btn .btn-primary
rel="next"}



#### Return

[[]{.fa .fa-arrow-left} State](/design-patterns/state){.btn .btn-default
rel="prev"}







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

    
    [English](https://refactoring.guru/design-patterns/strategy "English"){.dropdown-item
    .locale-link .active locale="en"}
    [Español](https://refactoring.guru/es/design-patterns/strategy "Español"){.dropdown-item
    .locale-link locale="es"}
    [Français](https://refactoring.guru/fr/design-patterns/strategy "Français"){.dropdown-item
    .locale-link locale="fr"}
    [日本語](https://refactoring.guru/ja/design-patterns/strategy "日本語"){.dropdown-item
    .locale-link locale="ja"}
    [한국어](https://refactoring.guru/ko/design-patterns/strategy "한국어"){.dropdown-item
    .locale-link locale="ko"}
    [Polski](https://refactoring.guru/pl/design-patterns/strategy "Polski"){.dropdown-item
    .locale-link locale="pl"} [Português
    Brasileiro](https://refactoring.guru/pt-br/design-patterns/strategy "Português Brasileiro"){.dropdown-item
    .locale-link locale="pt-br"}
    [Русский](https://refactoring.guru/ru/design-patterns/strategy "Русский"){.dropdown-item
    .locale-link locale="ru"}
    [Українська](https://refactoring.guru/uk/design-patterns/strategy "Українська"){.dropdown-item
    .locale-link locale="uk"}
    [中文](https://refactoringguru.cn/design-patterns/strategy "中文"){.dropdown-item
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






