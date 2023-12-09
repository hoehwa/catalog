



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


# Template Method {#template-method .title}


##  Intent

**Template Method** is a behavioral design pattern that defines the
skeleton of an algorithm in the superclass but lets subclasses override
specific steps of the algorithm without changing its structure.

<figure class="image">
<img
src="/images/patterns/content/template-method/template-method.png?id=eee9461742f832814f19612ccf472819"
srcset="/images/patterns/content/template-method/template-method-2x.png?id=4e164dc41be4dcfa122628864c2be210 2x"
width="640" alt="Template method design pattern" />
</figure>



##  Problem

Imagine that you're creating a data mining application that analyzes
corporate documents. Users feed the app documents in various formats
(PDF, DOC, CSV), and it tries to extract meaningful data from these docs
in a uniform format.

The first version of the app could work only with DOC files. In the
following version, it was able to support CSV files. A month later, you
"taught" it to extract data from PDF files.

<figure class="image">
<img
src="/images/patterns/diagrams/template-method/problem.png?id=60fa4f735c467ac1c9438231a1782807"
srcset="/images/patterns/diagrams/template-method/problem-2x.png?id=fc8b434afec7b6135043d0d2f48189f0 2x"
loading="lazy" width="620"
alt="Data mining classes contained a lot of duplicate code" />
<figcaption><p>Data mining classes contained a lot of
duplicate code.</p></figcaption>
</figure>

At some point, you noticed that all three classes have a lot of similar
code. While the code for dealing with various data formats was entirely
different in all classes, the code for data processing and analysis is
almost identical. Wouldn't it be great to get rid of the code
duplication, leaving the algorithm structure intact?

There was another problem related to client code that used these
classes. It had lots of conditionals that picked a proper course of
action depending on the class of the processing object. If all three
processing classes had a common interface or a base class, you'd be able
to eliminate the conditionals in client code and use polymorphism when
calling methods on a processing object.



##  Solution

The Template Method pattern suggests that you break down an algorithm
into a series of steps, turn these steps into methods, and put a series
of calls to these methods inside a single *template method.* The steps
may either be `abstract`, or have some default implementation. To use
the algorithm, the client is supposed to provide its own subclass,
implement all abstract steps, and override some of the optional ones if
needed (but not the template method itself).

Let's see how this will play out in our data mining app. We can create a
base class for all three parsing algorithms. This class defines a
template method consisting of a series of calls to various
document-processing steps.

<figure class="image">
<img
src="/images/patterns/diagrams/template-method/solution-en.png?id=98cb323d5736539b684da62a0fd49730"
srcset="/images/patterns/diagrams/template-method/solution-en-2x.png?id=4980d5dfb1fe07f065650e09756f5614 2x"
loading="lazy" width="600"
alt="Template method defines the skeleton of the algorithm" />
<figcaption><p>Template method breaks the algorithm into steps, allowing
subclasses to override these steps but not the
actual method.</p></figcaption>
</figure>

At first, we can declare all steps `abstract`, forcing the subclasses to
provide their own implementations for these methods. In our case,
subclasses already have all necessary implementations, so the only thing
we might need to do is adjust signatures of the methods to match the
methods of the superclass.

Now, let's see what we can do to get rid of the duplicate code. It looks
like the code for opening/closing files and extracting/parsing data is
different for various data formats, so there's no point in touching
those methods. However, implementation of other steps, such as analyzing
the raw data and composing reports, is very similar, so it can be pulled
up into the base class, where subclasses can share that code.

As you can see, we've got two types of steps:

-   *abstract steps* must be implemented by every subclass
-   *optional steps* already have some default implementation, but still
    can be overridden if needed

There's another type of step, called *hooks*. A hook is an optional step
with an empty body. A template method would work even if a hook isn't
overridden. Usually, hooks are placed before and after crucial steps of
algorithms, providing subclasses with additional extension points for an
algorithm.



