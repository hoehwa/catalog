



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


# Prototype {#prototype .title}


Also known as: [Clone]{style="display:inline-block"}



##  Intent

**Prototype** is a creational design pattern that lets you copy existing
objects without making your code dependent on their classes.

<figure class="image">
<img
src="/images/patterns/content/prototype/prototype.png?id=e912b1ada20bbf7b2ffc09e93b9fab20"
srcset="/images/patterns/content/prototype/prototype-2x.png?id=670789c80c8a114e25838ede2da4a881 2x"
width="640" alt="Prototype Design Pattern" />
</figure>



##  Problem

Say you have an object, and you want to create an exact copy of it. How
would you do it? First, you have to create a new object of the same
class. Then you have to go through all the fields of the original object
and copy their values over to the new object.

Nice! But there's a catch. Not all objects can be copied that way
because some of the object's fields may be private and not visible from
outside of the object itself.

<figure class="image">
<img
src="/images/patterns/content/prototype/prototype-comic-1-en.png?id=4cc45ae42e26cc9533a6ac540713d1fa"
data-600"=""
srcset="/images/patterns/content/prototype/prototype-comic-1-en-2x.png?id=1f5b9eeb00df663f4630ca6d38c4804d 2x"
loading="lazy"
alt="What can go wrong when copying things “from the outside&quot;?” width=" />
<figcaption><p>Copying an object “from the outside” <a
href="/cargo-cult">isn’t</a> always possible.</p></figcaption>
</figure>

There's one more problem with the direct approach. Since you have to
know the object's class to create a duplicate, your code becomes
dependent on that class. If the extra dependency doesn't scare you,
there's another catch. Sometimes you only know the interface that the
object follows, but not its concrete class, when, for example, a
parameter in a method accepts any objects that follow some interface.



##  Solution

The Prototype pattern delegates the cloning process to the actual
objects that are being cloned. The pattern declares a common interface
for all objects that support cloning. This interface lets you clone an
object without coupling your code to the class of that object. Usually,
such an interface contains just a single `clone` method.

The implementation of the `clone` method is very similar in all classes.
The method creates an object of the current class and carries over all
of the field values of the old object into the new one. You can even
copy private fields because most programming languages let objects
access private fields of other objects that belong to the same class.

An object that supports cloning is called a *prototype*. When your
objects have dozens of fields and hundreds of possible configurations,
cloning them might serve as an alternative to subclassing.

<figure class="image">
<img
src="/images/patterns/content/prototype/prototype-comic-2-en.png?id=e1df2dc39404c5eb2d485b7ae7c9914f"
srcset="/images/patterns/content/prototype/prototype-comic-2-en-2x.png?id=dda1589983832b69aee763037293beab 2x"
loading="lazy" width="343" alt="Pre-built prototypes" />
<figcaption><p>Pre-built prototypes can be an alternative
to subclassing.</p></figcaption>
</figure>

Here's how it works: you create a set of objects, configured in various
ways. When you need an object like the one you've configured, you just
clone a prototype instead of constructing a new object from scratch.



##  Real-World Analogy {#analogy}

In real life, prototypes are used for performing various tests before
starting mass production of a product. However, in this case, prototypes
don't participate in any actual production, playing a passive role
instead.

<figure class="image">
<img
src="/images/patterns/content/prototype/prototype-comic-3-en.png?id=ff16dedbd0c10944d27bf87d2adcf8a6"
srcset="/images/patterns/content/prototype/prototype-comic-3-en-2x.png?id=63dd16812865486d174b646882effd9a 2x"
loading="lazy" width="600" alt="The cell division" />
<figcaption><p>The division of a cell.</p></figcaption>
</figure>

Since industrial prototypes don't really copy themselves, a much closer
analogy to the pattern is the process of mitotic cell division (biology,
remember?). After mitotic division, a pair of identical cells is formed.
The original cell acts as a prototype and takes an active role in
creating the copy.



##  Structure


#### Basic implementation



<figure class="image">
<img
src="/images/patterns/diagrams/prototype/structure.png?id=088102c5e9785ff45debbbce86f4df81"
class="structure-img-non-indexed d-none d-xl-block"
srcset="/images/patterns/diagrams/prototype/structure-2x.png?id=ba75079f42f08028ae4cdbda0cfecc26 2x"
loading="lazy" width="500"
alt="The structure of the Prototype design pattern" /><img
src="/images/patterns/diagrams/prototype/structure-indexed.png?id=0e1c809842f5c43aca0541a2eba1f844"
class="structure-img-indexed d-xl-none"
srcset="/images/patterns/diagrams/prototype/structure-indexed-2x.png?id=74584ac729c0f6b49d2a97a53cc266ff 2x"
loading="lazy" width="520"
alt="The structure of the Prototype design pattern" />
</figure>



