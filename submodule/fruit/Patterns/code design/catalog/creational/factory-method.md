



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


# Factory Method {#factory-method .title}


Also known as: [Virtual Constructor]{style="display:inline-block"}



##  Intent

**Factory Method** is a creational design pattern that provides an
interface for creating objects in a superclass, but allows subclasses to
alter the type of objects that will be created.

<figure class="image">
<img
src="/images/patterns/content/factory-method/factory-method-en.png?id=cfa26f33dc8473e803fadae0d262100a"
srcset="/images/patterns/content/factory-method/factory-method-en-2x.png?id=b3961995a4449fb90820a693013511df 2x"
width="640" alt="Factory Method pattern" />
</figure>



##  Problem

Imagine that you're creating a logistics management application. The
first version of your app can only handle transportation by trucks, so
the bulk of your code lives inside the `Truck` class.

After a while, your app becomes pretty popular. Each day you receive
dozens of requests from sea transportation companies to incorporate sea
logistics into the app.

<figure class="image">
<img
src="/images/patterns/diagrams/factory-method/problem1-en.png?id=de638561be0bbb1025ada6bfcb815def"
srcset="/images/patterns/diagrams/factory-method/problem1-en-2x.png?id=9a4959d9dde4edadf809be33d3da0c74 2x"
loading="lazy" width="600"
alt="Adding a new transportation class to the program causes an issue" />
<figcaption><p>Adding a new class to the program isn’t that simple if
the rest of the code is already coupled to
existing classes.</p></figcaption>
</figure>

Great news, right? But how about the code? At present, most of your code
is coupled to the `Truck` class. Adding `Ships` into the app would
require making changes to the entire codebase. Moreover, if later you
decide to add another type of transportation to the app, you will
probably need to make all of these changes again.

As a result, you will end up with pretty nasty code, riddled with
conditionals that switch the app's behavior depending on the class of
transportation objects.



##  Solution

The Factory Method pattern suggests that you replace direct object
construction calls (using the `new` operator) with calls to a special
*factory* method. Don't worry: the objects are still created via the
`new` operator, but it's being called from within the factory method.
Objects returned by a factory method are often referred to as
*products.*

<figure class="image">
<img
src="/images/patterns/diagrams/factory-method/solution1.png?id=fc756d2af296b5b4d482e548214d08ef"
srcset="/images/patterns/diagrams/factory-method/solution1-2x.png?id=c482b3cd7a4d8dd73b4c8c12dfcaa03c 2x"
loading="lazy" width="620" alt="The structure of creator classes" />
<figcaption><p>Subclasses can alter the class of objects being returned
by the factory method.</p></figcaption>
</figure>

At first glance, this change may look pointless: we just moved the
constructor call from one part of the program to another. However,
consider this: now you can override the factory method in a subclass and
change the class of products being created by the method.

There's a slight limitation though: subclasses may return different
types of products only if these products have a common base class or
interface. Also, the factory method in the base class should have its
return type declared as this interface.

<figure class="image">
<img
src="/images/patterns/diagrams/factory-method/solution2-en.png?id=db5de848c1d490b835666ef54d131d46"
srcset="/images/patterns/diagrams/factory-method/solution2-en-2x.png?id=1209a3156e450b9d7c437ca6bb98b219 2x"
loading="lazy" width="490"
alt="The structure of the products hierarchy" />
<figcaption><p>All products must follow the
same interface.</p></figcaption>
</figure>

For example, both `Truck` and `Ship` classes should implement the
`Transport` interface, which declares a method called `deliver`. Each
class implements this method differently: trucks deliver cargo by land,
ships deliver cargo by sea. The factory method in the `RoadLogistics`
class returns truck objects, whereas the factory method in the
`SeaLogistics` class returns ships.