##  Real-World Analogy {#analogy}

<figure class="image">
<img
src="/images/patterns/diagrams/template-method/live-example.png?id=2485d52852f87da06c9cc0e2fd257d6a"
srcset="/images/patterns/diagrams/template-method/live-example-2x.png?id=89083a3dcd1fe2b627b9b6e6ff4986dc 2x"
loading="lazy" width="590" alt="Mass housing construction" />
<figcaption><p>A typical architectural plan can be slightly altered to
better fit the client’s needs.</p></figcaption>
</figure>

The template method approach can be used in mass housing construction.
The architectural plan for building a standard house may contain several
extension points that would let a potential owner adjust some details of
the resulting house.

Each building step, such as laying the foundation, framing, building
walls, installing plumbing and wiring for water and electricity, etc.,
can be slightly changed to make the resulting house a little bit
different from others.



##  Structure



<figure class="image">
<img
src="/images/patterns/diagrams/template-method/structure.png?id=924692f994bff6578d8408d90f6fc459"
class="structure-img-non-indexed d-none d-xl-block"
srcset="/images/patterns/diagrams/template-method/structure-2x.png?id=25082d6d6a76f51c6b64d8aeeaffdbb5 2x"
loading="lazy" width="340"
alt="Structure of the Template Method design pattern" /><img
src="/images/patterns/diagrams/template-method/structure-indexed.png?id=4ced6107519bc66710d2f05c0f4097a1"
class="structure-img-indexed d-xl-none"
srcset="/images/patterns/diagrams/template-method/structure-indexed-2x.png?id=86f28789cdcc5a4c415d6a1100de56fc 2x"
loading="lazy" width="350"
alt="Structure of the Template Method design pattern" />
</figure>


1.  The **Abstract Class** declares methods that act as steps of an
    algorithm, as well as the actual template method which calls these
    methods in a specific order. The steps may either be declared
    `abstract` or have some default implementation.

2.  **Concrete Classes** can override all of the steps, but not the
    template method itself.




##  Pseudocode

In this example, the **Template Method** pattern provides a "skeleton"
for various branches of artificial intelligence in a simple strategy
video game.

<figure class="image">
<img
src="/images/patterns/diagrams/template-method/example.png?id=c0ce5cc8070925a1cd345fac6afa16b6"
srcset="/images/patterns/diagrams/template-method/example-2x.png?id=d8b309659c4b722237ec97733da935bd 2x"
loading="lazy" width="430"
alt="Structure of the Template Method pattern example" />
<figcaption><p>AI classes of a simple video game.</p></figcaption>
</figure>

All races in the game have almost the same types of units and buildings.
Therefore you can reuse the same AI structure for various races, while
being able to override some of the details. With this approach, you can
override the orcs' AI to make it more aggressive, make humans more
defense-oriented, and make monsters unable to build anything. Adding a
new race to the game would require creating a new AI subclass and
overriding the default methods declared in the base AI class.

<figure class="code">
<pre class="code" lang="pseudocode"><code>// The abstract class defines a template method that contains a
// skeleton of some algorithm composed of calls, usually to
// abstract primitive operations. Concrete subclasses implement
// these operations, but leave the template method itself
// intact.
class GameAI is
    // The template method defines the skeleton of an algorithm.
    method turn() is
        collectResources()
        buildStructures()
        buildUnits()
        attack()

    // Some of the steps may be implemented right in a base
    // class.
    method collectResources() is
        foreach (s in this.builtStructures) do
            s.collect()

    // And some of them may be defined as abstract.
    abstract method buildStructures()
    abstract method buildUnits()

    // A class can have several template methods.
    method attack() is
        enemy = closestEnemy()
        if (enemy == null)
            sendScouts(map.center)
        else
            sendWarriors(enemy.position)

    abstract method sendScouts(position)
    abstract method sendWarriors(position)

