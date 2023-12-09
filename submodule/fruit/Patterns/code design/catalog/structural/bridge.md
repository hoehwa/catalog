



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


# Bridge {#bridge .title}


##  Intent

**Bridge** is a structural design pattern that lets you split a large
class or a set of closely related classes into two separate
hierarchies---abstraction and implementation---which can be developed
independently of each other.

<figure class="image">
<img
src="/images/patterns/content/bridge/bridge.png?id=bd543d4fb32e11647767301581a5ad54"
srcset="/images/patterns/content/bridge/bridge-2x.png?id=1e905ae5742e5cd10a7eb0e3175ef00d 2x"
width="640" alt="Bridge design pattern" />
</figure>



##  Problem

*Abstraction?* *Implementation?* Sound scary? Stay calm and let's
consider a simple example.

Say you have a geometric `Shape` class with a pair of subclasses:
`Circle` and `Square`. You want to extend this class hierarchy to
incorporate colors, so you plan to create `Red` and `Blue` shape
subclasses. However, since you already have two subclasses, you'll need
to create four class combinations such as `BlueCircle` and `RedSquare`.

<figure class="image">
<img
src="/images/patterns/diagrams/bridge/problem-en.png?id=81f8ed6e6f5d673e15203b22a7a3c502"
srcset="/images/patterns/diagrams/bridge/problem-en-2x.png?id=c67b62720e0465821bbcb84debbbaab0 2x"
loading="lazy" width="480" alt="Bridge pattern problem" />
<figcaption><p>Number of class combinations grows in
geometric progression.</p></figcaption>
</figure>

Adding new shape types and colors to the hierarchy will grow it
exponentially. For example, to add a triangle shape you'd need to
introduce two subclasses, one for each color. And after that, adding a
new color would require creating three subclasses, one for each shape
type. The further we go, the worse it becomes.



##  Solution

This problem occurs because we're trying to extend the shape classes in
two independent dimensions: by form and by color. That's a very common
issue with class inheritance.

The Bridge pattern attempts to solve this problem by switching from
inheritance to the object composition. What this means is that you
extract one of the dimensions into a separate class hierarchy, so that
the original classes will reference an object of the new hierarchy,
instead of having all of its state and behaviors within one class.

<figure class="image">
<img
src="/images/patterns/diagrams/bridge/solution-en.png?id=b72caae18c400d6088072f2f3adda7cd"
srcset="/images/patterns/diagrams/bridge/solution-en-2x.png?id=9439c9a85ac3db0399844b45fbbaecf6 2x"
loading="lazy" width="460"
alt="Solution suggested by the Bridge pattern" />
<figcaption><p>You can prevent the explosion of a class hierarchy by
transforming it into several related hierarchies.</p></figcaption>
</figure>

Following this approach, we can extract the color-related code into its
own class with two subclasses: `Red` and `Blue`. The `Shape` class then
gets a reference field pointing to one of the color objects. Now the
shape can delegate any color-related work to the linked color object.
That reference will act as a bridge between the `Shape` and `Color`
classes. From now on, adding new colors won't require changing the shape
hierarchy, and vice versa.

#### Abstraction and Implementation