<figure class="image">
<img
src="/images/patterns/diagrams/factory-method/solution3-en.png?id=b6f53911fc0d56f9ef99501fc4aec059"
srcset="/images/patterns/diagrams/factory-method/solution3-en-2x.png?id=542c0ba89e91ac11ea79e94bc0229f70 2x"
loading="lazy" width="640"
alt="The structure of the code after applying the factory method pattern" />
<figcaption><p>As long as all product classes implement a common
interface, you can pass their objects to the client code without
breaking it.</p></figcaption>
</figure>

The code that uses the factory method (often called the *client* code)
doesn't see a difference between the actual products returned by various
subclasses. The client treats all the products as abstract `Transport`.
The client knows that all transport objects are supposed to have the
`deliver` method, but exactly how it works isn't important to the
client.



##  Structure



<figure class="image">
<img
src="/images/patterns/diagrams/factory-method/structure.png?id=4cba0803f42517cfe8548c9bc7dc4c9b"
class="structure-img-non-indexed d-none d-xl-block"
srcset="/images/patterns/diagrams/factory-method/structure-2x.png?id=9ea3aa8a47f8be22e12e523c15b448fd 2x"
loading="lazy" width="660"
alt="The structure of the Factory Method pattern" /><img
src="/images/patterns/diagrams/factory-method/structure-indexed.png?id=4c603207859ca1f939b17b60a3a2e9e0"
class="structure-img-indexed d-xl-none"
srcset="/images/patterns/diagrams/factory-method/structure-indexed-2x.png?id=c794e4f2d05013fb176464a1d1a5d7ab 2x"
loading="lazy" width="660"
alt="The structure of the Factory Method pattern" />
</figure>


1.  The **Product** declares the interface, which is common to all
    objects that can be produced by the creator and its subclasses.

2.  **Concrete Products** are different implementations of the product
    interface.

3.  The **Creator** class declares the factory method that returns new
    product objects. It's important that the return type of this method
    matches the product interface.

    You can declare the factory method as `abstract` to force all
    subclasses to implement their own versions of the method. As an
    alternative, the base factory method can return some default product
    type.

    Note, despite its name, product creation is **not** the primary
    responsibility of the creator. Usually, the creator class already
    has some core business logic related to products. The factory method
    helps to decouple this logic from the concrete product classes. Here
    is an analogy: a large software development company can have a
    training department for programmers. However, the primary function
    of the company as a whole is still writing code, not producing
    programmers.

4.  **Concrete Creators** override the base factory method so it returns
    a different type of product.

    Note that the factory method doesn't have to **create** new
    instances all the time. It can also return existing objects from a
    cache, an object pool, or another source.




##  Pseudocode

This example illustrates how the **Factory Method** can be used for
creating cross-platform UI elements without coupling the client code to
concrete UI classes.

<figure class="image">
<img
src="/images/patterns/diagrams/factory-method/example.png?id=67db9a5cb817913444efcb1c067c9835"
srcset="/images/patterns/diagrams/factory-method/example-2x.png?id=a2470830778e318263155000dbdc5870 2x"
loading="lazy" width="640"
alt="The structure of the Factory Method pattern example" />
<figcaption><p>The cross-platform dialog example.</p></figcaption>
</figure>

The base `Dialog` class uses different UI elements to render its window.
Under various operating systems, these elements may look a little bit
different, but they should still behave consistently. A button in
Windows is still a button in Linux.

When the factory method comes into play, you don't need to rewrite the
logic of the `Dialog` class for each operating system. If we declare a
factory method that produces buttons inside the base `Dialog` class, we
can later create a subclass that returns Windows-styled buttons from the
factory method. The subclass then inherits most of the code from the
base class, but, thanks to the factory method, can render
Windows-looking buttons on the screen.

For this pattern to work, the base `Dialog` class must work with
abstract buttons: a base class or an interface that all concrete buttons
follow. This way the code within `Dialog` remains functional, whichever
type of buttons it works with.

Of course, you can apply this approach to other UI elements as well.
However, with each new factory method you add to the `Dialog`, you get
closer to the [Abstract Factory](/design-patterns/abstract-factory)
pattern. Fear not, we'll talk about this pattern later.