1.  The **Prototype** interface declares the cloning methods. In most
    cases, it's a single `clone` method.

2.  The **Concrete Prototype** class implements the cloning method. In
    addition to copying the original object's data to the clone, this
    method may also handle some edge cases of the cloning process
    related to cloning linked objects, untangling recursive
    dependencies, etc.

3.  The **Client** can produce a copy of any object that follows the
    prototype interface.

#### Prototype registry implementation



<figure class="image">
<img
src="/images/patterns/diagrams/prototype/structure-prototype-cache.png?id=609c2af5d14ed55dcbb218a00f98e7d5"
class="structure-img-non-indexed d-none d-xl-block"
srcset="/images/patterns/diagrams/prototype/structure-prototype-cache-2x.png?id=a1e4514bbcc9b10968b856f19b407105 2x"
loading="lazy" width="550" alt="The prototype registry" /><img
src="/images/patterns/diagrams/prototype/structure-prototype-cache-indexed.png?id=10a4a84a1a318f59dbc2b806fc936d04"
class="structure-img-indexed d-xl-none"
srcset="/images/patterns/diagrams/prototype/structure-prototype-cache-indexed-2x.png?id=47b99eb7ae51158bdbb31deea4f5e98f 2x"
loading="lazy" width="550" alt="The prototype registry" />
</figure>



1.  The **Prototype Registry** provides an easy way to access
    frequently-used prototypes. It stores a set of pre-built objects
    that are ready to be copied. The simplest prototype registry is a
    `name → prototype` hash map. However, if you need better search
    criteria than a simple name, you can build a much more robust
    version of the registry.




##  Pseudocode

In this example, the **Prototype** pattern lets you produce exact copies
of geometric objects, without coupling the code to their classes.

<figure class="image">
<img
src="/images/patterns/diagrams/prototype/example.png?id=47bc6c1058cb100b81e675b5ca6bda6c"
srcset="/images/patterns/diagrams/prototype/example-2x.png?id=80393e0df17ae8130e5ada832d494949 2x"
loading="lazy" width="470"
alt="The structure of the Prototype pattern example" />
<figcaption><p>Cloning a set of objects that belong to a
class hierarchy.</p></figcaption>
</figure>

All shape classes follow the same interface, which provides a cloning
method. A subclass may call the parent's cloning method before copying
its own field values to the resulting object.

<figure class="code">
<pre class="code" lang="pseudocode"><code>// Base prototype.
abstract class Shape is
    field X: int
    field Y: int
    field color: string

    // A regular constructor.
    constructor Shape() is
        // ...

    // The prototype constructor. A fresh object is initialized
    // with values from the existing object.
    constructor Shape(source: Shape) is
        this()
        this.X = source.X
        this.Y = source.Y
        this.color = source.color

    // The clone operation returns one of the Shape subclasses.
    abstract method clone():Shape


// Concrete prototype. The cloning method creates a new object
// in one go by calling the constructor of the current class and
// passing the current object as the constructor&#39;s argument.
// Performing all the actual copying in the constructor helps to
// keep the result consistent: the constructor will not return a
// result until the new object is fully built; thus, no object
// can have a reference to a partially-built clone.
class Rectangle extends Shape is
    field width: int
    field height: int

    constructor Rectangle(source: Rectangle) is
        // A parent constructor call is needed to copy private
        // fields defined in the parent class.
        super(source)
        this.width = source.width
        this.height = source.height

    method clone():Shape is
        return new Rectangle(this)


class Circle extends Shape is
    field radius: int

    constructor Circle(source: Circle) is
        super(source)
        this.radius = source.radius

    method clone():Shape is
        return new Circle(this)


// Somewhere in the client code.
class Application is
    field shapes: array of Shape

    constructor Application() is
        Circle circle = new Circle()
        circle.X = 10
        circle.Y = 10
        circle.radius = 20
        shapes.add(circle)

        Circle anotherCircle = circle.clone()
        shapes.add(anotherCircle)
        // The `anotherCircle` variable contains an exact copy
        // of the `circle` object.

        Rectangle rectangle = new Rectangle()
        rectangle.width = 10
        rectangle.height = 20
        shapes.add(rectangle)

    method businessLogic() is
        // Prototype rocks because it lets you produce a copy of
        // an object without knowing anything about its type.
        Array shapesCopy = new Array of Shapes.

        // For instance, we don&#39;t know the exact elements in the
        // shapes array. All we know is that they are all
        // shapes. But thanks to polymorphism, when we call the
        // `clone` method on a shape the program checks its real
        // class and runs the appropriate clone method defined
        // in that class. That&#39;s why we get proper clones
        // instead of a set of simple Shape objects.
        foreach (s in shapes) do
            shapesCopy.add(s.clone())

        // The `shapesCopy` array contains exact copies of the
        // `shape` array&#39;s children.</code></pre>
