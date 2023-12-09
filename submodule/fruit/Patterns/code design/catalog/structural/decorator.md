



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








[](/){.home} / [Design Patterns](/design-patterns){.type} / [Structural
Patterns](/design-patterns/structural-patterns){.type}


# Decorator {#decorator .title}


Also known as: [Wrapper]{style="display:inline-block"}



##  Intent

**Decorator** is a structural design pattern that lets you attach new
behaviors to objects by placing these objects inside special wrapper
objects that contain the behaviors.

<figure class="image">
<img
src="/images/patterns/content/decorator/decorator.png?id=710c66670c7123e0928d3b3758aea79e"
srcset="/images/patterns/content/decorator/decorator-2x.png?id=736ab07b1d8920ab2c7a70c9cb1305cc 2x"
width="640" alt="Decorator design pattern" />
</figure>



##  Problem

Imagine that you're working on a notification library which lets other
programs notify their users about important events.

The initial version of the library was based on the `Notifier` class
that had only a few fields, a constructor and a single `send` method.
The method could accept a message argument from a client and send the
message to a list of emails that were passed to the notifier via its
constructor. A third-party app which acted as a client was supposed to
create and configure the notifier object once, and then use it each time
something important happened.

<figure class="image">
<img
src="/images/patterns/diagrams/decorator/problem1-en.png?id=7658efddaaf43acb64ac63a92025cc1e"
srcset="/images/patterns/diagrams/decorator/problem1-en-2x.png?id=0bf0496ca959de8698bee735e4e62aac 2x"
loading="lazy" width="540"
alt="Structure of the library before applying the Decorator pattern" />
<figcaption><p>A program could use the notifier class to send
notifications about important events to a predefined set
of emails.</p></figcaption>
</figure>

At some point, you realize that users of the library expect more than
just email notifications. Many of them would like to receive an SMS
about critical issues. Others would like to be notified on Facebook and,
of course, the corporate users would love to get Slack notifications.

<figure class="image">
<img
src="/images/patterns/diagrams/decorator/problem2.png?id=ba5d5e106ea8c4848d60e230feca9135"
srcset="/images/patterns/diagrams/decorator/problem2-2x.png?id=28b2c8509b4e78c031d728424b876ebc 2x"
loading="lazy" width="440"
alt="Structure of the library after implementing other notification types" />
<figcaption><p>Each notification type is implemented as a
notifier’s subclass.</p></figcaption>
</figure>

How hard can that be? You extended the `Notifier` class and put the
additional notification methods into new subclasses. Now the client was
supposed to instantiate the desired notification class and use it for
all further notifications.

But then someone reasonably asked you, "Why can't you use several
notification types at once? If your house is on fire, you'd probably
want to be informed through every channel."

You tried to address that problem by creating special subclasses which
combined several notification methods within one class. However, it
quickly became apparent that this approach would bloat the code
immensely, not only the library code but the client code as well.

<figure class="image">
<img
src="/images/patterns/diagrams/decorator/problem3.png?id=f3b3e7a107d870871f2c3167adcb7ccb"
srcset="/images/patterns/diagrams/decorator/problem3-2x.png?id=abb7a87b521ce97d7661dd9c0b988cc3 2x"
loading="lazy" width="630"
alt="Structure of the library after creating class combinations" />
<figcaption><p>Combinatorial explosion of subclasses.</p></figcaption>
</figure>

You have to find some other way to structure notifications classes so
that their number won't accidentally break some Guinness record.



##  Solution

Extending a class is the first thing that comes to mind when you need to
alter an object's behavior. However, inheritance has several serious
caveats that you need to be aware of.

-   Inheritance is static. You can't alter the behavior of an existing
    object at runtime. You can only replace the whole object with
    another one that's created from a different subclass.
-   Subclasses can have just one parent class. In most languages,
    inheritance doesn't let a class inherit behaviors of multiple
    classes at the same time.

