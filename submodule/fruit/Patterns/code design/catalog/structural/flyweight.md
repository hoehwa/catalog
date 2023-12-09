



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


# Flyweight {#flyweight .title}


Also known as: [Cache]{style="display:inline-block"}



##  Intent

**Flyweight** is a structural design pattern that lets you fit more
objects into the available amount of RAM by sharing common parts of
state between multiple objects instead of keeping all of the data in
each object.

<figure class="image">
<img
src="/images/patterns/content/flyweight/flyweight.png?id=e34fbacb847dd609b5e68aaf252c4db0"
srcset="/images/patterns/content/flyweight/flyweight-2x.png?id=6a8f17d9550c75c3d648a605c4d31b45 2x"
width="640" alt="Flyweight design pattern" />
</figure>



##  Problem

To have some fun after long working hours, you decided to create a
simple video game: players would be moving around a map and shooting
each other. You chose to implement a realistic particle system and make
it a distinctive feature of the game. Vast quantities of bullets,
missiles, and shrapnel from explosions should fly all over the map and
deliver a thrilling experience to the player.

Upon its completion, you pushed the last commit, built the game and sent
it to your friend for a test drive. Although the game was running
flawlessly on your machine, your friend wasn't able to play for long. On
his computer, the game kept crashing after a few minutes of gameplay.
After spending several hours digging through debug logs, you discovered
that the game crashed because of an insufficient amount of RAM. It
turned out that your friend's rig was much less powerful than your own
computer, and that's why the problem emerged so quickly on his machine.

The actual problem was related to your particle system. Each particle,
such as a bullet, a missile or a piece of shrapnel was represented by a
separate object containing plenty of data. At some point, when the
carnage on a player's screen reached its climax, newly created particles
no longer fit into the remaining RAM, so the program crashed.

<figure class="image">
<img
src="/images/patterns/diagrams/flyweight/problem-en.png?id=7cfc97e5bf1cb38274c93823447cf17e"
srcset="/images/patterns/diagrams/flyweight/problem-en-2x.png?id=80d8ed54c18cc72473045bbd398f9b43 2x"
loading="lazy" width="660" alt="Flyweight pattern problem" />
</figure>



##  Solution

On closer inspection of the `Particle` class, you may notice that the
color and sprite fields consume a lot more memory than other fields.
What's worse is that these two fields store almost identical data across
all particles. For example, all bullets have the same color and sprite.

<figure class="image">
<img
src="/images/patterns/diagrams/flyweight/solution1-en.png?id=4b962ce51832e49a24f16f36be79ec45"
srcset="/images/patterns/diagrams/flyweight/solution1-en-2x.png?id=89d70cf5947b93412fe48750a398d8c3 2x"
loading="lazy" width="640" alt="Flyweight pattern solution" />
</figure>

Other parts of a particle's state, such as coordinates, movement vector
and speed, are unique to each particle. After all, the values of these
fields change over time. This data represents the always changing
context in which the particle exists, while the color and sprite remain
constant for each particle.

This constant data of an object is usually called the *intrinsic state*.
It lives within the object; other objects can only read it, not change
it. The rest of the object's state, often altered "from the outside" by
other objects, is called the *extrinsic state*.

The Flyweight pattern suggests that you stop storing the extrinsic state
inside the object. Instead, you should pass this state to specific
methods which rely on it. Only the intrinsic state stays within the
object, letting you reuse it in different contexts. As a result, you'd
need fewer of these objects since they only differ in the intrinsic
state, which has much fewer variations than the extrinsic.

<figure class="image">
<img
src="/images/patterns/diagrams/flyweight/solution3-en.png?id=e861e35c1214c46ac7333a127462de68"
srcset="/images/patterns/diagrams/flyweight/solution3-en-2x.png?id=a8679f0aa03f6521dd206fcbc5ed9176 2x"
loading="lazy" width="424" alt="Flyweight pattern solution" />
</figure>

Let's return to our game. Assuming that we had extracted the extrinsic
state from our particle class, only three different objects would
suffice to represent all particles in the game: a bullet, a missile, and
a piece of shrapnel. As you've probably guessed by now, an object that
only stores the intrinsic state is called a flyweight.

#### Extrinsic state storage

Where does the extrinsic state move to? Some class should still store
it, right? In most cases, it gets moved to the container object, which
aggregates objects before we apply the pattern.