The GoF book []{.pop-i}["Gang of Four" is a nickname given to the four
authors of the original book about design patterns: *Design Patterns:
Elements of Reusable Object-Oriented Software*
<https://refactoring.guru/gof-book>.]{.pop-content} introduces the terms
*Abstraction* and *Implementation* as part of the Bridge definition. In
my opinion, the terms sound too academic and make the pattern seem more
complicated than it really is. Having read the simple example with
shapes and colors, let's decipher the meaning behind the GoF book's
scary words.

*Abstraction* (also called *interface*) is a high-level control layer
for some entity. This layer isn't supposed to do any real work on its
own. It should delegate the work to the *implementation* layer (also
called *platform*).

Note that we're not talking about *interfaces* or *abstract classes*
from your programming language. These aren't the same things.

When talking about real applications, the abstraction can be represented
by a graphical user interface (GUI), and the implementation could be the
underlying operating system code (API) which the GUI layer calls in
response to user interactions.

Generally speaking, you can extend such an app in two independent
directions:

-   Have several different GUIs (for instance, tailored for regular
    customers or admins).
-   Support several different APIs (for example, to be able to launch
    the app under Windows, Linux, and macOS).

In a worst-case scenario, this app might look like a giant spaghetti
bowl, where hundreds of conditionals connect different types of GUI with
various APIs all over the code.

<figure class="image">
<img
src="/images/patterns/content/bridge/bridge-3-en.png?id=15b8262114938f7bef6602af33f0a62e"
srcset="/images/patterns/content/bridge/bridge-3-en-2x.png?id=65f98465cec6c4c7e38a635689943822 2x"
loading="lazy" width="600"
alt="Managing changes is much easier in modular code" />
<figcaption><p>Making even a simple change to a monolithic codebase is
pretty hard because you must understand the <em>entire thing</em> very
well. Making changes to smaller, well-defined modules is
much easier.</p></figcaption>
</figure>

You can bring order to this chaos by extracting the code related to
specific interface-platform combinations into separate classes. However,
soon you'll discover that there are *lots* of these classes. The class
hierarchy will grow exponentially because adding a new GUI or supporting
a different API would require creating more and more classes.

Let's try to solve this issue with the Bridge pattern. It suggests that
we divide the classes into two hierarchies:

-   Abstraction: the GUI layer of the app.
-   Implementation: the operating systems' APIs.

<figure class="image">
<img
src="/images/patterns/content/bridge/bridge-2-en.png?id=5c5aef57ca6aa8c3c97fd8922fc8bb58"
srcset="/images/patterns/content/bridge/bridge-2-en-2x.png?id=bbd64c96e6711636356944b3564ad67e 2x"
loading="lazy" width="640" alt="Cross-platform architecture" />
<figcaption><p>One of the ways to structure a
cross-platform application.</p></figcaption>
</figure>

The abstraction object controls the appearance of the app, delegating
the actual work to the linked implementation object. Different
implementations are interchangeable as long as they follow a common
interface, enabling the same GUI to work under Windows and Linux.

As a result, you can change the GUI classes without touching the
API-related classes. Moreover, adding support for another operating
system only requires creating a subclass in the implementation
hierarchy.



##  Structure



<figure class="image">
<img
src="/images/patterns/diagrams/bridge/structure-en.png?id=827afa4b40008dc29d26fe0f4d41b9cc"
class="structure-img-non-indexed d-none d-xl-block"
srcset="/images/patterns/diagrams/bridge/structure-en-2x.png?id=77e749744fb5375839b1cf1aa1061648 2x"
loading="lazy" width="560" alt="Bridge design pattern" /><img
src="/images/patterns/diagrams/bridge/structure-en-indexed.png?id=0461ee029a15b02e03e9735f2ca576d4"
class="structure-img-indexed d-xl-none"
srcset="/images/patterns/diagrams/bridge/structure-en-indexed-2x.png?id=99713473c8ba3c08ce6a3540f1453ebc 2x"
loading="lazy" width="560" alt="Bridge design pattern" />
</figure>


1.  The **Abstraction** provides high-level control logic. It relies on
    the implementation object to do the actual low-level work.

2.  The **Implementation** declares the interface that's common for all
    concrete implementations. An abstraction can only communicate with
    an implementation object via methods that are declared here.

    The abstraction may list the same methods as the implementation, but
    usually the abstraction declares some complex behaviors that rely on
    a wide variety of primitive operations declared by the
    implementation.

3.  **Concrete Implementations** contain platform-specific code.

4.  **Refined Abstractions** provide variants of control logic. Like
    their parent, they work with different implementations via the
    general implementation interface.

5.  Usually, the **Client** is only interested in working with the
    abstraction. However, it's the client's job to link the abstraction
    object with one of the implementation objects.




##  Pseudocode

This example illustrates how the **Bridge** pattern can help divide the
monolithic code of an app that manages devices and their remote
controls. The `Device` classes act as the implementation, whereas the
`Remote`s act as the abstraction.

<figure class="image">
<img
src="/images/patterns/diagrams/bridge/example-en.png?id=89c406a189c45885004d7fa094f616b1"
srcset="/images/patterns/diagrams/bridge/example-en-2x.png?id=19bb8272b4082c5f47c4d047e6cb9967 2x"
loading="lazy" width="640"
alt="Structure of the Bridge pattern example" />
<figcaption><p>The original class hierarchy is divided into two parts:
devices and remote controls.</p></figcaption>
</figure>

The base remote control class declares a reference field that links it
with a device object. All remotes work with the devices via the general
device interface, which lets the same remote support multiple device
types.

You can develop the remote control classes independently from the device
classes. All that's needed is to create a new remote subclass. For
example, a basic remote control might only have two buttons, but you
could extend it with additional features, such as an extra battery or a
touchscreen.

The client code links the desired type of remote control with a specific
device object via the remote's constructor.

<figure class="code">
<pre class="code" lang="pseudocode"><code>// The &quot;abstraction&quot; defines the interface for the &quot;control&quot;
// part of the two class hierarchies. It maintains a reference
// to an object of the &quot;implementation&quot; hierarchy and delegates
// all of the real work to this object.
class RemoteControl is
    protected field device: Device
    constructor RemoteControl(device: Device) is
        this.device = device
    method togglePower() is
        if (device.isEnabled()) then
            device.disable()
        else
            device.enable()
    method volumeDown() is
        device.setVolume(device.getVolume() - 10)
    method volumeUp() is
        device.setVolume(device.getVolume() + 10)
    method channelDown() is
        device.setChannel(device.getChannel() - 1)
    method channelUp() is
        device.setChannel(device.getChannel() + 1)


// You can extend classes from the abstraction hierarchy
// independently from device classes.
class AdvancedRemoteControl extends RemoteControl is
    method mute() is
        device.setVolume(0)


// The &quot;implementation&quot; interface declares methods common to all
// concrete implementation classes. It doesn&#39;t have to match the
// abstraction&#39;s interface. In fact, the two interfaces can be
// entirely different. Typically the implementation interface
// provides only primitive operations, while the abstraction
// defines higher-level operations based on those primitives.
interface Device is
    method isEnabled()
    method enable()
    method disable()
    method getVolume()
    method setVolume(percent)
    method getChannel()
    method setChannel(channel)


// All devices follow the same interface.
class Tv implements Device is
    // ...

class Radio implements Device is
    // ...


// Somewhere in client code.
tv = new Tv()
remote = new RemoteControl(tv)
remote.togglePower()

radio = new Radio()
remote = new AdvancedRemoteControl(radio)</code></pre>
</figure>



##  Applicability



Use the Bridge pattern when you want to divide and organize a monolithic
class that has several variants of some functionality (for example, if
the class can work with various database servers).



The bigger a class becomes, the harder it is to figure out how it works,
and the longer it takes to make a change. The changes made to one of the
variations of functionality may require making changes across the whole
class, which often results in making errors or not addressing some
critical side effects.

The Bridge pattern lets you split the monolithic class into several
class hierarchies. After this, you can change the classes in each
hierarchy independently of the classes in the others. This approach
simplifies code maintenance and minimizes the risk of breaking existing
code.



Use the pattern when you need to extend a class in several orthogonal
(independent) dimensions.



The Bridge suggests that you extract a separate class hierarchy for each
of the dimensions. The original class delegates the related work to the
objects belonging to those hierarchies instead of doing everything on
its own.



Use the Bridge if you need to be able to switch implementations at
runtime.



Although it's optional, the Bridge pattern lets you replace the
implementation object inside the abstraction. It's as easy as assigning
a new value to a field.

By the way, this last item is the main reason why so many people confuse
the Bridge with the [Strategy](/design-patterns/strategy) pattern.
Remember that a pattern is more than just a certain way to structure
your classes. It may also communicate intent and a problem being
addressed.





##  How to Implement {#checklist}

1.  Identify the orthogonal dimensions in your classes. These
    independent concepts could be: abstraction/platform,
    domain/infrastructure, front-end/back-end, or
    interface/implementation.

2.  See what operations the client needs and define them in the base
    abstraction class.

3.  Determine the operations available on all platforms. Declare the
    ones that the abstraction needs in the general implementation
    interface.

4.  For all platforms in your domain create concrete implementation
    classes, but make sure they all follow the implementation interface.

5.  Inside the abstraction class, add a reference field for the
    implementation type. The abstraction delegates most of the work to
    the implementation object that's referenced in that field.

6.  If you have several variants of high-level logic, create refined
    abstractions for each variant by extending the base abstraction
    class.

7.  The client code should pass an implementation object to the
    abstraction's constructor to associate one with the other. After
    that, the client can forget about the implementation and work only
    with the abstraction object.



##  Pros and Cons {#pros-cons}



-    You can create platform-independent classes and apps.
-    The client code works with high-level abstractions. It isn't
    exposed to the platform details.
-    *Open/Closed Principle*. You can introduce new abstractions and
    implementations independently from each other.
-    *Single Responsibility Principle*. You can focus on high-level
    logic in the abstraction and on platform details in the
    implementation.



-    You might make the code more complicated by applying the pattern to
    a highly cohesive class.





##  Relations with Other Patterns {#relations}

-   [Bridge](/design-patterns/bridge) is usually designed up-front,
    letting you develop parts of an application independently of each
    other. On the other hand, [Adapter](/design-patterns/adapter) is
    commonly used with an existing app to make some
    otherwise-incompatible classes work together nicely.

-   [Bridge](/design-patterns/bridge), [State](/design-patterns/state),
    [Strategy](/design-patterns/strategy) (and to some degree
    [Adapter](/design-patterns/adapter)) have very similar structures.
    Indeed, all of these patterns are based on composition, which is
    delegating work to other objects. However, they all solve different
    problems. A pattern isn't just a recipe for structuring your code in
    a specific way. It can also communicate to other developers the
    problem the pattern solves.

-   You can use [Abstract Factory](/design-patterns/abstract-factory)
    along with [Bridge](/design-patterns/bridge). This pairing is useful
    when some abstractions defined by *Bridge* can only work with
    specific implementations. In this case, *Abstract Factory* can
    encapsulate these relations and hide the complexity from the client
    code.

-   You can combine [Builder](/design-patterns/builder) with
    [Bridge](/design-patterns/bridge): the director class plays the role
    of the abstraction, while different builders act as implementations.



##  Code Examples {#implementations}

[![Bridge in
C#](/images/patterns/icons/csharp.svg?id=da64592defc6e86d57c39c66e9de3e58){width="53"
height="53"
loading="lazy"}](/design-patterns/bridge/csharp/example "Bridge in C#"){.prog-lang-link}
[![Bridge in
C++](/images/patterns/icons/cpp.svg?id=f7782ed8b8666246bfcc3f8fefc3b858){width="53"
height="53"
loading="lazy"}](/design-patterns/bridge/cpp/example "Bridge in C++"){.prog-lang-link}
[![Bridge in
Go](/images/patterns/icons/go.svg?id=1a89927eb99b1ea3fde7701d97970aca){width="53"
height="53"
loading="lazy"}](/design-patterns/bridge/go/example "Bridge in Go"){.prog-lang-link}
[![Bridge in
Java](/images/patterns/icons/java.svg?id=e6d87e2dca08c953fe3acd1275ed4f4e){width="53"
height="53"
loading="lazy"}](/design-patterns/bridge/java/example "Bridge in Java"){.prog-lang-link}
[![Bridge in
PHP](/images/patterns/icons/php.svg?id=be1906eb26b71ec1d3b93720d6156618){width="53"
height="53"
loading="lazy"}](/design-patterns/bridge/php/example "Bridge in PHP"){.prog-lang-link}
[![Bridge in
Python](/images/patterns/icons/python.svg?id=6d815d43c0f7050a1151b43e51569c9f){width="53"
height="53"
loading="lazy"}](/design-patterns/bridge/python/example "Bridge in Python"){.prog-lang-link}
[![Bridge in
Ruby](/images/patterns/icons/ruby.svg?id=b065b718c914bf8e960ef731600be1eb){width="53"
height="53"
loading="lazy"}](/design-patterns/bridge/ruby/example "Bridge in Ruby"){.prog-lang-link}
[![Bridge in
Rust](/images/patterns/icons/rust.svg?id=1f5698a4b5ae23fe79413511747e4a87){width="53"
height="53"
loading="lazy"}](/design-patterns/bridge/rust/example "Bridge in Rust"){.prog-lang-link}
[![Bridge in
Swift](/images/patterns/icons/swift.svg?id=0b716c2d52ec3a48fbe91ac031070c1d){width="53"
height="53"
loading="lazy"}](/design-patterns/bridge/swift/example "Bridge in Swift"){.prog-lang-link}
[![Bridge in
TypeScript](/images/patterns/icons/typescript.svg?id=2239d0f16cb703540c205dd8cb0c0cb7){width="53"
height="53"
loading="lazy"}](/design-patterns/bridge/typescript/example "Bridge in TypeScript"){.prog-lang-link}





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

[Composite []{.fa .fa-arrow-right}](/design-patterns/composite){.btn
.btn-primary rel="next"}



#### Return

[[]{.fa .fa-arrow-left} Adapter](/design-patterns/adapter){.btn
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

    
    [English](https://refactoring.guru/design-patterns/bridge "English"){.dropdown-item
    .locale-link .active locale="en"}
    [Español](https://refactoring.guru/es/design-patterns/bridge "Español"){.dropdown-item
    .locale-link locale="es"}
    [Français](https://refactoring.guru/fr/design-patterns/bridge "Français"){.dropdown-item
    .locale-link locale="fr"}
    [日本語](https://refactoring.guru/ja/design-patterns/bridge "日本語"){.dropdown-item
    .locale-link locale="ja"}
    [한국어](https://refactoring.guru/ko/design-patterns/bridge "한국어"){.dropdown-item
    .locale-link locale="ko"}
    [Polski](https://refactoring.guru/pl/design-patterns/bridge "Polski"){.dropdown-item
    .locale-link locale="pl"} [Português
    Brasileiro](https://refactoring.guru/pt-br/design-patterns/bridge "Português Brasileiro"){.dropdown-item
    .locale-link locale="pt-br"}
    [Русский](https://refactoring.guru/ru/design-patterns/bridge "Русский"){.dropdown-item
    .locale-link locale="ru"}
    [Українська](https://refactoring.guru/uk/design-patterns/bridge "Українська"){.dropdown-item
    .locale-link locale="uk"}
    [中文](https://refactoringguru.cn/design-patterns/bridge "中文"){.dropdown-item
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