<figure class="code">
<pre class="code" lang="pseudocode"><code>// The creator class declares the factory method that must
// return an object of a product class. The creator&#39;s subclasses
// usually provide the implementation of this method.
class Dialog is
    // The creator may also provide some default implementation
    // of the factory method.
    abstract method createButton():Button

    // Note that, despite its name, the creator&#39;s primary
    // responsibility isn&#39;t creating products. It usually
    // contains some core business logic that relies on product
    // objects returned by the factory method. Subclasses can
    // indirectly change that business logic by overriding the
    // factory method and returning a different type of product
    // from it.
    method render() is
        // Call the factory method to create a product object.
        Button okButton = createButton()
        // Now use the product.
        okButton.onClick(closeDialog)
        okButton.render()


// Concrete creators override the factory method to change the
// resulting product&#39;s type.
class WindowsDialog extends Dialog is
    method createButton():Button is
        return new WindowsButton()

class WebDialog extends Dialog is
    method createButton():Button is
        return new HTMLButton()


// The product interface declares the operations that all
// concrete products must implement.
interface Button is
    method render()
    method onClick(f)

// Concrete products provide various implementations of the
// product interface.
class WindowsButton implements Button is
    method render(a, b) is
        // Render a button in Windows style.
    method onClick(f) is
        // Bind a native OS click event.

class HTMLButton implements Button is
    method render(a, b) is
        // Return an HTML representation of a button.
    method onClick(f) is
        // Bind a web browser click event.


class Application is
    field dialog: Dialog

    // The application picks a creator&#39;s type depending on the
    // current configuration or environment settings.
    method initialize() is
        config = readApplicationConfigFile()

        if (config.OS == &quot;Windows&quot;) then
            dialog = new WindowsDialog()
        else if (config.OS == &quot;Web&quot;) then
            dialog = new WebDialog()
        else
            throw new Exception(&quot;Error! Unknown operating system.&quot;)

    // The client code works with an instance of a concrete
    // creator, albeit through its base interface. As long as
    // the client keeps working with the creator via the base
    // interface, you can pass it any creator&#39;s subclass.
    method main() is
        this.initialize()
        dialog.render()</code></pre>
</figure>



##  Applicability



Use the Factory Method when you don't know beforehand the exact types
and dependencies of the objects your code should work with.



The Factory Method separates product construction code from the code
that actually uses the product. Therefore it's easier to extend the
product construction code independently from the rest of the code.

For example, to add a new product type to the app, you'll only need to
create a new creator subclass and override the factory method in it.



Use the Factory Method when you want to provide users of your library or
framework with a way to extend its internal components.



Inheritance is probably the easiest way to extend the default behavior
of a library or framework. But how would the framework recognize that
your subclass should be used instead of a standard component?

The solution is to reduce the code that constructs components across the
framework into a single factory method and let anyone override this
method in addition to extending the component itself.

Let's see how that would work. Imagine that you write an app using an
open source UI framework. Your app should have round buttons, but the
framework only provides square ones. You extend the standard `Button`
class with a glorious `RoundButton` subclass. But now you need to tell
the main `UIFramework` class to use the new button subclass instead of a
default one.

To achieve this, you create a subclass `UIWithRoundButtons` from a base
framework class and override its `createButton` method. While this
method returns `Button` objects in the base class, you make your
subclass return `RoundButton` objects. Now use the `UIWithRoundButtons`
class instead of `UIFramework`. And that's about it!



Use the Factory Method when you want to save system resources by reusing
existing objects instead of rebuilding them each time.



You often experience this need when dealing with large,
resource-intensive objects such as database connections, file systems,
and network resources.

Let's think about what has to be done to reuse an existing object:

1.  First, you need to create some storage to keep track of all of the
    created objects.
2.  When someone requests an object, the program should look for a free
    object inside that pool.
