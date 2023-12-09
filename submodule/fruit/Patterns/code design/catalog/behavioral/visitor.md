



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


# Visitor {#visitor .title}


##  Intent

**Visitor** is a behavioral design pattern that lets you separate
algorithms from the objects on which they operate.

<figure class="image">
<img
src="/images/patterns/content/visitor/visitor.png?id=f36d100188340db7a18854ef7916f972"
srcset="/images/patterns/content/visitor/visitor-2x.png?id=2c5d9ab3046d782c19809d3b80650d65 2x"
width="640" alt="Visitor Design Pattern" />
</figure>



##  Problem

Imagine that your team develops an app which works with geographic
information structured as one colossal graph. Each node of the graph may
represent a complex entity such as a city, but also more granular things
like industries, sightseeing areas, etc. The nodes are connected with
others if there's a road between the real objects that they represent.
Under the hood, each node type is represented by its own class, while
each specific node is an object.

<figure class="image">
<img
src="/images/patterns/diagrams/visitor/problem1.png?id=e7076532da1e936f3519c63270da8454"
srcset="/images/patterns/diagrams/visitor/problem1-2x.png?id=2e5d5143ac55af218754f28761bec17e 2x"
loading="lazy" width="560" alt="Exporting the graph into XML" />
<figcaption><p>Exporting the graph into XML.</p></figcaption>
</figure>

At some point, you got a task to implement exporting the graph into XML
format. At first, the job seemed pretty straightforward. You planned to
add an export method to each node class and then leverage recursion to
go over each node of the graph, executing the export method. The
solution was simple and elegant: thanks to polymorphism, you weren't
coupling the code which called the export method to concrete classes of
nodes.

Unfortunately, the system architect refused to allow you to alter
existing node classes. He said that the code was already in production
and he didn't want to risk breaking it because of a potential bug in
your changes.

<figure class="image">
<img
src="/images/patterns/diagrams/visitor/problem2-en.png?id=f53c592d755890f5d027d7950b9967fc"
srcset="/images/patterns/diagrams/visitor/problem2-en-2x.png?id=8a241a88057253b879e7b756023b52a1 2x"
loading="lazy" width="500"
alt="The XML export method had to be added into all node classes" />
<figcaption><p>The XML export method had to be added into all node
classes, which bore the risk of breaking the whole application if any
bugs slipped through along with the change.</p></figcaption>
</figure>

Besides, he questioned whether it makes sense to have the XML export
code within the node classes. The primary job of these classes was to
work with geodata. The XML export behavior would look alien there.

There was another reason for the refusal. It was highly likely that
after this feature was implemented, someone from the marketing
department would ask you to provide the ability to export into a
different format, or request some other weird stuff. This would force
you to change those precious and fragile classes again.



##  Solution

The Visitor pattern suggests that you place the new behavior into a
separate class called *visitor*, instead of trying to integrate it into
existing classes. The original object that had to perform the behavior
is now passed to one of the visitor's methods as an argument, providing
the method access to all necessary data contained within the object.

Now, what if that behavior can be executed over objects of different
classes? For example, in our case with XML export, the actual
implementation will probably be a little bit different across various
node classes. Thus, the visitor class may define not one, but a set of
methods, each of which could take arguments of different types, like
this:

<figure class="code">
<pre class="code" lang="pseudocode"><code>class ExportVisitor implements Visitor is
    method doForCity(City c) { ... }
    method doForIndustry(Industry f) { ... }
    method doForSightSeeing(SightSeeing ss) { ... }
    // ...</code></pre>
</figure>

But how exactly would we call these methods, especially when dealing
with the whole graph? These methods have different signatures, so we
can't use polymorphism. To pick a proper visitor method that's able to
process a given object, we'd need to check its class. Doesn't this sound
like a nightmare?

<figure class="code">
<pre class="code" lang="pseudocode"><code>foreach (Node node in graph)
    if (node instanceof City)
        exportVisitor.doForCity((City) node)
    if (node instanceof Industry)
        exportVisitor.doForIndustry((Industry) node)
    // ...
}</code></pre>
</figure>