In our case, that's the main `Game` object that stores all particles in
the `particles` field. To move the extrinsic state into this class, you
need to create several array fields for storing coordinates, vectors,
and speed of each individual particle. But that's not all. You need
another array for storing references to a specific flyweight that
represents a particle. These arrays must be in sync so that you can
access all data of a particle using the same index.

<figure class="image">
<img
src="/images/patterns/diagrams/flyweight/solution2-en.png?id=3e4154df627d99ecd099e07301f8eb81"
srcset="/images/patterns/diagrams/flyweight/solution2-en-2x.png?id=64debda3b847213b134d303bd32613cb 2x"
loading="lazy" width="640" alt="Flyweight pattern solution" />
</figure>

A more elegant solution is to create a separate context class that would
store the extrinsic state along with reference to the flyweight object.
This approach would require having just a single array in the container
class.

Wait a second! Won't we need to have as many of these contextual objects
as we had at the very beginning? Technically, yes. But the thing is,
these objects are much smaller than before. The most memory-consuming
fields have been moved to just a few flyweight objects. Now, a thousand
small contextual objects can reuse a single heavy flyweight object
instead of storing a thousand copies of its data.

#### Flyweight and immutability

Since the same flyweight object can be used in different contexts, you
have to make sure that its state can't be modified. A flyweight should
initialize its state just once, via constructor parameters. It shouldn't
expose any setters or public fields to other objects.

#### Flyweight factory

For more convenient access to various flyweights, you can create a
factory method that manages a pool of existing flyweight objects. The
method accepts the intrinsic state of the desired flyweight from a
client, looks for an existing flyweight object matching this state, and
returns it if it was found. If not, it creates a new flyweight and adds
it to the pool.

There are several options where this method could be placed. The most
obvious place is a flyweight container. Alternatively, you could create
a new factory class. Or you could make the factory method static and put
it inside an actual flyweight class.



##  Structure



<figure class="image">
<img
src="/images/patterns/diagrams/flyweight/structure.png?id=c1e7e1748f957a4792822f902bc1d420"
class="structure-img-non-indexed d-none d-xl-block"
srcset="/images/patterns/diagrams/flyweight/structure-2x.png?id=a7c8347421bde16435fc90a706f5dd34 2x"
loading="lazy" width="640"
alt="Structure of the Flyweight design pattern" /><img
src="/images/patterns/diagrams/flyweight/structure-indexed.png?id=aa490792baa26b04464dacbc1f4a19cd"
class="structure-img-indexed d-xl-none"
srcset="/images/patterns/diagrams/flyweight/structure-indexed-2x.png?id=205e2f7d08b4ac0695f445a9db8989c4 2x"
loading="lazy" width="630"
alt="Structure of the Flyweight design pattern" />
</figure>


1.  The Flyweight pattern is merely an optimization. Before applying it,
    make sure your program does have the RAM consumption problem related
    to having a massive number of similar objects in memory at the same
    time. Make sure that this problem can't be solved in any other
    meaningful way.

2.  The **Flyweight** class contains the portion of the original
    object's state that can be shared between multiple objects. The same
    flyweight object can be used in many different contexts. The state
    stored inside a flyweight is called *intrinsic.* The state passed to
    the flyweight's methods is called *extrinsic.*

3.  The **Context** class contains the extrinsic state, unique across
    all original objects. When a context is paired with one of the
    flyweight objects, it represents the full state of the original
    object.

4.  Usually, the behavior of the original object remains in the
    flyweight class. In this case, whoever calls a flyweight's method
    must also pass appropriate bits of the extrinsic state into the
    method's parameters. On the other hand, the behavior can be moved to
    the context class, which would use the linked flyweight merely as a
    data object.

5.  The **Client** calculates or stores the extrinsic state of
    flyweights. From the client's perspective, a flyweight is a template
    object which can be configured at runtime by passing some contextual
    data into parameters of its methods.

6.  The **Flyweight Factory** manages a pool of existing flyweights.
    With the factory, clients don't create flyweights directly. Instead,
    they call the factory, passing it bits of the intrinsic state of the
    desired flyweight. The factory looks over previously created
    flyweights and either returns an existing one that matches search
    criteria or creates a new one if nothing is found.




##  Pseudocode

In this example, the **Flyweight** pattern helps to reduce memory usage
when rendering millions of tree objects on a canvas.

<figure class="image">
<img
src="/images/patterns/diagrams/flyweight/example.png?id=0818d078c1a79f373e96397f37b7ee06"
srcset="/images/patterns/diagrams/flyweight/example-2x.png?id=9423640fe3688a64201389b6e7aa1f48 2x"
loading="lazy" width="540" alt="Flyweight pattern example" />
</figure>