3.  ... and then return it to the client code.
4.  If there are no free objects, the program should create a new one
    (and add it to the pool).

That's a lot of code! And it must all be put into a single place so that
you don't pollute the program with duplicate code.

Probably the most obvious and convenient place where this code could be
placed is the constructor of the class whose objects we're trying to
reuse. However, a constructor must always return **new objects** by
definition. It can't return existing instances.

Therefore, you need to have a regular method capable of creating new
objects as well as reusing existing ones. That sounds very much like a
factory method.





##  How to Implement {#checklist}

1.  Make all products follow the same interface. This interface should
    declare methods that make sense in every product.

2.  Add an empty factory method inside the creator class. The return
    type of the method should match the common product interface.

3.  In the creator's code find all references to product constructors.
    One by one, replace them with calls to the factory method, while
    extracting the product creation code into the factory method.

    You might need to add a temporary parameter to the factory method to
    control the type of returned product.

    At this point, the code of the factory method may look pretty ugly.
    It may have a large `switch` statement that picks which product
    class to instantiate. But don't worry, we'll fix it soon enough.

4.  Now, create a set of creator subclasses for each type of product
    listed in the factory method. Override the factory method in the
    subclasses and extract the appropriate bits of construction code
    from the base method.

5.  If there are too many product types and it doesn't make sense to
    create subclasses for all of them, you can reuse the control
    parameter from the base class in subclasses.

    For instance, imagine that you have the following hierarchy of
    classes: the base `Mail` class with a couple of subclasses:
    `AirMail` and `GroundMail`; the `Transport` classes are `Plane`,
    `Truck` and `Train`. While the `AirMail` class only uses `Plane`
    objects, `GroundMail` may work with both `Truck` and `Train`
    objects. You can create a new subclass (say `TrainMail`) to handle
    both cases, but there's another option. The client code can pass an
    argument to the factory method of the `GroundMail` class to control
    which product it wants to receive.

6.  If, after all of the extractions, the base factory method has become
    empty, you can make it abstract. If there's something left, you can
    make it a default behavior of the method.



##  Pros and Cons {#pros-cons}



-    You avoid tight coupling between the creator and the concrete
    products.
-    *Single Responsibility Principle*. You can move the product
    creation code into one place in the program, making the code easier
    to support.
-    *Open/Closed Principle*. You can introduce new types of products
    into the program without breaking existing client code.



-    The code may become more complicated since you need to introduce a
    lot of new subclasses to implement the pattern. The best case
    scenario is when you're introducing the pattern into an existing
    hierarchy of creator classes.





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

-   You can use [Factory Method](/design-patterns/factory-method) along
    with [Iterator](/design-patterns/iterator) to let collection
    subclasses return different types of iterators that are compatible
    with the collections.

-   [Prototype](/design-patterns/prototype) isn't based on inheritance,
    so it doesn't have its drawbacks. On the other hand, *Prototype*
    requires a complicated initialization of the cloned object. [Factory
    Method](/design-patterns/factory-method) is based on inheritance but
    doesn't require an initialization step.

-   [Factory Method](/design-patterns/factory-method) is a
    specialization of [Template
    Method](/design-patterns/template-method). At the same time, a
    *Factory Method* may serve as a step in a large *Template Method*.



##  Code Examples {#implementations}

