



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








[](/){.home} / [Design Patterns](/design-patterns){.type} / [Creational
Patterns](/design-patterns/creational-patterns){.type}


# Singleton {#singleton .title}


##  Intent

**Singleton** is a creational design pattern that lets you ensure that a
class has only one instance, while providing a global access point to
this instance.

<figure class="image">
<img
src="/images/patterns/content/singleton/singleton.png?id=108a0b9b5ea5c4426e0afa4504491d6f"
srcset="/images/patterns/content/singleton/singleton-2x.png?id=accb2cc7594f7a491ce01dddf0d2f876 2x"
width="640" alt="Singleton pattern" />
</figure>



##  Problem

The Singleton pattern solves two problems at the same time, violating
the *Single Responsibility Principle*:

1.  **Ensure that a class has just a single instance**. Why would anyone
    want to control how many instances a class has? The most common
    reason for this is to control access to some shared resource---for
    example, a database or a file.

    Here's how it works: imagine that you created an object, but after a
    while decided to create a new one. Instead of receiving a fresh
    object, you'll get the one you already created.

    Note that this behavior is impossible to implement with a regular
    constructor since a constructor call **must** always return a new
    object by design.

<figure class="image">
<img
src="/images/patterns/content/singleton/singleton-comic-1-en.png?id=157509c5693a657ba465c7a9d58a7c25"
srcset="/images/patterns/content/singleton/singleton-comic-1-en-2x.png?id=05678e879d13f7f6a377bab7fba18acc 2x"
loading="lazy" width="600" alt="The global access to an object" />
<figcaption><p>Clients may not even realize that they’re working with
the same object all the time.</p></figcaption>
</figure>

2.  **Provide a global access point to that instance**. Remember those
    global variables that you (all right, me) used to store some
    essential objects? While they're very handy, they're also very
    unsafe since any code can potentially overwrite the contents of
    those variables and crash the app.

    Just like a global variable, the Singleton pattern lets you access
    some object from anywhere in the program. However, it also protects
    that instance from being overwritten by other code.

    There's another side to this problem: you don't want the code that
    solves problem #1 to be scattered all over your program. It's much
    better to have it within one class, especially if the rest of your
    code already depends on it.

Nowadays, the Singleton pattern has become so popular that people may
call something a *singleton* even if it solves just one of the listed
problems.



##  Solution

All implementations of the Singleton have these two steps in common:

-   Make the default constructor private, to prevent other objects from
    using the `new` operator with the Singleton class.
-   Create a static creation method that acts as a constructor. Under
    the hood, this method calls the private constructor to create an
    object and saves it in a static field. All following calls to this
    method return the cached object.

If your code has access to the Singleton class, then it's able to call
the Singleton's static method. So whenever that method is called, the
same object is always returned.



##  Real-World Analogy {#analogy}

The government is an excellent example of the Singleton pattern. A
country can have only one official government. Regardless of the
personal identities of the individuals who form governments, the title,
"The Government of X", is a global point of access that identifies the
group of people in charge.



##  Structure



<figure class="image">
<img
src="/images/patterns/diagrams/singleton/structure-en.png?id=4e4306d3a90f40d74c7a4d2d2506b8ec"
class="structure-img-non-indexed d-none d-xl-block"
srcset="/images/patterns/diagrams/singleton/structure-en-2x.png?id=cae4853e43f06db09f249668c35d61a1 2x"
loading="lazy" width="430"
alt="The structure of the Singleton pattern" /><img
src="/images/patterns/diagrams/singleton/structure-en-indexed.png?id=b0217ae066cd3b757677d119551f9a8f"
class="structure-img-indexed d-xl-none"
srcset="/images/patterns/diagrams/singleton/structure-en-indexed-2x.png?id=d552220be21d0eda3a8cbe5ccec6dad1 2x"
loading="lazy" width="430"
alt="The structure of the Singleton pattern" />
</figure>


1.  The **Singleton** class declares the static method `getInstance`
    that returns the same instance of its own class.

    The Singleton's constructor should be hidden from the client code.
    Calling the `getInstance` method should be the only way of getting
    the Singleton object.




##  Pseudocode

In this example, the database connection class acts as a **Singleton**.
This class doesn't have a public constructor, so the only way to get its
object is to call the `getInstance` method. This method caches the first
created object and returns it in all subsequent calls.