One of the ways to overcome these caveats is by using *Aggregation* or
*Composition* []{.pop-i}[*Aggregation*: object A contains objects B; B
can live without A.\
*Composition*: object A consists of objects B; A manages life cycle of
B; B can't live without A.]{.pop-content} instead of *Inheritance*. Both
of the alternatives work almost the same way: one object *has a*
reference to another and delegates it some work, whereas with
inheritance, the object itself *is* able to do that work, inheriting the
behavior from its superclass.

With this new approach you can easily substitute the linked "helper"
object with another, changing the behavior of the container at runtime.
An object can use the behavior of various classes, having references to
multiple objects and delegating them all kinds of work.
Aggregation/composition is the key principle behind many design
patterns, including Decorator. On that note, let's return to the pattern
discussion.

<figure class="image">
<img
src="/images/patterns/diagrams/decorator/solution1-en.png?id=468e68f1e9ae21649d63dd454500741d"
srcset="/images/patterns/diagrams/decorator/solution1-en-2x.png?id=0acaa7d75290a1647f5402bc5d1c03e7 2x"
loading="lazy" width="550" alt="Inheritance vs. Aggregation" />
<figcaption><p>Inheritance vs. Aggregation</p></figcaption>
</figure>

"Wrapper" is the alternative nickname for the Decorator pattern that
clearly expresses the main idea of the pattern. A *wrapper* is an object
that can be linked with some *target* object. The wrapper contains the
same set of methods as the target and delegates to it all requests it
receives. However, the wrapper may alter the result by doing something
either before or after it passes the request to the target.

When does a simple wrapper become the real decorator? As I mentioned,
the wrapper implements the same interface as the wrapped object. That's
why from the client's perspective these objects are identical. Make the
wrapper's reference field accept any object that follows that interface.
This will let you cover an object in multiple wrappers, adding the
combined behavior of all the wrappers to it.

In our notifications example, let's leave the simple email notification
behavior inside the base `Notifier` class, but turn all other
notification methods into decorators.

<figure class="image">
<img
src="/images/patterns/diagrams/decorator/solution2.png?id=cbee4a27080ce3a0bf773482613e1347"
srcset="/images/patterns/diagrams/decorator/solution2-2x.png?id=7775f76b94dbd5cd25f711ce81f59262 2x"
loading="lazy" width="640"
alt="The solution with the Decorator pattern" />
<figcaption><p>Various notification methods
become decorators.</p></figcaption>
</figure>

The client code would need to wrap a basic notifier object into a set of
decorators that match the client's preferences. The resulting objects
will be structured as a stack.

<figure class="image">
<img
src="/images/patterns/diagrams/decorator/solution3-en.png?id=b7e2e2036435265350ba0c6796162ab5"
srcset="/images/patterns/diagrams/decorator/solution3-en-2x.png?id=9a4ef2b4267685a83d0233d78775497b 2x"
loading="lazy" width="300"
alt="Apps might configure complex stacks of notification decorators" />
<figcaption><p>Apps might configure complex stacks of
notification decorators.</p></figcaption>
</figure>

The last decorator in the stack would be the object that the client
actually works with. Since all decorators implement the same interface
as the base notifier, the rest of the client code won't care whether it
works with the "pure" notifier object or the decorated one.

We could apply the same approach to other behaviors such as formatting
messages or composing the recipient list. The client can decorate the
object with any custom decorators, as long as they follow the same
interface as the others.



##  Real-World Analogy {#analogy}

<figure class="image">
<img
src="/images/patterns/content/decorator/decorator-comic-1.png?id=80d95baacbfb91f5bcdbdc7814b0c64d"
srcset="/images/patterns/content/decorator/decorator-comic-1-2x.png?id=ba869f621b6e0ea173fdc2b535fc7eed 2x"
loading="lazy" width="600" alt="Example of the Decorator pattern" />
<figcaption><p>You get a combined effect from wearing multiple pieces
of clothing.</p></figcaption>
</figure>

Wearing clothes is an example of using decorators. When you're cold, you
wrap yourself in a sweater. If you're still cold with a sweater, you can
wear a jacket on top. If it's raining, you can put on a raincoat. All of
these garments "extend" your basic behavior but aren't part of you, and
you can easily take off any piece of clothing whenever you don't need
it.



##  Structure



<figure class="image">
<img
src="/images/patterns/diagrams/decorator/structure.png?id=8c95d894aecce5315cc1b12093a7ea0c"
class="structure-img-non-indexed d-none d-xl-block"
srcset="/images/patterns/diagrams/decorator/structure-2x.png?id=3cfa1f10417a4ef0c12580bc4a63b80d 2x"
loading="lazy" width="480"
alt="Structure of the Decorator design pattern" /><img
src="/images/patterns/diagrams/decorator/structure-indexed.png?id=09401b230a58f2249e4c9a1195d485a0"
class="structure-img-indexed d-xl-none"
srcset="/images/patterns/diagrams/decorator/structure-indexed-2x.png?id=2733e7d0e322bfb2f150ccf8a878dbf6 2x"
loading="lazy" width="500"
alt="Structure of the Decorator design pattern" />
</figure>


1.  The **Component** declares the common interface for both wrappers
    and wrapped objects.

2.  **Concrete Component** is a class of objects being wrapped. It
    defines the basic behavior, which can be altered by decorators.

3.  The **Base Decorator** class has a field for referencing a wrapped
    object. The field's type should be declared as the component
    interface so it can contain both concrete components and decorators.
    The base decorator delegates all operations to the wrapped object.

4.  **Concrete Decorators** define extra behaviors that can be added to
    components dynamically. Concrete decorators override methods of the
    base decorator and execute their behavior either before or after
    calling the parent method.

5.  The **Client** can wrap components in multiple layers of decorators,
    as long as it works with all objects via the component interface.




##  Pseudocode

In this example, the **Decorator** pattern lets you compress and encrypt
sensitive data independently from the code that actually uses this data.

<figure class="image">
<img
src="/images/patterns/diagrams/decorator/example.png?id=eec9dc488f00c85f50e764323baa723e"
srcset="/images/patterns/diagrams/decorator/example-2x.png?id=4891323a27d5601a174eec366187d833 2x"
loading="lazy" width="540"
alt="Structure of the Decorator pattern example" />
<figcaption><p>The encryption and compression
decorators example.</p></figcaption>
</figure>

The application wraps the data source object with a pair of decorators.
Both wrappers change the way the data is written to and read from the
disk:

-   Just before the data is **written to disk**, the decorators encrypt
    and compress it. The original class writes the encrypted and
    protected data to the file without knowing about the change.

-   Right after the data is **read from disk**, it goes through the same
    decorators, which decompress and decode it.

The decorators and the data source class implement the same interface,
which makes them all interchangeable in the client code.

<figure class="code">
<pre class="code" lang="pseudocode"><code>// The component interface defines operations that can be
// altered by decorators.
interface DataSource is
    method writeData(data)
    method readData():data

// Concrete components provide default implementations for the
// operations. There might be several variations of these
// classes in a program.
class FileDataSource implements DataSource is
    constructor FileDataSource(filename) { ... }

    method writeData(data) is
        // Write data to file.

    method readData():data is
        // Read data from file.

// The base decorator class follows the same interface as the
// other components. The primary purpose of this class is to
// define the wrapping interface for all concrete decorators.
// The default implementation of the wrapping code might include
// a field for storing a wrapped component and the means to
// initialize it.
class DataSourceDecorator implements DataSource is
    protected field wrappee: DataSource

    constructor DataSourceDecorator(source: DataSource) is
        wrappee = source

    // The base decorator simply delegates all work to the
    // wrapped component. Extra behaviors can be added in
    // concrete decorators.
    method writeData(data) is
        wrappee.writeData(data)

    // Concrete decorators may call the parent implementation of
    // the operation instead of calling the wrapped object
    // directly. This approach simplifies extension of decorator
    // classes.
    method readData():data is
        return wrappee.readData()

// Concrete decorators must call methods on the wrapped object,
// but may add something of their own to the result. Decorators
// can execute the added behavior either before or after the
// call to a wrapped object.
class EncryptionDecorator extends DataSourceDecorator is
    method writeData(data) is
        // 1. Encrypt passed data.
        // 2. Pass encrypted data to the wrappee&#39;s writeData
        // method.

    method readData():data is
        // 1. Get data from the wrappee&#39;s readData method.
        // 2. Try to decrypt it if it&#39;s encrypted.
        // 3. Return the result.

// You can wrap objects in several layers of decorators.
class CompressionDecorator extends DataSourceDecorator is
    method writeData(data) is
        // 1. Compress passed data.
        // 2. Pass compressed data to the wrappee&#39;s writeData
        // method.

    method readData():data is
        // 1. Get data from the wrappee&#39;s readData method.
        // 2. Try to decompress it if it&#39;s compressed.
        // 3. Return the result.


// Option 1. A simple example of a decorator assembly.
class Application is
    method dumbUsageExample() is
        source = new FileDataSource(&quot;somefile.dat&quot;)
        source.writeData(salaryRecords)
        // The target file has been written with plain data.

        source = new CompressionDecorator(source)
        source.writeData(salaryRecords)
        // The target file has been written with compressed
        // data.

        source = new EncryptionDecorator(source)
        // The source variable now contains this:
        // Encryption &gt; Compression &gt; FileDataSource
        source.writeData(salaryRecords)
        // The file has been written with compressed and
        // encrypted data.


// Option 2. Client code that uses an external data source.
// SalaryManager objects neither know nor care about data
// storage specifics. They work with a pre-configured data
// source received from the app configurator.
class SalaryManager is
    field source: DataSource

    constructor SalaryManager(source: DataSource) { ... }

    method load() is
        return source.readData()

    method save() is
        source.writeData(salaryRecords)
    // ...Other useful methods...


// The app can assemble different stacks of decorators at
// runtime, depending on the configuration or environment.
class ApplicationConfigurator is
    method configurationExample() is
        source = new FileDataSource(&quot;salary.dat&quot;)
        if (enabledEncryption)
            source = new EncryptionDecorator(source)
        if (enabledCompression)
            source = new CompressionDecorator(source)

        logger = new SalaryManager(source)
        salary = logger.load()
    // ...</code></pre>
</figure>



##  Applicability



Use the Decorator pattern when you need to be able to assign extra
behaviors to objects at runtime without breaking the code that uses
these objects.



The Decorator lets you structure your business logic into layers, create
a decorator for each layer and compose objects with various combinations
of this logic at runtime. The client code can treat all these objects in
the same way, since they all follow a common interface.



Use the pattern when it's awkward or not possible to extend an object's
behavior using inheritance.



Many programming languages have the `final` keyword that can be used to
prevent further extension of a class. For a final class, the only way to
reuse the existing behavior would be to wrap the class with your own
wrapper, using the Decorator pattern.





##  How to Implement {#checklist}

1.  Make sure your business domain can be represented as a primary
    component with multiple optional layers over it.

2.  Figure out what methods are common to both the primary component and
    the optional layers. Create a component interface and declare those
    methods there.

3.  Create a concrete component class and define the base behavior in
    it.

4.  Create a base decorator class. It should have a field for storing a
    reference to a wrapped object. The field should be declared with the
    component interface type to allow linking to concrete components as
    well as decorators. The base decorator must delegate all work to the
    wrapped object.

5.  Make sure all classes implement the component interface.

6.  Create concrete decorators by extending them from the base
    decorator. A concrete decorator must execute its behavior before or
    after the call to the parent method (which always delegates to the
    wrapped object).

7.  The client code must be responsible for creating decorators and
    composing them in the way the client needs.



##  Pros and Cons {#pros-cons}



-    You can extend an object's behavior without making a new subclass.
-    You can add or remove responsibilities from an object at runtime.
-    You can combine several behaviors by wrapping an object into
    multiple decorators.
-    *Single Responsibility Principle*. You can divide a monolithic
    class that implements many possible variants of behavior into
    several smaller classes.



-    It's hard to remove a specific wrapper from the wrappers stack.
-    It's hard to implement a decorator in such a way that its behavior
    doesn't depend on the order in the decorators stack.
-    The initial configuration code of layers might look pretty ugly.





##  Relations with Other Patterns {#relations}

-   [Adapter](/design-patterns/adapter) provides a completely different
    interface for accessing an existing object. On the other hand, with
    the [Decorator](/design-patterns/decorator) pattern the interface
    either stays the same or gets extended. In addition, *Decorator*
    supports recursive composition, which isn't possible when you use
    *Adapter*.

-   With [Adapter](/design-patterns/adapter) you access an existing
    object via different interface. With
    [Proxy](/design-patterns/proxy), the interface stays the same. With
    [Decorator](/design-patterns/decorator) you access the object via an
    enhanced interface.

-   [Chain of Responsibility](/design-patterns/chain-of-responsibility)
    and [Decorator](/design-patterns/decorator) have very similar class
    structures. Both patterns rely on recursive composition to pass the
    execution through a series of objects. However, there are several
    crucial differences.

    The *CoR* handlers can execute arbitrary operations independently of
    each other. They can also stop passing the request further at any
    point. On the other hand, various *Decorators* can extend the
    object's behavior while keeping it consistent with the base
    interface. In addition, decorators aren't allowed to break the flow
    of the request.

-   [Composite](/design-patterns/composite) and
    [Decorator](/design-patterns/decorator) have similar structure
    diagrams since both rely on recursive composition to organize an
    open-ended number of objects.

    A *Decorator* is like a *Composite* but only has one child
    component. There's another significant difference: *Decorator* adds
    additional responsibilities to the wrapped object, while *Composite*
    just "sums up" its children's results.

    However, the patterns can also cooperate: you can use *Decorator* to
    extend the behavior of a specific object in the *Composite* tree.

-   Designs that make heavy use of
    [Composite](/design-patterns/composite) and
    [Decorator](/design-patterns/decorator) can often benefit from using
    [Prototype](/design-patterns/prototype). Applying the pattern lets
    you clone complex structures instead of re-constructing them from
    scratch.

-   [Decorator](/design-patterns/decorator) lets you change the skin of
    an object, while [Strategy](/design-patterns/strategy) lets you
    change the guts.

-   [Decorator](/design-patterns/decorator) and
    [Proxy](/design-patterns/proxy) have similar structures, but very
    different intents. Both patterns are built on the composition
    principle, where one object is supposed to delegate some of the work
    to another. The difference is that a *Proxy* usually manages the
    life cycle of its service object on its own, whereas the composition
    of *Decorators* is always controlled by the client.



##  Code Examples {#implementations}

[![Decorator in
C#](/images/patterns/icons/csharp.svg?id=da64592defc6e86d57c39c66e9de3e58){width="53"
height="53"
loading="lazy"}](/design-patterns/decorator/csharp/example "Decorator in C#"){.prog-lang-link}
[![Decorator in
C++](/images/patterns/icons/cpp.svg?id=f7782ed8b8666246bfcc3f8fefc3b858){width="53"
height="53"
loading="lazy"}](/design-patterns/decorator/cpp/example "Decorator in C++"){.prog-lang-link}
[![Decorator in
Go](/images/patterns/icons/go.svg?id=1a89927eb99b1ea3fde7701d97970aca){width="53"
height="53"
loading="lazy"}](/design-patterns/decorator/go/example "Decorator in Go"){.prog-lang-link}
[![Decorator in
Java](/images/patterns/icons/java.svg?id=e6d87e2dca08c953fe3acd1275ed4f4e){width="53"
height="53"
loading="lazy"}](/design-patterns/decorator/java/example "Decorator in Java"){.prog-lang-link}
[![Decorator in
PHP](/images/patterns/icons/php.svg?id=be1906eb26b71ec1d3b93720d6156618){width="53"
height="53"
loading="lazy"}](/design-patterns/decorator/php/example "Decorator in PHP"){.prog-lang-link}
[![Decorator in
Python](/images/patterns/icons/python.svg?id=6d815d43c0f7050a1151b43e51569c9f){width="53"
height="53"
loading="lazy"}](/design-patterns/decorator/python/example "Decorator in Python"){.prog-lang-link}
[![Decorator in
Ruby](/images/patterns/icons/ruby.svg?id=b065b718c914bf8e960ef731600be1eb){width="53"
height="53"
loading="lazy"}](/design-patterns/decorator/ruby/example "Decorator in Ruby"){.prog-lang-link}
[![Decorator in
Rust](/images/patterns/icons/rust.svg?id=1f5698a4b5ae23fe79413511747e4a87){width="53"
height="53"
loading="lazy"}](/design-patterns/decorator/rust/example "Decorator in Rust"){.prog-lang-link}
[![Decorator in
Swift](/images/patterns/icons/swift.svg?id=0b716c2d52ec3a48fbe91ac031070c1d){width="53"
height="53"
loading="lazy"}](/design-patterns/decorator/swift/example "Decorator in Swift"){.prog-lang-link}
[![Decorator in
TypeScript](/images/patterns/icons/typescript.svg?id=2239d0f16cb703540c205dd8cb0c0cb7){width="53"
height="53"
loading="lazy"}](/design-patterns/decorator/typescript/example "Decorator in TypeScript"){.prog-lang-link}





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

[Facade []{.fa .fa-arrow-right}](/design-patterns/facade){.btn
.btn-primary rel="next"}



#### Return

[[]{.fa .fa-arrow-left} Composite](/design-patterns/composite){.btn
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

    
    [English](https://refactoring.guru/design-patterns/decorator "English"){.dropdown-item
    .locale-link .active locale="en"}
    [Español](https://refactoring.guru/es/design-patterns/decorator "Español"){.dropdown-item
    .locale-link locale="es"}
    [Français](https://refactoring.guru/fr/design-patterns/decorator "Français"){.dropdown-item
    .locale-link locale="fr"}
    [日本語](https://refactoring.guru/ja/design-patterns/decorator "日本語"){.dropdown-item
    .locale-link locale="ja"}
    [한국어](https://refactoring.guru/ko/design-patterns/decorator "한국어"){.dropdown-item
    .locale-link locale="ko"}
    [Polski](https://refactoring.guru/pl/design-patterns/decorator "Polski"){.dropdown-item
    .locale-link locale="pl"} [Português
    Brasileiro](https://refactoring.guru/pt-br/design-patterns/decorator "Português Brasileiro"){.dropdown-item
    .locale-link locale="pt-br"}
    [Русский](https://refactoring.guru/ru/design-patterns/decorator "Русский"){.dropdown-item
    .locale-link locale="ru"}
    [Українська](https://refactoring.guru/uk/design-patterns/decorator "Українська"){.dropdown-item
    .locale-link locale="uk"}
    [中文](https://refactoringguru.cn/design-patterns/decorator "中文"){.dropdown-item
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