[![Factory Method in
C#](/images/patterns/icons/csharp.svg?id=da64592defc6e86d57c39c66e9de3e58){width="53"
height="53"
loading="lazy"}](/design-patterns/factory-method/csharp/example "Factory Method in C#"){.prog-lang-link}
[![Factory Method in
C++](/images/patterns/icons/cpp.svg?id=f7782ed8b8666246bfcc3f8fefc3b858){width="53"
height="53"
loading="lazy"}](/design-patterns/factory-method/cpp/example "Factory Method in C++"){.prog-lang-link}
[![Factory Method in
Go](/images/patterns/icons/go.svg?id=1a89927eb99b1ea3fde7701d97970aca){width="53"
height="53"
loading="lazy"}](/design-patterns/factory-method/go/example "Factory Method in Go"){.prog-lang-link}
[![Factory Method in
Java](/images/patterns/icons/java.svg?id=e6d87e2dca08c953fe3acd1275ed4f4e){width="53"
height="53"
loading="lazy"}](/design-patterns/factory-method/java/example "Factory Method in Java"){.prog-lang-link}
[![Factory Method in
PHP](/images/patterns/icons/php.svg?id=be1906eb26b71ec1d3b93720d6156618){width="53"
height="53"
loading="lazy"}](/design-patterns/factory-method/php/example "Factory Method in PHP"){.prog-lang-link}
[![Factory Method in
Python](/images/patterns/icons/python.svg?id=6d815d43c0f7050a1151b43e51569c9f){width="53"
height="53"
loading="lazy"}](/design-patterns/factory-method/python/example "Factory Method in Python"){.prog-lang-link}
[![Factory Method in
Ruby](/images/patterns/icons/ruby.svg?id=b065b718c914bf8e960ef731600be1eb){width="53"
height="53"
loading="lazy"}](/design-patterns/factory-method/ruby/example "Factory Method in Ruby"){.prog-lang-link}
[![Factory Method in
Rust](/images/patterns/icons/rust.svg?id=1f5698a4b5ae23fe79413511747e4a87){width="53"
height="53"
loading="lazy"}](/design-patterns/factory-method/rust/example "Factory Method in Rust"){.prog-lang-link}
[![Factory Method in
Swift](/images/patterns/icons/swift.svg?id=0b716c2d52ec3a48fbe91ac031070c1d){width="53"
height="53"
loading="lazy"}](/design-patterns/factory-method/swift/example "Factory Method in Swift"){.prog-lang-link}
[![Factory Method in
TypeScript](/images/patterns/icons/typescript.svg?id=2239d0f16cb703540c205dd8cb0c0cb7){width="53"
height="53"
loading="lazy"}](/design-patterns/factory-method/typescript/example "Factory Method in TypeScript"){.prog-lang-link}



##  Extra Content {#extras}

-   Read our [Factory Comparison](/design-patterns/factory-comparison)
    if you can't figure out the difference between various factory
    patterns and concepts.





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

[Abstract Factory []{.fa
.fa-arrow-right}](/design-patterns/abstract-factory){.btn .btn-primary
rel="next"}



#### Return

[[]{.fa .fa-arrow-left} Creational
Patterns](/design-patterns/creational-patterns){.btn .btn-default
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

    
    [English](https://refactoring.guru/design-patterns/factory-method "English"){.dropdown-item
    .locale-link .active locale="en"}
    [Español](https://refactoring.guru/es/design-patterns/factory-method "Español"){.dropdown-item
    .locale-link locale="es"}
    [Français](https://refactoring.guru/fr/design-patterns/factory-method "Français"){.dropdown-item
    .locale-link locale="fr"}
    [日本語](https://refactoring.guru/ja/design-patterns/factory-method "日本語"){.dropdown-item
    .locale-link locale="ja"}
    [한국어](https://refactoring.guru/ko/design-patterns/factory-method "한국어"){.dropdown-item
    .locale-link locale="ko"}
    [Polski](https://refactoring.guru/pl/design-patterns/factory-method "Polski"){.dropdown-item
    .locale-link locale="pl"} [Português
    Brasileiro](https://refactoring.guru/pt-br/design-patterns/factory-method "Português Brasileiro"){.dropdown-item
    .locale-link locale="pt-br"}
    [Русский](https://refactoring.guru/ru/design-patterns/factory-method "Русский"){.dropdown-item
    .locale-link locale="ru"}
    [Українська](https://refactoring.guru/uk/design-patterns/factory-method "Українська"){.dropdown-item
    .locale-link locale="uk"}
    [中文](https://refactoringguru.cn/design-patterns/factory-method "中文"){.dropdown-item
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