<figure class="code">
<pre class="code" lang="pseudocode"><code>// The Database class defines the `getInstance` method that lets
// clients access the same instance of a database connection
// throughout the program.
class Database is
    // The field for storing the singleton instance should be
    // declared static.
    private static field instance: Database

    // The singleton&#39;s constructor should always be private to
    // prevent direct construction calls with the `new`
    // operator.
    private constructor Database() is
        // Some initialization code, such as the actual
        // connection to a database server.
        // ...

    // The static method that controls access to the singleton
    // instance.
    public static method getInstance() is
        if (Database.instance == null) then
            acquireThreadLock() and then
                // Ensure that the instance hasn&#39;t yet been
                // initialized by another thread while this one
                // has been waiting for the lock&#39;s release.
                if (Database.instance == null) then
                    Database.instance = new Database()
        return Database.instance

    // Finally, any singleton should define some business logic
    // which can be executed on its instance.
    public method query(sql) is
        // For instance, all database queries of an app go
        // through this method. Therefore, you can place
        // throttling or caching logic here.
        // ...

class Application is
    method main() is
        Database foo = Database.getInstance()
        foo.query(&quot;SELECT ...&quot;)
        // ...
        Database bar = Database.getInstance()
        bar.query(&quot;SELECT ...&quot;)
        // The variable `bar` will contain the same object as
        // the variable `foo`.</code></pre>
</figure>



##  Applicability



Use the Singleton pattern when a class in your program should have just
a single instance available to all clients; for example, a single
database object shared by different parts of the program.



The Singleton pattern disables all other means of creating objects of a
class except for the special creation method. This method either creates
a new object or returns an existing one if it has already been created.



Use the Singleton pattern when you need stricter control over global
variables.



Unlike global variables, the Singleton pattern guarantees that there's
just one instance of a class. Nothing, except for the Singleton class
itself, can replace the cached instance.

Note that you can always adjust this limitation and allow creating any
number of Singleton instances. The only piece of code that needs
changing is the body of the `getInstance` method.





##  How to Implement {#checklist}

1.  Add a private static field to the class for storing the singleton
    instance.

2.  Declare a public static creation method for getting the singleton
    instance.

3.  Implement "lazy initialization" inside the static method. It should
    create a new object on its first call and put it into the static
    field. The method should always return that instance on all
    subsequent calls.

4.  Make the constructor of the class private. The static method of the
    class will still be able to call the constructor, but not the other
    objects.

5.  Go over the client code and replace all direct calls to the
    singleton's constructor with calls to its static creation method.



##  Pros and Cons {#pros-cons}



-    You can be sure that a class has only a single instance.
-    You gain a global access point to that instance.
-    The singleton object is initialized only when it's requested for
    the first time.



-    Violates the *Single Responsibility Principle*. The pattern solves
    two problems at the time.
-    The Singleton pattern can mask bad design, for instance, when the
    components of the program know too much about each other.
-    The pattern requires special treatment in a multithreaded
    environment so that multiple threads won't create a singleton object
    several times.
-    It may be difficult to unit test the client code of the Singleton
    because many test frameworks rely on inheritance when producing mock
    objects. Since the constructor of the singleton class is private and
    overriding static methods is impossible in most languages, you will
    need to think of a creative way to mock the singleton. Or just don't
    write the tests. Or don't use the Singleton pattern.





##  Relations with Other Patterns {#relations}

-   A [Facade](/design-patterns/facade) class can often be transformed
    into a [Singleton](/design-patterns/singleton) since a single facade
    object is sufficient in most cases.

-   [Flyweight](/design-patterns/flyweight) would resemble
    [Singleton](/design-patterns/singleton) if you somehow managed to
    reduce all shared states of the objects to just one flyweight
    object. But there are two fundamental differences between these
    patterns:

    1.  There should be only one Singleton instance, whereas a
        *Flyweight* class can have multiple instances with different
        intrinsic states.
    2.  The *Singleton* object can be mutable. Flyweight objects are
        immutable.

-   [Abstract Factories](/design-patterns/abstract-factory),
    [Builders](/design-patterns/builder) and
    [Prototypes](/design-patterns/prototype) can all be implemented as
    [Singletons](/design-patterns/singleton).



##  Code Examples {#implementations}