</figure>



##  Applicability



Use the Prototype pattern when your code shouldn't depend on the
concrete classes of objects that you need to copy.



This happens a lot when your code works with objects passed to you from
3rd-party code via some interface. The concrete classes of these objects
are unknown, and you couldn't depend on them even if you wanted to.

The Prototype pattern provides the client code with a general interface
for working with all objects that support cloning. This interface makes
the client code independent from the concrete classes of objects that it
clones.



Use the pattern when you want to reduce the number of subclasses that
only differ in the way they initialize their respective objects.



Suppose you have a complex class that requires a laborious configuration
before it can be used. There are several common ways to configure this
class, and this code is scattered through your app. To reduce the
duplication, you create several subclasses and put every common
configuration code into their constructors. You solved the duplication
problem, but now you have lots of dummy subclasses.

The Prototype pattern lets you use a set of pre-built objects configured
in various ways as prototypes. Instead of instantiating a subclass that
matches some configuration, the client can simply look for an
appropriate prototype and clone it.





##  How to Implement {#checklist}

1.  Create the prototype interface and declare the `clone` method in it.
    Or just add the method to all classes of an existing class
    hierarchy, if you have one.

2.  A prototype class must define the alternative constructor that
    accepts an object of that class as an argument. The constructor must
    copy the values of all fields defined in the class from the passed
    object into the newly created instance. If you're changing a
    subclass, you must call the parent constructor to let the superclass
    handle the cloning of its private fields.

    If your programming language doesn't support method overloading, you
    won't be able to create a separate "prototype" constructor. Thus,
    copying the object's data into the newly created clone will have to
    be performed within the `clone` method. Still, having this code in a
    regular constructor is safer because the resulting object is
    returned fully configured right after you call the `new` operator.

3.  The cloning method usually consists of just one line: running a
    `new` operator with the prototypical version of the constructor.
    Note, that every class must explicitly override the cloning method
    and use its own class name along with the `new` operator. Otherwise,
    the cloning method may produce an object of a parent class.

4.  Optionally, create a centralized prototype registry to store a
    catalog of frequently used prototypes.

    You can implement the registry as a new factory class or put it in
    the base prototype class with a static method for fetching the
    prototype. This method should search for a prototype based on search
    criteria that the client code passes to the method. The criteria
    might either be a simple string tag or a complex set of search
    parameters. After the appropriate prototype is found, the registry
    should clone it and return the copy to the client.

    Finally, replace the direct calls to the subclasses' constructors
    with calls to the factory method of the prototype registry.



##  Pros and Cons {#pros-cons}



-    You can clone objects without coupling to their concrete classes.
-    You can get rid of repeated initialization code in favor of cloning
    pre-built prototypes.
-    You can produce complex objects more conveniently.
-    You get an alternative to inheritance when dealing with
    configuration presets for complex objects.



-    Cloning complex objects that have circular references might be very
    tricky.





##  Relations with Other Patterns {#relations}

-   Many designs start by using [Factory
    Method](/design-patterns/factory-method) (less complicated and more
    customizable via subclasses) and evolve toward [Abstract
    Factory](/design-patterns/abstract-factory),
    [Prototype](/design-patterns/prototype), or
    [Builder](/design-patterns/builder) (more flexible, but more
    complicated).

-   [Abstract Factory](/design-patterns/abstract-factory) classes are
    often based on a set of [Factory
    Methods](/design-patterns/factory-method), but you can also use
    [Prototype](/design-patterns/prototype) to compose the methods on
    these classes.

-   [Prototype](/design-patterns/prototype) can help when you need to
    save copies of [Commands](/design-patterns/command) into history.

-   Designs that make heavy use of
    [Composite](/design-patterns/composite) and
    [Decorator](/design-patterns/decorator) can often benefit from using
    [Prototype](/design-patterns/prototype). Applying the pattern lets
    you clone complex structures instead of re-constructing them from
    scratch.

-   [Prototype](/design-patterns/prototype) isn't based on inheritance,
    so it doesn't have its drawbacks. On the other hand, *Prototype*
    requires a complicated initialization of the cloned object. [Factory
    Method](/design-patterns/factory-method) is based on inheritance but
    doesn't require an initialization step.

-   Sometimes [Prototype](/design-patterns/prototype) can be a simpler
    alternative to [Memento](/design-patterns/memento). This works if
    the object, the state of which you want to store in the history, is
    fairly straightforward and doesn't have links to external resources,
    or the links are easy to re-establish.