// Concrete classes have to implement all abstract operations of
// the base class but they must not override the template method
// itself.
class OrcsAI extends GameAI is
    method buildStructures() is
        if (there are some resources) then
            // Build farms, then barracks, then stronghold.

    method buildUnits() is
        if (there are plenty of resources) then
            if (there are no scouts)
                // Build peon, add it to scouts group.
            else
                // Build grunt, add it to warriors group.

    // ...

    method sendScouts(position) is
        if (scouts.length &gt; 0) then
            // Send scouts to position.

    method sendWarriors(position) is
        if (warriors.length &gt; 5) then
            // Send warriors to position.

// Subclasses can also override some operations with a default
// implementation.
class MonstersAI extends GameAI is
    method collectResources() is
        // Monsters don&#39;t collect resources.

    method buildStructures() is
        // Monsters don&#39;t build structures.

    method buildUnits() is
        // Monsters don&#39;t build units.</code></pre>
</figure>



##  Applicability



Use the Template Method pattern when you want to let clients extend only
particular steps of an algorithm, but not the whole algorithm or its
structure.



The Template Method lets you turn a monolithic algorithm into a series
of individual steps which can be easily extended by subclasses while
keeping intact the structure defined in a superclass.



Use the pattern when you have several classes that contain almost
identical algorithms with some minor differences. As a result, you might
need to modify all classes when the algorithm changes.



When you turn such an algorithm into a template method, you can also
pull up the steps with similar implementations into a superclass,
eliminating code duplication. Code that varies between subclasses can
remain in subclasses.





##  How to Implement {#checklist}

1.  Analyze the target algorithm to see whether you can break it into
    steps. Consider which steps are common to all subclasses and which
    ones will always be unique.

2.  Create the abstract base class and declare the template method and a
    set of abstract methods representing the algorithm's steps. Outline
    the algorithm's structure in the template method by executing
    corresponding steps. Consider making the template method `final` to
    prevent subclasses from overriding it.

3.  It's okay if all the steps end up being abstract. However, some
    steps might benefit from having a default implementation. Subclasses
    don't have to implement those methods.

4.  Think of adding hooks between the crucial steps of the algorithm.

5.  For each variation of the algorithm, create a new concrete subclass.
    It *must* implement all of the abstract steps, but *may* also
    override some of the optional ones.



##  Pros and Cons {#pros-cons}



-    You can let clients override only certain parts of a large
    algorithm, making them less affected by changes that happen to other
    parts of the algorithm.
-    You can pull the duplicate code into a superclass.



-    Some clients may be limited by the provided skeleton of an
    algorithm.
-    You might violate the *Liskov Substitution Principle* by
    suppressing a default step implementation via a subclass.
-    Template methods tend to be harder to maintain the more steps they
    have.





##  Relations with Other Patterns {#relations}

-   [Factory Method](/design-patterns/factory-method) is a
    specialization of [Template
    Method](/design-patterns/template-method). At the same time, a
    *Factory Method* may serve as a step in a large *Template Method*.

-   [Template Method](/design-patterns/template-method) is based on
    inheritance: it lets you alter parts of an algorithm by extending
    those parts in subclasses. [Strategy](/design-patterns/strategy) is
    based on composition: you can alter parts of the object's behavior
    by supplying it with different strategies that correspond to that
    behavior. *Template Method* works at the class level, so it's
    static. *Strategy* works on the object level, letting you switch
    behaviors at runtime.



##  Code Examples {#implementations}