You might ask, why don't we use method overloading? That's when you give
all methods the same name, even if they support different sets of
parameters. Unfortunately, even assuming that our programming language
supports it at all (as Java and C# do), it won't help us. Since the
exact class of a node object is unknown in advance, the overloading
mechanism won't be able to determine the correct method to execute.
It'll default to the method that takes an object of the base `Node`
class.

However, the Visitor pattern addresses this problem. It uses a technique
called [Double Dispatch](/design-patterns/visitor-double-dispatch),
which helps to execute the proper method on an object without cumbersome
conditionals. Instead of letting the client select a proper version of
the method to call, how about we delegate this choice to objects we're
passing to the visitor as an argument? Since the objects know their own
classes, they'll be able to pick a proper method on the visitor less
awkwardly. They "accept" a visitor and tell it what visiting method
should be executed.

<figure class="code">
<pre class="code" lang="pseudocode"><code>// Client code
foreach (Node node in graph)
    node.accept(exportVisitor)

// City
class City is
    method accept(Visitor v) is
        v.doForCity(this)
    // ...

// Industry
class Industry is
    method accept(Visitor v) is
        v.doForIndustry(this)
    // ...</code></pre>
</figure>

I confess. We had to change the node classes after all. But at least the
change is trivial and it lets us add further behaviors without altering
the code once again.

Now, if we extract a common interface for all visitors, all existing
nodes can work with any visitor you introduce into the app. If you find
yourself introducing a new behavior related to nodes, all you have to do
is implement a new visitor class.



##  Real-World Analogy {#analogy}

<figure class="image">
<img
src="/images/patterns/content/visitor/visitor-comic-1.png?id=7ee4fa8800f7c4df4e1aa3b1aca2b7f1"
srcset="/images/patterns/content/visitor/visitor-comic-1-2x.png?id=439032451eb49ebbcb5257f25ecee790 2x"
loading="lazy" width="600" alt="Insurance agent" />
<figcaption><p>A good insurance agent is always ready to offer different
policies to various types of organizations.</p></figcaption>
</figure>

Imagine a seasoned insurance agent who's eager to get new customers. He
can visit every building in a neighborhood, trying to sell insurance to
everyone he meets. Depending on the type of organization that occupies
the building, he can offer specialized insurance policies:

-   If it's a residential building, he sells medical insurance.
-   If it's a bank, he sells theft insurance.
-   If it's a coffee shop, he sells fire and flood insurance.



##  Structure



<figure class="image">
<img
src="/images/patterns/diagrams/visitor/structure-en.png?id=34126311c4e0d5c9fbb970595d2f1777"
class="structure-img-non-indexed d-none d-xl-block"
srcset="/images/patterns/diagrams/visitor/structure-en-2x.png?id=8f0367e7fdc92dbe05df3a86f2d0db45 2x"
loading="lazy" width="520"
alt="Structure of the Visitor design pattern" /><img
src="/images/patterns/diagrams/visitor/structure-en-indexed.png?id=5896a26c1b13364872b585022f29f29c"
class="structure-img-indexed d-xl-none"
srcset="/images/patterns/diagrams/visitor/structure-en-indexed-2x.png?id=16068894aa794946000a539b5f950086 2x"
loading="lazy" width="520"
alt="Structure of the Visitor design pattern" />
</figure>


1.  The **Visitor** interface declares a set of visiting methods that
    can take concrete elements of an object structure as arguments.
    These methods may have the same names if the program is written in a
    language that supports overloading, but the type of their parameters
    must be different.

2.  Each **Concrete Visitor** implements several versions of the same
    behaviors, tailored for different concrete element classes.

3.  The **Element** interface declares a method for "accepting"
    visitors. This method should have one parameter declared with the
    type of the visitor interface.

4.  Each **Concrete Element** must implement the acceptance method. The
    purpose of this method is to redirect the call to the proper
    visitor's method corresponding to the current element class. Be
    aware that even if a base element class implements this method, all
    subclasses must still override this method in their own classes and
    call the appropriate method on the visitor object.

5.  The **Client** usually represents a collection or some other complex
    object (for example, a [Composite](/design-patterns/composite)
    tree). Usually, clients aren't aware of all the concrete element
    classes because they work with objects from that collection via some
    abstract interface.




##  Pseudocode

In this example, the **Visitor** pattern adds XML export support to the
class hierarchy of geometric shapes.

<figure class="image">
<img
src="/images/patterns/diagrams/visitor/example.png?id=d66acd1b9096c47db17ab3bb82b54a59"
srcset="/images/patterns/diagrams/visitor/example-2x.png?id=f44438b98f13fcb50898baefad67ffff 2x"
loading="lazy" width="560"
alt="Structure of the Visitor pattern example" />
<figcaption><p>Exporting various types of objects into XML format via a
visitor object.</p></figcaption>
</figure>

<figure class="code">
<pre class="code" lang="pseudocode"><code>// The element interface declares an `accept` method that takes
// the base visitor interface as an argument.
interface Shape is
    method move(x, y)
    method draw()
    method accept(v: Visitor)

// Each concrete element class must implement the `accept`
// method in such a way that it calls the visitor&#39;s method that
// corresponds to the element&#39;s class.
class Dot implements Shape is
    // ...

    // Note that we&#39;re calling `visitDot`, which matches the
    // current class name. This way we let the visitor know the
    // class of the element it works with.
    method accept(v: Visitor) is
        v.visitDot(this)

class Circle implements Shape is
    // ...
    method accept(v: Visitor) is
        v.visitCircle(this)

class Rectangle implements Shape is
    // ...
    method accept(v: Visitor) is
        v.visitRectangle(this)

class CompoundShape implements Shape is
    // ...
    method accept(v: Visitor) is
        v.visitCompoundShape(this)


// The Visitor interface declares a set of visiting methods that
// correspond to element classes. The signature of a visiting
// method lets the visitor identify the exact class of the
// element that it&#39;s dealing with.
interface Visitor is
    method visitDot(d: Dot)
    method visitCircle(c: Circle)
    method visitRectangle(r: Rectangle)
    method visitCompoundShape(cs: CompoundShape)

// Concrete visitors implement several versions of the same
// algorithm, which can work with all concrete element classes.
//
// You can experience the biggest benefit of the Visitor pattern
// when using it with a complex object structure such as a
// Composite tree. In this case, it might be helpful to store
// some intermediate state of the algorithm while executing the
// visitor&#39;s methods over various objects of the structure.
class XMLExportVisitor implements Visitor is
    method visitDot(d: Dot) is
        // Export the dot&#39;s ID and center coordinates.

    method visitCircle(c: Circle) is
        // Export the circle&#39;s ID, center coordinates and
        // radius.

    method visitRectangle(r: Rectangle) is
        // Export the rectangle&#39;s ID, left-top coordinates,
        // width and height.

    method visitCompoundShape(cs: CompoundShape) is
        // Export the shape&#39;s ID as well as the list of its
        // children&#39;s IDs.


// The client code can run visitor operations over any set of
// elements without figuring out their concrete classes. The
// accept operation directs a call to the appropriate operation
// in the visitor object.
class Application is
    field allShapes: array of Shapes

    method export() is
        exportVisitor = new XMLExportVisitor()

        foreach (shape in allShapes) do
            shape.accept(exportVisitor)</code></pre>
</figure>

If you wonder why we need the `accept` method in this example, my
article [Visitor and Double
Dispatch](/design-patterns/visitor-double-dispatch) addresses this
question in detail.



##  Applicability



Use the Visitor when you need to perform an operation on all elements of
a complex object structure (for example, an object tree).



The Visitor pattern lets you execute an operation over a set of objects
with different classes by having a visitor object implement several
variants of the same operation, which correspond to all target classes.



Use the Visitor to clean up the business logic of auxiliary behaviors.



The pattern lets you make the primary classes of your app more focused
on their main jobs by extracting all other behaviors into a set of
visitor classes.



Use the pattern when a behavior makes sense only in some classes of a
class hierarchy, but not in others.



You can extract this behavior into a separate visitor class and
implement only those visiting methods that accept objects of relevant
classes, leaving the rest empty.





##  How to Implement {#checklist}

1.  Declare the visitor interface with a set of "visiting" methods, one
    per each concrete element class that exists in the program.

2.  Declare the element interface. If you're working with an existing
    element class hierarchy, add the abstract "acceptance" method to the
    base class of the hierarchy. This method should accept a visitor
    object as an argument.

3.  Implement the acceptance methods in all concrete element classes.
    These methods must simply redirect the call to a visiting method on
    the incoming visitor object which matches the class of the current
    element.

4.  The element classes should only work with visitors via the visitor
    interface. Visitors, however, must be aware of all concrete element
    classes, referenced as parameter types of the visiting methods.

5.  For each behavior that can't be implemented inside the element
    hierarchy, create a new concrete visitor class and implement all of
    the visiting methods.

    You might encounter a situation where the visitor will need access
    to some private members of the element class. In this case, you can
    either make these fields or methods public, violating the element's
    encapsulation, or nest the visitor class in the element class. The
    latter is only possible if you're lucky to work with a programming
    language that supports nested classes.

6.  The client must create visitor objects and pass them into elements
    via "acceptance" methods.



##  Pros and Cons {#pros-cons}



-    *Open/Closed Principle*. You can introduce a new behavior that can
    work with objects of different classes without changing these
    classes.
-    *Single Responsibility Principle*. You can move multiple versions
    of the same behavior into the same class.
-    A visitor object can accumulate some useful information while
    working with various objects. This might be handy when you want to
    traverse some complex object structure, such as an object tree, and
    apply the visitor to each object of this structure.



-    You need to update all visitors each time a class gets added to or
    removed from the element hierarchy.
-    Visitors might lack the necessary access to the private fields and
    methods of the elements that they're supposed to work with.





##  Relations with Other Patterns {#relations}

-   You can treat [Visitor](/design-patterns/visitor) as a powerful
    version of the [Command](/design-patterns/command) pattern. Its
    objects can execute operations over various objects of different
    classes.

-   You can use [Visitor](/design-patterns/visitor) to execute an
    operation over an entire [Composite](/design-patterns/composite)
    tree.

-   You can use [Visitor](/design-patterns/visitor) along with
    [Iterator](/design-patterns/iterator) to traverse a complex data
    structure and execute some operation over its elements, even if they
    all have different classes.



##  Code Examples {#implementations}

[![Visitor in
C#](/images/patterns/icons/csharp.svg?id=da64592defc6e86d57c39c66e9de3e58){width="53"
height="53"
loading="lazy"}](/design-patterns/visitor/csharp/example "Visitor in C#"){.prog-lang-link}
[![Visitor in
C++](/images/patterns/icons/cpp.svg?id=f7782ed8b8666246bfcc3f8fefc3b858){width="53"
height="53"
loading="lazy"}](/design-patterns/visitor/cpp/example "Visitor in C++"){.prog-lang-link}
[![Visitor in
Go](/images/patterns/icons/go.svg?id=1a89927eb99b1ea3fde7701d97970aca){width="53"
height="53"
loading="lazy"}](/design-patterns/visitor/go/example "Visitor in Go"){.prog-lang-link}
[![Visitor in
Java](/images/patterns/icons/java.svg?id=e6d87e2dca08c953fe3acd1275ed4f4e){width="53"
height="53"
loading="lazy"}](/design-patterns/visitor/java/example "Visitor in Java"){.prog-lang-link}
[![Visitor in
PHP](/images/patterns/icons/php.svg?id=be1906eb26b71ec1d3b93720d6156618){width="53"
height="53"
loading="lazy"}](/design-patterns/visitor/php/example "Visitor in PHP"){.prog-lang-link}
[![Visitor in
Python](/images/patterns/icons/python.svg?id=6d815d43c0f7050a1151b43e51569c9f){width="53"
height="53"
loading="lazy"}](/design-patterns/visitor/python/example "Visitor in Python"){.prog-lang-link}
[![Visitor in
Ruby](/images/patterns/icons/ruby.svg?id=b065b718c914bf8e960ef731600be1eb){width="53"
height="53"
loading="lazy"}](/design-patterns/visitor/ruby/example "Visitor in Ruby"){.prog-lang-link}
[![Visitor in
Rust](/images/patterns/icons/rust.svg?id=1f5698a4b5ae23fe79413511747e4a87){width="53"
height="53"
loading="lazy"}](/design-patterns/visitor/rust/example "Visitor in Rust"){.prog-lang-link}
[![Visitor in
Swift](/images/patterns/icons/swift.svg?id=0b716c2d52ec3a48fbe91ac031070c1d){width="53"
height="53"
loading="lazy"}](/design-patterns/visitor/swift/example "Visitor in Swift"){.prog-lang-link}
[![Visitor in
TypeScript](/images/patterns/icons/typescript.svg?id=2239d0f16cb703540c205dd8cb0c0cb7){width="53"
height="53"
loading="lazy"}](/design-patterns/visitor/typescript/example "Visitor in TypeScript"){.prog-lang-link}



##  Extra Content {#extras}

-   Puzzled why we can't simply replace the Visitor pattern with method
    overloading? Read my article [Visitor and Double
    Dispatch](/design-patterns/visitor-double-dispatch) to learn about
    the nasty details.





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

[Visitor and Double Dispatch []{.fa
.fa-arrow-right}](/design-patterns/visitor-double-dispatch){.btn
.btn-primary rel="next"}



#### Return

[[]{.fa .fa-arrow-left} Template
Method](/design-patterns/template-method){.btn .btn-default rel="prev"}







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

    
    [English](https://refactoring.guru/design-patterns/visitor "English"){.dropdown-item
    .locale-link .active locale="en"}
    [Español](https://refactoring.guru/es/design-patterns/visitor "Español"){.dropdown-item
    .locale-link locale="es"}
    [Français](https://refactoring.guru/fr/design-patterns/visitor "Français"){.dropdown-item
    .locale-link locale="fr"}
    [日本語](https://refactoring.guru/ja/design-patterns/visitor "日本語"){.dropdown-item
    .locale-link locale="ja"}
    [한국어](https://refactoring.guru/ko/design-patterns/visitor "한국어"){.dropdown-item
    .locale-link locale="ko"}
    [Polski](https://refactoring.guru/pl/design-patterns/visitor "Polski"){.dropdown-item
    .locale-link locale="pl"} [Português
    Brasileiro](https://refactoring.guru/pt-br/design-patterns/visitor "Português Brasileiro"){.dropdown-item
    .locale-link locale="pt-br"}
    [Русский](https://refactoring.guru/ru/design-patterns/visitor "Русский"){.dropdown-item
    .locale-link locale="ru"}
    [Українська](https://refactoring.guru/uk/design-patterns/visitor "Українська"){.dropdown-item
    .locale-link locale="uk"}
    [中文](https://refactoringguru.cn/design-patterns/visitor "中文"){.dropdown-item
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






