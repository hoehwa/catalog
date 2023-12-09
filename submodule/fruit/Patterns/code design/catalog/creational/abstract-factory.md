



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


# Abstract Factory {#abstract-factory .title}


##  Intent

**Abstract Factory** is a creational design pattern that lets you
produce families of related objects without specifying their
concrete classes.

<figure class="image">
<img
src="/images/patterns/content/abstract-factory/abstract-factory-en.png?id=d0210ee255712a245fead94a3fafabe0"
srcset="/images/patterns/content/abstract-factory/abstract-factory-en-2x.png?id=a488ca862db731876fa0513bb2105640 2x"
width="640" alt="Abstract Factory pattern" />
</figure>



##  Problem

Imagine that you're creating a furniture shop simulator. Your code
consists of classes that represent:

1.  A family of related products, say: `Chair` + `Sofa` + `CoffeeTable`.

2.  Several variants of this family. For example, products `Chair` +
    `Sofa` + `CoffeeTable` are available in these variants: `Modern`,
    `Victorian`, `ArtDeco`.

<figure class="image">
<img
src="/images/patterns/diagrams/abstract-factory/problem-en.png?id=e38c307511e684828be898de02d6c268"
srcset="/images/patterns/diagrams/abstract-factory/problem-en-2x.png?id=7de667bc24583c3ac03ccb80f3613cfe 2x"
loading="lazy" width="420" alt="Product families and their variants." />
<figcaption><p>Product families and their variants.</p></figcaption>
</figure>

You need a way to create individual furniture objects so that they match
other objects of the same family. Customers get quite mad when they
receive non-matching furniture.

<figure class="image">
<img
src="/images/patterns/content/abstract-factory/abstract-factory-comic-1-en.png?id=f4012920c5034122eedbb0c9fec0cdb3"
srcset="/images/patterns/content/abstract-factory/abstract-factory-comic-1-en-2x.png?id=e2d4e7bbdd41899a3a85ebefa88bca3e 2x"
loading="lazy" width="600" />
<figcaption><p>A Modern-style sofa doesn’t match
Victorian-style chairs.</p></figcaption>
</figure>

Also, you don't want to change existing code when adding new products or
families of products to the program. Furniture vendors update their
catalogs very often, and you wouldn't want to change the core code each
time it happens.



##  Solution

The first thing the Abstract Factory pattern suggests is to explicitly
declare interfaces for each distinct product of the product family
(e.g., chair, sofa or coffee table). Then you can make all variants of
products follow those interfaces. For example, all chair variants can
implement the `Chair` interface; all coffee table variants can implement
the `CoffeeTable` interface, and so on.

<figure class="image">
<img
src="/images/patterns/diagrams/abstract-factory/solution1.png?id=71f2018d8bb443b9cce90d57110675e3"
srcset="/images/patterns/diagrams/abstract-factory/solution1-2x.png?id=eacec286153e058db9255d26541c0529 2x"
loading="lazy" width="420" alt="The Chairs class hierarchy" />
<figcaption><p>All variants of the same object must be moved to a single
class hierarchy.</p></figcaption>
</figure>

The next move is to declare the *Abstract Factory*---an interface with a
list of creation methods for all products that are part of the product
family (for example, `createChair`, `createSofa` and
`createCoffeeTable`). These methods must return **abstract** product
types represented by the interfaces we extracted previously: `Chair`,
`Sofa`, `CoffeeTable` and so on.

<figure class="image">
<img
src="/images/patterns/diagrams/abstract-factory/solution2.png?id=53975d6e4714c6f942633a879f7ac571"
srcset="/images/patterns/diagrams/abstract-factory/solution2-2x.png?id=b21557081f75ac7b4110427e89a10378 2x"
loading="lazy" width="640" alt="The _Factories_ class hierarchy" />
<figcaption><p>Each concrete factory corresponds to a specific
product variant.</p></figcaption>
</figure>