[![Singleton in
C#](/images/patterns/icons/csharp.svg?id=da64592defc6e86d57c39c66e9de3e58){width="53"
height="53"
loading="lazy"}](/design-patterns/singleton/csharp/example "Singleton in C#"){.prog-lang-link}
[![Singleton in
C++](/images/patterns/icons/cpp.svg?id=f7782ed8b8666246bfcc3f8fefc3b858){width="53"
height="53"
loading="lazy"}](/design-patterns/singleton/cpp/example "Singleton in C++"){.prog-lang-link}
[![Singleton in
Go](/images/patterns/icons/go.svg?id=1a89927eb99b1ea3fde7701d97970aca){width="53"
height="53"
loading="lazy"}](/design-patterns/singleton/go/example "Singleton in Go"){.prog-lang-link}
[![Singleton in
Java](/images/patterns/icons/java.svg?id=e6d87e2dca08c953fe3acd1275ed4f4e){width="53"
height="53"
loading="lazy"}](/design-patterns/singleton/java/example "Singleton in Java"){.prog-lang-link}
[![Singleton in
PHP](/images/patterns/icons/php.svg?id=be1906eb26b71ec1d3b93720d6156618){width="53"
height="53"
loading="lazy"}](/design-patterns/singleton/php/example "Singleton in PHP"){.prog-lang-link}
[![Singleton in
Python](/images/patterns/icons/python.svg?id=6d815d43c0f7050a1151b43e51569c9f){width="53"
height="53"
loading="lazy"}](/design-patterns/singleton/python/example "Singleton in Python"){.prog-lang-link}
[![Singleton in
Ruby](/images/patterns/icons/ruby.svg?id=b065b718c914bf8e960ef731600be1eb){width="53"
height="53"
loading="lazy"}](/design-patterns/singleton/ruby/example "Singleton in Ruby"){.prog-lang-link}
[![Singleton in
Rust](/images/patterns/icons/rust.svg?id=1f5698a4b5ae23fe79413511747e4a87){width="53"
height="53"
loading="lazy"}](/design-patterns/singleton/rust/example "Singleton in Rust"){.prog-lang-link}
[![Singleton in
Swift](/images/patterns/icons/swift.svg?id=0b716c2d52ec3a48fbe91ac031070c1d){width="53"
height="53"
loading="lazy"}](/design-patterns/singleton/swift/example "Singleton in Swift"){.prog-lang-link}
[![Singleton in
TypeScript](/images/patterns/icons/typescript.svg?id=2239d0f16cb703540c205dd8cb0c0cb7){width="53"
height="53"
loading="lazy"}](/design-patterns/singleton/typescript/example "Singleton in TypeScript"){.prog-lang-link}





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

[Structural Patterns []{.fa
.fa-arrow-right}](/design-patterns/structural-patterns){.btn
.btn-primary rel="next"}



#### Return

[[]{.fa .fa-arrow-left} Prototype](/design-patterns/prototype){.btn
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

    
    [English](https://refactoring.guru/design-patterns/singleton "English"){.dropdown-item
    .locale-link .active locale="en"}
    [Español](https://refactoring.guru/es/design-patterns/singleton "Español"){.dropdown-item
    .locale-link locale="es"}
    [Français](https://refactoring.guru/fr/design-patterns/singleton "Français"){.dropdown-item
    .locale-link locale="fr"}
    [日本語](https://refactoring.guru/ja/design-patterns/singleton "日本語"){.dropdown-item
    .locale-link locale="ja"}
    [한국어](https://refactoring.guru/ko/design-patterns/singleton "한국어"){.dropdown-item
    .locale-link locale="ko"}
    [Polski](https://refactoring.guru/pl/design-patterns/singleton "Polski"){.dropdown-item
    .locale-link locale="pl"} [Português
    Brasileiro](https://refactoring.guru/pt-br/design-patterns/singleton "Português Brasileiro"){.dropdown-item
    .locale-link locale="pt-br"}
    [Русский](https://refactoring.guru/ru/design-patterns/singleton "Русский"){.dropdown-item
    .locale-link locale="ru"}
    [Українська](https://refactoring.guru/uk/design-patterns/singleton "Українська"){.dropdown-item
    .locale-link locale="uk"}
    [中文](https://refactoringguru.cn/design-patterns/singleton "中文"){.dropdown-item
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