[![Template Method in
C#](/images/patterns/icons/csharp.svg?id=da64592defc6e86d57c39c66e9de3e58){width="53"
height="53"
loading="lazy"}](/design-patterns/template-method/csharp/example "Template Method in C#"){.prog-lang-link}
[![Template Method in
C++](/images/patterns/icons/cpp.svg?id=f7782ed8b8666246bfcc3f8fefc3b858){width="53"
height="53"
loading="lazy"}](/design-patterns/template-method/cpp/example "Template Method in C++"){.prog-lang-link}
[![Template Method in
Go](/images/patterns/icons/go.svg?id=1a89927eb99b1ea3fde7701d97970aca){width="53"
height="53"
loading="lazy"}](/design-patterns/template-method/go/example "Template Method in Go"){.prog-lang-link}
[![Template Method in
Java](/images/patterns/icons/java.svg?id=e6d87e2dca08c953fe3acd1275ed4f4e){width="53"
height="53"
loading="lazy"}](/design-patterns/template-method/java/example "Template Method in Java"){.prog-lang-link}
[![Template Method in
PHP](/images/patterns/icons/php.svg?id=be1906eb26b71ec1d3b93720d6156618){width="53"
height="53"
loading="lazy"}](/design-patterns/template-method/php/example "Template Method in PHP"){.prog-lang-link}
[![Template Method in
Python](/images/patterns/icons/python.svg?id=6d815d43c0f7050a1151b43e51569c9f){width="53"
height="53"
loading="lazy"}](/design-patterns/template-method/python/example "Template Method in Python"){.prog-lang-link}
[![Template Method in
Ruby](/images/patterns/icons/ruby.svg?id=b065b718c914bf8e960ef731600be1eb){width="53"
height="53"
loading="lazy"}](/design-patterns/template-method/ruby/example "Template Method in Ruby"){.prog-lang-link}
[![Template Method in
Rust](/images/patterns/icons/rust.svg?id=1f5698a4b5ae23fe79413511747e4a87){width="53"
height="53"
loading="lazy"}](/design-patterns/template-method/rust/example "Template Method in Rust"){.prog-lang-link}
[![Template Method in
Swift](/images/patterns/icons/swift.svg?id=0b716c2d52ec3a48fbe91ac031070c1d){width="53"
height="53"
loading="lazy"}](/design-patterns/template-method/swift/example "Template Method in Swift"){.prog-lang-link}
[![Template Method in
TypeScript](/images/patterns/icons/typescript.svg?id=2239d0f16cb703540c205dd8cb0c0cb7){width="53"
height="53"
loading="lazy"}](/design-patterns/template-method/typescript/example "Template Method in TypeScript"){.prog-lang-link}





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

[Visitor []{.fa .fa-arrow-right}](/design-patterns/visitor){.btn
.btn-primary rel="next"}



#### Return

[[]{.fa .fa-arrow-left} Strategy](/design-patterns/strategy){.btn
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

    
    [English](https://refactoring.guru/design-patterns/template-method "English"){.dropdown-item
    .locale-link .active locale="en"}
    [Español](https://refactoring.guru/es/design-patterns/template-method "Español"){.dropdown-item
    .locale-link locale="es"}
    [Français](https://refactoring.guru/fr/design-patterns/template-method "Français"){.dropdown-item
    .locale-link locale="fr"}
    [日本語](https://refactoring.guru/ja/design-patterns/template-method "日本語"){.dropdown-item
    .locale-link locale="ja"}
    [한국어](https://refactoring.guru/ko/design-patterns/template-method "한국어"){.dropdown-item
    .locale-link locale="ko"}
    [Polski](https://refactoring.guru/pl/design-patterns/template-method "Polski"){.dropdown-item
    .locale-link locale="pl"} [Português
    Brasileiro](https://refactoring.guru/pt-br/design-patterns/template-method "Português Brasileiro"){.dropdown-item
    .locale-link locale="pt-br"}
    [Русский](https://refactoring.guru/ru/design-patterns/template-method "Русский"){.dropdown-item
    .locale-link locale="ru"}
    [Українська](https://refactoring.guru/uk/design-patterns/template-method "Українська"){.dropdown-item
    .locale-link locale="uk"}
    [中文](https://refactoringguru.cn/design-patterns/template-method "中文"){.dropdown-item
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