Now, how about the product variants? For each variant of a product
family, we create a separate factory class based on the
`AbstractFactory` interface. A factory is a class that returns products
of a particular kind. For example, the `ModernFurnitureFactory` can only
create `ModernChair`, `ModernSofa` and `ModernCoffeeTable` objects.

The client code has to work with both factories and products via their
respective abstract interfaces. This lets you change the type of a
factory that you pass to the client code, as well as the product variant
that the client code receives, without breaking the actual client code.

<figure class="image">
<img
src="/images/patterns/content/abstract-factory/abstract-factory-comic-2-en.png?id=fbce1a263acfefc76074fd20fae7b8c3"
srcset="/images/patterns/content/abstract-factory/abstract-factory-comic-2-en-2x.png?id=824023e4cfdc6f4d2457e6dc3e51ccfb 2x"
loading="lazy" width="600" />
<figcaption><p>The client shouldn’t care about the concrete class of the
factory it works with.</p></figcaption>
</figure>

Say the client wants a factory to produce a chair. The client doesn't
have to be aware of the factory's class, nor does it matter what kind of
chair it gets. Whether it's a Modern model or a Victorian-style chair,
the client must treat all chairs in the same manner, using the abstract
`Chair` interface. With this approach, the only thing that the client
knows about the chair is that it implements the `sitOn` method in some
way. Also, whichever variant of the chair is returned, it'll always
match the type of sofa or coffee table produced by the same factory
object.

There's one more thing left to clarify: if the client is only exposed to
the abstract interfaces, what creates the actual factory objects?
Usually, the application creates a concrete factory object at the
initialization stage. Just before that, the app must select the factory
type depending on the configuration or the environment settings.



##  Structure



<figure class="image">
<img
src="/images/patterns/diagrams/abstract-factory/structure.png?id=a3112cdd98765406af94595a3c5e7762"
class="structure-img-non-indexed d-none d-xl-block"
srcset="/images/patterns/diagrams/abstract-factory/structure-2x.png?id=c4d3634ec2e74e02a0fe1a83ce9b50f6 2x"
loading="lazy" width="720" alt="Abstract Factory design pattern" /><img
src="/images/patterns/diagrams/abstract-factory/structure-indexed.png?id=6ae1c99cbd90cf58753c633624fb1a04"
class="structure-img-indexed d-xl-none"
srcset="/images/patterns/diagrams/abstract-factory/structure-indexed-2x.png?id=cb6d4e1e89826c42966dc7097374f889 2x"
loading="lazy" width="700" alt="Abstract Factory design pattern" />
</figure>


1.  **Abstract Products** declare interfaces for a set of distinct but
    related products which make up a product family.

2.  **Concrete Products** are various implementations of abstract
    products, grouped by variants. Each abstract product (chair/sofa)
    must be implemented in all given variants (Victorian/Modern).

3.  The **Abstract Factory** interface declares a set of methods for
    creating each of the abstract products.

4.  **Concrete Factories** implement creation methods of the abstract
    factory. Each concrete factory corresponds to a specific variant of
    products and creates only those product variants.

5.  Although concrete factories instantiate concrete products,
    signatures of their creation methods must return corresponding
    *abstract* products. This way the client code that uses a factory
    doesn't get coupled to the specific variant of the product it gets
    from a factory. The **Client** can work with any concrete
    factory/product variant, as long as it communicates with their
    objects via abstract interfaces.




##  Pseudocode

This example illustrates how the **Abstract Factory** pattern can be
used for creating cross-platform UI elements without coupling the client
code to concrete UI classes, while keeping all created elements
consistent with a selected operating system.

<figure class="image">
<img
src="/images/patterns/diagrams/abstract-factory/example.png?id=5928a61d18bf00b047463471c599100a"
srcset="/images/patterns/diagrams/abstract-factory/example-2x.png?id=eb5127b1d6486f6fad73be2d5e444449 2x"
loading="lazy" width="640"
alt="The class diagram for the Abstract Factory pattern example" />
<figcaption><p>The cross-platform UI classes example.</p></figcaption>
</figure>