The pattern extracts the repeating intrinsic state from a main `Tree`
class and moves it into the flyweight class `TreeType`.

Now instead of storing the same data in multiple objects, it's kept in
just a few flyweight objects and linked to appropriate `Tree` objects
which act as contexts. The client code creates new tree objects using
the flyweight factory, which encapsulates the complexity of searching
for the right object and reusing it if needed.

<figure class="code">
<pre class="code" lang="pseudocode"><code>// The flyweight class contains a portion of the state of a
// tree. These fields store values that are unique for each
// particular tree. For instance, you won&#39;t find here the tree
// coordinates. But the texture and colors shared between many
// trees are here. Since this data is usually BIG, you&#39;d waste a
// lot of memory by keeping it in each tree object. Instead, we
// can extract texture, color and other repeating data into a
// separate object which lots of individual tree objects can
// reference.
class TreeType is
    field name
    field color
    field texture
    constructor TreeType(name, color, texture) { ... }
    method draw(canvas, x, y) is
        // 1. Create a bitmap of a given type, color &amp; texture.
        // 2. Draw the bitmap on the canvas at X and Y coords.

// Flyweight factory decides whether to re-use existing
// flyweight or to create a new object.
class TreeFactory is
    static field treeTypes: collection of tree types
    static method getTreeType(name, color, texture) is
        type = treeTypes.find(name, color, texture)
        if (type == null)
            type = new TreeType(name, color, texture)
            treeTypes.add(type)
        return type

// The contextual object contains the extrinsic part of the tree
// state. An application can create billions of these since they
// are pretty small: just two integer coordinates and one
// reference field.
class Tree is
    field x,y
    field type: TreeType
    constructor Tree(x, y, type) { ... }
    method draw(canvas) is
        type.draw(canvas, this.x, this.y)

// The Tree and the Forest classes are the flyweight&#39;s clients.
// You can merge them if you don&#39;t plan to develop the Tree
// class any further.
class Forest is
    field trees: collection of Trees

    method plantTree(x, y, name, color, texture) is
        type = TreeFactory.getTreeType(name, color, texture)
        tree = new Tree(x, y, type)
        trees.add(tree)

    method draw(canvas) is
        foreach (tree in trees) do
            tree.draw(canvas)</code></pre>
</figure>



##  Applicability



Use the Flyweight pattern only when your program must support a huge
number of objects which barely fit into available RAM.



The benefit of applying the pattern depends heavily on how and where
it's used. It's most useful when:

-   an application needs to spawn a huge number of similar objects
-   this drains all available RAM on a target device
-   the objects contain duplicate states which can be extracted and
    shared between multiple objects





##  How to Implement {#checklist}

1.  Divide fields of a class that will become a flyweight into two
    parts:

    -   the intrinsic state: the fields that contain unchanging data
        duplicated across many objects
    -   the extrinsic state: the fields that contain contextual data
        unique to each object

2.  Leave the fields that represent the intrinsic state in the class,
    but make sure they're immutable. They should take their initial
    values only inside the constructor.

3.  Go over methods that use fields of the extrinsic state. For each
    field used in the method, introduce a new parameter and use it
    instead of the field.

4.  Optionally, create a factory class to manage the pool of flyweights.
    It should check for an existing flyweight before creating a new one.
    Once the factory is in place, clients must only request flyweights
    through it. They should describe the desired flyweight by passing
    its intrinsic state to the factory.

5.  The client must store or calculate values of the extrinsic state
    (context) to be able to call methods of flyweight objects. For the
    sake of convenience, the extrinsic state along with the
    flyweight-referencing field may be moved to a separate context
    class.



##  Pros and Cons {#pros-cons}



-    You can save lots of RAM, assuming your program has tons of similar
    objects.



-    You might be trading RAM over CPU cycles when some of the context
    data needs to be recalculated each time somebody calls a flyweight
    method.
-    The code becomes much more complicated. New team members will
    always be wondering why the state of an entity was separated in such
    a way.





##  Relations with Other Patterns {#relations}

-   You can implement shared leaf nodes of the
    [Composite](/design-patterns/composite) tree as
    [Flyweights](/design-patterns/flyweight) to save some RAM.

-   [Flyweight](/design-patterns/flyweight) shows how to make lots of
    little objects, whereas [Facade](/design-patterns/facade) shows how
    to make a single object that represents an entire subsystem.

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