-   [Abstract Factories](/design-patterns/abstract-factory),
    [Builders](/design-patterns/builder) and
    [Prototypes](/design-patterns/prototype) can all be implemented as
    [Singletons](/design-patterns/singleton).



##  Code Examples {#implementations}

[![Prototype in
C#](/images/patterns/icons/csharp.svg?id=da64592defc6e86d57c39c66e9de3e58){width="53"
height="53"
loading="lazy"}](/design-patterns/prototype/csharp/example "Prototype in C#"){.prog-lang-link}
[![Prototype in
C++](/images/patterns/icons/cpp.svg?id=f7782ed8b8666246bfcc3f8fefc3b858){width="53"
height="53"
loading="lazy"}](/design-patterns/prototype/cpp/example "Prototype in C++"){.prog-lang-link}
[![Prototype in
Go](/images/patterns/icons/go.svg?id=1a89927eb99b1ea3fde7701d97970aca){width="53"
height="53"
loading="lazy"}](/design-patterns/prototype/go/example "Prototype in Go"){.prog-lang-link}
[![Prototype in
Java](/images/patterns/icons/java.svg?id=e6d87e2dca08c953fe3acd1275ed4f4e){width="53"
height="53"
loading="lazy"}](/design-patterns/prototype/java/example "Prototype in Java"){.prog-lang-link}
[![Prototype in
PHP](/images/patterns/icons/php.svg?id=be1906eb26b71ec1d3b93720d6156618){width="53"
height="53"
loading="lazy"}](/design-patterns/prototype/php/example "Prototype in PHP"){.prog-lang-link}
[![Prototype in
Python](/images/patterns/icons/python.svg?id=6d815d43c0f7050a1151b43e51569c9f){width="53"
height="53"
loading="lazy"}](/design-patterns/prototype/python/example "Prototype in Python"){.prog-lang-link}
[![Prototype in
Ruby](/images/patterns/icons/ruby.svg?id=b065b718c914bf8e960ef731600be1eb){width="53"
height="53"
loading="lazy"}](/design-patterns/prototype/ruby/example "Prototype in Ruby"){.prog-lang-link}
[![Prototype in
Rust](/images/patterns/icons/rust.svg?id=1f5698a4b5ae23fe79413511747e4a87){width="53"
height="53"
loading="lazy"}](/design-patterns/prototype/rust/example "Prototype in Rust"){.prog-lang-link}
[![Prototype in
Swift](/images/patterns/icons/swift.svg?id=0b716c2d52ec3a48fbe91ac031070c1d){width="53"
height="53"
loading="lazy"}](/design-patterns/prototype/swift/example "Prototype in Swift"){.prog-lang-link}
[![Prototype in
TypeScript](/images/patterns/icons/typescript.svg?id=2239d0f16cb703540c205dd8cb0c0cb7){width="53"
height="53"
loading="lazy"}](/design-patterns/prototype/typescript/example "Prototype in TypeScript"){.prog-lang-link}





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

[Singleton []{.fa .fa-arrow-right}](/design-patterns/singleton){.btn
.btn-primary rel="next"}



#### Return

[[]{.fa .fa-arrow-left} Builder](/design-patterns/builder){.btn
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

    
    [English](https://refactoring.guru/design-patterns/prototype "English"){.dropdown-item
    .locale-link .active locale="en"}
    [Español](https://refactoring.guru/es/design-patterns/prototype "Español"){.dropdown-item
    .locale-link locale="es"}
    [Français](https://refactoring.guru/fr/design-patterns/prototype "Français"){.dropdown-item
    .locale-link locale="fr"}
    [日本語](https://refactoring.guru/ja/design-patterns/prototype "日本語"){.dropdown-item
    .locale-link locale="ja"}
    [한국어](https://refactoring.guru/ko/design-patterns/prototype "한국어"){.dropdown-item
    .locale-link locale="ko"}
    [Polski](https://refactoring.guru/pl/design-patterns/prototype "Polski"){.dropdown-item
    .locale-link locale="pl"} [Português
    Brasileiro](https://refactoring.guru/pt-br/design-patterns/prototype "Português Brasileiro"){.dropdown-item
    .locale-link locale="pt-br"}
    [Русский](https://refactoring.guru/ru/design-patterns/prototype "Русский"){.dropdown-item
    .locale-link locale="ru"}
    [Українська](https://refactoring.guru/uk/design-patterns/prototype "Українська"){.dropdown-item
    .locale-link locale="uk"}
    [中文](https://refactoringguru.cn/design-patterns/prototype "中文"){.dropdown-item
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