The same UI elements in a cross-platform application are expected to
behave similarly, but look a little bit different under different
operating systems. Moreover, it's your job to make sure that the UI
elements match the style of the current operating system. You wouldn't
want your program to render macOS controls when it's executed in
Windows.

The Abstract Factory interface declares a set of creation methods that
the client code can use to produce different types of UI elements.
Concrete factories correspond to specific operating systems and create
the UI elements that match that particular OS.

It works like this: when an application launches, it checks the type of
the current operating system. The app uses this information to create a
factory object from a class that matches the operating system. The rest
of the code uses this factory to create UI elements. This prevents the
wrong elements from being created.

With this approach, the client code doesn't depend on concrete classes
of factories and UI elements as long as it works with these objects via
their abstract interfaces. This also lets the client code support other
factories or UI elements that you might add in the future.

As a result, you don't need to modify the client code each time you add
a new variation of UI elements to your app. You just have to create a
new factory class that produces these elements and slightly modify the
app's initialization code so it selects that class when appropriate.

<figure class="code">
<pre class="code" lang="pseudocode"><code>// The abstract factory interface declares a set of methods that
// return different abstract products. These products are called
// a family and are related by a high-level theme or concept.
// Products of one family are usually able to collaborate among
// themselves. A family of products may have several variants,
// but the products of one variant are incompatible with the
// products of another variant.
interface GUIFactory is
    method createButton():Button
    method createCheckbox():Checkbox


// Concrete factories produce a family of products that belong
// to a single variant. The factory guarantees that the
// resulting products are compatible. Signatures of the concrete
// factory&#39;s methods return an abstract product, while inside
// the method a concrete product is instantiated.
class WinFactory implements GUIFactory is
    method createButton():Button is
        return new WinButton()
    method createCheckbox():Checkbox is
        return new WinCheckbox()

// Each concrete factory has a corresponding product variant.
class MacFactory implements GUIFactory is
    method createButton():Button is
        return new MacButton()
    method createCheckbox():Checkbox is
        return new MacCheckbox()


// Each distinct product of a product family should have a base
// interface. All variants of the product must implement this
// interface.
interface Button is
    method paint()

// Concrete products are created by corresponding concrete
// factories.
class WinButton implements Button is
    method paint() is
        // Render a button in Windows style.

class MacButton implements Button is
    method paint() is
        // Render a button in macOS style.

// Here&#39;s the base interface of another product. All products
// can interact with each other, but proper interaction is
// possible only between products of the same concrete variant.
interface Checkbox is
    method paint()

class WinCheckbox implements Checkbox is
    method paint() is
        // Render a checkbox in Windows style.

class MacCheckbox implements Checkbox is
    method paint() is
        // Render a checkbox in macOS style.


// The client code works with factories and products only
// through abstract types: GUIFactory, Button and Checkbox. This
// lets you pass any factory or product subclass to the client
// code without breaking it.
class Application is
    private field factory: GUIFactory
    private field button: Button
    constructor Application(factory: GUIFactory) is
        this.factory = factory
    method createUI() is
        this.button = factory.createButton()
    method paint() is
        button.paint()


// The application picks the factory type depending on the
// current configuration or environment settings and creates it
// at runtime (usually at the initialization stage).
class ApplicationConfigurator is
    method main() is
        config = readApplicationConfigFile()

        if (config.OS == &quot;Windows&quot;) then
            factory = new WinFactory()
        else if (config.OS == &quot;Mac&quot;) then
            factory = new MacFactory()
        else
            throw new Exception(&quot;Error! Unknown operating system.&quot;)

        Application app = new Application(factory)</code></pre>
</figure>



##  Applicability



Use the Abstract Factory when your code needs to work with various
families of related products, but you don't want it to depend on the
concrete classes of those products---they might be unknown beforehand or
you simply want to allow for future extensibility.



The Abstract Factory provides you with an interface for creating objects
from each class of the product family. As long as your code creates
objects via this interface, you don't have to worry about creating the
wrong variant of a product which doesn't match the products already
created by your app.