##  Code Examples {#implementations}

[![Flyweight in
C#](/images/patterns/icons/csharp.svg?id=da64592defc6e86d57c39c66e9de3e58){width="53"
height="53"
loading="lazy"}](/design-patterns/flyweight/csharp/example "Flyweight in C#"){.prog-lang-link}
[![Flyweight in
C++](/images/patterns/icons/cpp.svg?id=f7782ed8b8666246bfcc3f8fefc3b858){width="53"
height="53"
loading="lazy"}](/design-patterns/flyweight/cpp/example "Flyweight in C++"){.prog-lang-link}
[![Flyweight in
Go](/images/patterns/icons/go.svg?id=1a89927eb99b1ea3fde7701d97970aca){width="53"
height="53"
loading="lazy"}](/design-patterns/flyweight/go/example "Flyweight in Go"){.prog-lang-link}
[![Flyweight in
Java](/images/patterns/icons/java.svg?id=e6d87e2dca08c953fe3acd1275ed4f4e){width="53"
height="53"
loading="lazy"}](/design-patterns/flyweight/java/example "Flyweight in Java"){.prog-lang-link}
[![Flyweight in
PHP](/images/patterns/icons/php.svg?id=be1906eb26b71ec1d3b93720d6156618){width="53"
height="53"
loading="lazy"}](/design-patterns/flyweight/php/example "Flyweight in PHP"){.prog-lang-link}
[![Flyweight in
Python](/images/patterns/icons/python.svg?id=6d815d43c0f7050a1151b43e51569c9f){width="53"
height="53"
loading="lazy"}](/design-patterns/flyweight/python/example "Flyweight in Python"){.prog-lang-link}
[![Flyweight in
Ruby](/images/patterns/icons/ruby.svg?id=b065b718c914bf8e960ef731600be1eb){width="53"
height="53"
loading="lazy"}](/design-patterns/flyweight/ruby/example "Flyweight in Ruby"){.prog-lang-link}
[![Flyweight in
Rust](/images/patterns/icons/rust.svg?id=1f5698a4b5ae23fe79413511747e4a87){width="53"
height="53"
loading="lazy"}](/design-patterns/flyweight/rust/example "Flyweight in Rust"){.prog-lang-link}
[![Flyweight in
Swift](/images/patterns/icons/swift.svg?id=0b716c2d52ec3a48fbe91ac031070c1d){width="53"
height="53"
loading="lazy"}](/design-patterns/flyweight/swift/example "Flyweight in Swift"){.prog-lang-link}
[![Flyweight in
TypeScript](/images/patterns/icons/typescript.svg?id=2239d0f16cb703540c205dd8cb0c0cb7){width="53"
height="53"
loading="lazy"}](/design-patterns/flyweight/typescript/example "Flyweight in TypeScript"){.prog-lang-link}





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

[Proxy []{.fa .fa-arrow-right}](/design-patterns/proxy){.btn
.btn-primary rel="next"}



#### Return

[[]{.fa .fa-arrow-left} Facade](/design-patterns/facade){.btn
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

    
    [English](https://refactoring.guru/design-patterns/flyweight "English"){.dropdown-item
    .locale-link .active locale="en"}
    [Español](https://refactoring.guru/es/design-patterns/flyweight "Español"){.dropdown-item
    .locale-link locale="es"}
    [Français](https://refactoring.guru/fr/design-patterns/flyweight "Français"){.dropdown-item
    .locale-link locale="fr"}
    [日本語](https://refactoring.guru/ja/design-patterns/flyweight "日本語"){.dropdown-item
    .locale-link locale="ja"}
    [한국어](https://refactoring.guru/ko/design-patterns/flyweight "한국어"){.dropdown-item
    .locale-link locale="ko"}
    [Polski](https://refactoring.guru/pl/design-patterns/flyweight "Polski"){.dropdown-item
    .locale-link locale="pl"} [Português
    Brasileiro](https://refactoring.guru/pt-br/design-patterns/flyweight "Português Brasileiro"){.dropdown-item
    .locale-link locale="pt-br"}
    [Русский](https://refactoring.guru/ru/design-patterns/flyweight "Русский"){.dropdown-item
    .locale-link locale="ru"}
    [Українська](https://refactoring.guru/uk/design-patterns/flyweight "Українська"){.dropdown-item
    .locale-link locale="uk"}
    [中文](https://refactoringguru.cn/design-patterns/flyweight "中文"){.dropdown-item
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