Consider implementing the Abstract Factory when you have a class with a
set of [Factory Methods](/design-patterns/factory-method) that blur its
primary responsibility.



In a well-designed program *each class is responsible only for one
thing*. When a class deals with multiple product types, it may be worth
extracting its factory methods into a stand-alone factory class or a
full-blown Abstract Factory implementation.





##  How to Implement {#checklist}

1.  Map out a matrix of distinct product types versus variants of these
    products.

2.  Declare abstract product interfaces for all product types. Then make
    all concrete product classes implement these interfaces.

3.  Declare the abstract factory interface with a set of creation
    methods for all abstract products.

4.  Implement a set of concrete factory classes, one for each product
    variant.

5.  Create factory initialization code somewhere in the app. It should
    instantiate one of the concrete factory classes, depending on the
    application configuration or the current environment. Pass this
    factory object to all classes that construct products.

6.  Scan through the code and find all direct calls to product
    constructors. Replace them with calls to the appropriate creation
    method on the factory object.



##  Pros and Cons {#pros-cons}



-    You can be sure that the products you're getting from a factory are
    compatible with each other.
-    You avoid tight coupling between concrete products and client code.
-    *Single Responsibility Principle*. You can extract the product
    creation code into one place, making the code easier to support.
-    *Open/Closed Principle*. You can introduce new variants of products
    without breaking existing client code.



-    The code may become more complicated than it should be, since a lot
    of new interfaces and classes are introduced along with the pattern.





##  Relations with Other Patterns {#relations}

-   Many designs start by using [Factory
    Method](/design-patterns/factory-method) (less complicated and more
    customizable via subclasses) and evolve toward [Abstract
    Factory](/design-patterns/abstract-factory),
    [Prototype](/design-patterns/prototype), or
    [Builder](/design-patterns/builder) (more flexible, but more
    complicated).

-   [Builder](/design-patterns/builder) focuses on constructing complex
    objects step by step. [Abstract
    Factory](/design-patterns/abstract-factory) specializes in creating
    families of related objects. *Abstract Factory* returns the product
    immediately, whereas *Builder* lets you run some additional
    construction steps before fetching the product.

-   [Abstract Factory](/design-patterns/abstract-factory) classes are
    often based on a set of [Factory
    Methods](/design-patterns/factory-method), but you can also use
    [Prototype](/design-patterns/prototype) to compose the methods on
    these classes.

-   [Abstract Factory](/design-patterns/abstract-factory) can serve as
    an alternative to [Facade](/design-patterns/facade) when you only
    want to hide the way the subsystem objects are created from the
    client code.

-   You can use [Abstract Factory](/design-patterns/abstract-factory)
    along with [Bridge](/design-patterns/bridge). This pairing is useful
    when some abstractions defined by *Bridge* can only work with
    specific implementations. In this case, *Abstract Factory* can
    encapsulate these relations and hide the complexity from the client
    code.

-   [Abstract Factories](/design-patterns/abstract-factory),
    [Builders](/design-patterns/builder) and
    [Prototypes](/design-patterns/prototype) can all be implemented as
    [Singletons](/design-patterns/singleton).



##  Code Examples {#implementations}

[![Abstract Factory in
C#](/images/patterns/icons/csharp.svg?id=da64592defc6e86d57c39c66e9de3e58){width="53"
height="53"
loading="lazy"}](/design-patterns/abstract-factory/csharp/example "Abstract Factory in C#"){.prog-lang-link}
[![Abstract Factory in
C++](/images/patterns/icons/cpp.svg?id=f7782ed8b8666246bfcc3f8fefc3b858){width="53"
height="53"
loading="lazy"}](/design-patterns/abstract-factory/cpp/example "Abstract Factory in C++"){.prog-lang-link}
[![Abstract Factory in
Go](/images/patterns/icons/go.svg?id=1a89927eb99b1ea3fde7701d97970aca){width="53"
height="53"
loading="lazy"}](/design-patterns/abstract-factory/go/example "Abstract Factory in Go"){.prog-lang-link}
[![Abstract Factory in
Java](/images/patterns/icons/java.svg?id=e6d87e2dca08c953fe3acd1275ed4f4e){width="53"
height="53"
loading="lazy"}](/design-patterns/abstract-factory/java/example "Abstract Factory in Java"){.prog-lang-link}
[![Abstract Factory in
PHP](/images/patterns/icons/php.svg?id=be1906eb26b71ec1d3b93720d6156618){width="53"
height="53"
loading="lazy"}](/design-patterns/abstract-factory/php/example "Abstract Factory in PHP"){.prog-lang-link}
[![Abstract Factory in
Python](/images/patterns/icons/python.svg?id=6d815d43c0f7050a1151b43e51569c9f){width="53"
height="53"
loading="lazy"}](/design-patterns/abstract-factory/python/example "Abstract Factory in Python"){.prog-lang-link}
[![Abstract Factory in
Ruby](/images/patterns/icons/ruby.svg?id=b065b718c914bf8e960ef731600be1eb){width="53"
height="53"
loading="lazy"}](/design-patterns/abstract-factory/ruby/example "Abstract Factory in Ruby"){.prog-lang-link}
[![Abstract Factory in
Rust](/images/patterns/icons/rust.svg?id=1f5698a4b5ae23fe79413511747e4a87){width="53"
height="53"
loading="lazy"}](/design-patterns/abstract-factory/rust/example "Abstract Factory in Rust"){.prog-lang-link}
[![Abstract Factory in
Swift](/images/patterns/icons/swift.svg?id=0b716c2d52ec3a48fbe91ac031070c1d){width="53"
height="53"
loading="lazy"}](/design-patterns/abstract-factory/swift/example "Abstract Factory in Swift"){.prog-lang-link}
[![Abstract Factory in
TypeScript](/images/patterns/icons/typescript.svg?id=2239d0f16cb703540c205dd8cb0c0cb7){width="53"
height="53"
loading="lazy"}](/design-patterns/abstract-factory/typescript/example "Abstract Factory in TypeScript"){.prog-lang-link}



##  Extra Content {#extras}

-   Read our [Factory Comparison](/design-patterns/factory-comparison)
    to learn more about the differences between various factory patterns
    and concepts.





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

[Factory Comparison []{.fa
.fa-arrow-right}](/design-patterns/factory-comparison){.btn .btn-primary
rel="next"}



#### Return

[[]{.fa .fa-arrow-left} Factory
Method](/design-patterns/factory-method){.btn .btn-default rel="prev"}







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

    
    [English](https://refactoring.guru/design-patterns/abstract-factory "English"){.dropdown-item
    .locale-link .active locale="en"}
    [Español](https://refactoring.guru/es/design-patterns/abstract-factory "Español"){.dropdown-item
    .locale-link locale="es"}
    [Français](https://refactoring.guru/fr/design-patterns/abstract-factory "Français"){.dropdown-item
    .locale-link locale="fr"}
    [日本語](https://refactoring.guru/ja/design-patterns/abstract-factory "日本語"){.dropdown-item
    .locale-link locale="ja"}
    [한국어](https://refactoring.guru/ko/design-patterns/abstract-factory "한국어"){.dropdown-item
    .locale-link locale="ko"}
    [Polski](https://refactoring.guru/pl/design-patterns/abstract-factory "Polski"){.dropdown-item
    .locale-link locale="pl"} [Português
    Brasileiro](https://refactoring.guru/pt-br/design-patterns/abstract-factory "Português Brasileiro"){.dropdown-item
    .locale-link locale="pt-br"}
    [Русский](https://refactoring.guru/ru/design-patterns/abstract-factory "Русский"){.dropdown-item
    .locale-link locale="ru"}
    [Українська](https://refactoring.guru/uk/design-patterns/abstract-factory "Українська"){.dropdown-item
    .locale-link locale="uk"}
    [中文](https://refactoringguru.cn/design-patterns/abstract-factory "中文"){.dropdown-item
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






