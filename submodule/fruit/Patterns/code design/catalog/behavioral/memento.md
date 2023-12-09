



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


# Memento {#memento .title}


Also known as: [Snapshot]{style="display:inline-block"}



##  Intent

**Memento** is a behavioral design pattern that lets you save and
restore the previous state of an object without revealing the details of
its implementation.

<figure class="image">
<img
src="/images/patterns/content/memento/memento-en.png?id=e51abf6a98a5b1f91e0f3a000f113e1a"
srcset="/images/patterns/content/memento/memento-en-2x.png?id=6782c5bbd8e036321dfd86558b540dda 2x"
width="640" alt="Memento design pattern" />
</figure>



##  Problem

Imagine that you're creating a text editor app. In addition to simple
text editing, your editor can format text, insert inline images, etc.

At some point, you decided to let users undo any operations carried out
on the text. This feature has become so common over the years that
nowadays people expect every app to have it. For the implementation, you
chose to take the direct approach. Before performing any operation, the
app records the state of all objects and saves it in some storage.
Later, when a user decides to revert an action, the app fetches the
latest snapshot from the history and uses it to restore the state of all
objects.

<figure class="image">
<img
src="/images/patterns/diagrams/memento/problem1-en.png?id=e0d795264bcc87b62a27e41d89d54899"
srcset="/images/patterns/diagrams/memento/problem1-en-2x.png?id=566e033ea5d3ab01e47fc4fc8697f994 2x"
loading="lazy" width="470" alt="Reverting operations in the editor" />
<figcaption><p>Before executing an operation, the app saves a snapshot
of the objects’ state, which can later be used to restore objects to
their previous state.</p></figcaption>
</figure>

Let's think about those state snapshots. How exactly would you produce
one? You'd probably need to go over all the fields in an object and copy
their values into storage. However, this would only work if the object
had quite relaxed access restrictions to its contents. Unfortunately,
most real objects won't let others peek inside them that easily, hiding
all significant data in private fields.

Ignore that problem for now and let's assume that our objects behave
like hippies: preferring open relations and keeping their state public.
While this approach would solve the immediate problem and let you
produce snapshots of objects' states at will, it still has some serious
issues. In the future, you might decide to refactor some of the editor
classes, or add or remove some of the fields. Sounds easy, but this
would also require changing the classes responsible for copying the
state of the affected objects.

<figure class="image">
<img
src="/images/patterns/diagrams/memento/problem2-en.png?id=a1c8258832f35d27f1a566322b34bf78"
srcset="/images/patterns/diagrams/memento/problem2-en-2x.png?id=0fa1afcb7eaf54093e64722a2f187f8c 2x"
loading="lazy" width="300"
alt="How to make a copy of the object&#39;s private state?" />
<figcaption><p>How to make a copy of the object’s
private state?</p></figcaption>
</figure>

But there's more. Let's consider the actual "snapshots" of the editor's
state. What data does it contain? At a bare minimum, it must contain the
actual text, cursor coordinates, current scroll position, etc. To make a
snapshot, you'd need to collect these values and put them into some kind
of container.

Most likely, you're going to store lots of these container objects
inside some list that would represent the history. Therefore the
containers would probably end up being objects of one class. The class
would have almost no methods, but lots of fields that mirror the
editor's state. To allow other objects to write and read data to and
from a snapshot, you'd probably need to make its fields public. That
would expose all the editor's states, private or not. Other classes
would become dependent on every little change to the snapshot class,
which would otherwise happen within private fields and methods without
affecting outer classes.

It looks like we've reached a dead end: you either expose all internal
details of classes, making them too fragile, or restrict access to their
state, making it impossible to produce snapshots. Is there any other way
to implement the \"undo\"?



##  Solution

All problems that we've just experienced are caused by broken
encapsulation. Some objects try to do more than they are supposed to. To
collect the data required to perform some action, they invade the
private space of other objects instead of letting these objects perform
the actual action.

The Memento pattern delegates creating the state snapshots to the actual
owner of that state, the *originator* object. Hence, instead of other
objects trying to copy the editor's state from the "outside," the editor
class itself can make the snapshot since it has full access to its own
state.

The pattern suggests storing the copy of the object's state in a special
object called *memento*. The contents of the memento aren't accessible
to any other object except the one that produced it. Other objects must
communicate with mementos using a limited interface which may allow
fetching the snapshot's metadata (creation time, the name of the
performed operation, etc.), but not the original object's state
contained in the snapshot.

<figure class="image">
<img
src="/images/patterns/diagrams/memento/solution-en.png?id=b8adab0fc6d22cf8d630e560b9a8fafd"
srcset="/images/patterns/diagrams/memento/solution-en-2x.png?id=cfba1b6b9f65659c29178f7399e30b49 2x"
loading="lazy" width="610"
alt="The originator has full access to the memento, whereas the caretaker can only access the metadata" />
<figcaption><p>The originator has full access to the memento, whereas
the caretaker can only access the metadata.</p></figcaption>
</figure>

Such a restrictive policy lets you store mementos inside other objects,
usually called *caretakers*. Since the caretaker works with the memento
only via the limited interface, it's not able to tamper with the state
stored inside the memento. At the same time, the originator has access
to all fields inside the memento, allowing it to restore its previous
state at will.

In our text editor example, we can create a separate history class to
act as the caretaker. A stack of mementos stored inside the caretaker
will grow each time the editor is about to execute an operation. You
could even render this stack within the app's UI, displaying the history
of previously performed operations to a user.

When a user triggers the undo, the history grabs the most recent memento
from the stack and passes it back to the editor, requesting a roll-back.
Since the editor has full access to the memento, it changes its own
state with the values taken from the memento.



##  Structure


#### Implementation based on nested classes

The classic implementation of the pattern relies on support for nested
classes, available in many popular programming languages (such as C++,
C#, and Java).



<figure class="image">
<img
src="/images/patterns/diagrams/memento/structure1.png?id=4b4a42363a005b617d4df06689787385"
class="structure-img-non-indexed d-none d-xl-block"
srcset="/images/patterns/diagrams/memento/structure1-2x.png?id=d4e77295e51c2417f22b7abb396d5977 2x"
loading="lazy" width="580" alt="Memento based on nested classes" /><img
src="/images/patterns/diagrams/memento/structure1-indexed.png?id=f79a8356b087ae6b004aec42b787ae2e"
class="structure-img-indexed d-xl-none"
srcset="/images/patterns/diagrams/memento/structure1-indexed-2x.png?id=62fea7bdbc96420568869ea3bd25f6ad 2x"
loading="lazy" width="580" alt="Memento based on nested classes" />
</figure>



1.  The **Originator** class can produce snapshots of its own state, as
    well as restore its state from snapshots when needed.

2.  The **Memento** is a value object that acts as a snapshot of the
    originator's state. It's a common practice to make the memento
    immutable and pass it the data only once, via the constructor.

3.  The **Caretaker** knows not only "when" and "why" to capture the
    originator's state, but also when the state should be restored.

    A caretaker can keep track of the originator's history by storing a
    stack of mementos. When the originator has to travel back in
    history, the caretaker fetches the topmost memento from the stack
    and passes it to the originator's restoration method.

4.  In this implementation, the memento class is nested inside the
    originator. This lets the originator access the fields and methods
    of the memento, even though they're declared private. On the other
    hand, the caretaker has very limited access to the memento's fields
    and methods, which lets it store mementos in a stack but not tamper
    with their state.

#### Implementation based on an intermediate interface

There's an alternative implementation, suitable for programming
languages that don't support nested classes (yeah, PHP, I'm talking
about you).



<figure class="image">
<img
src="/images/patterns/diagrams/memento/structure2.png?id=fcff71cb648389be2e302fbe55e2f847"
class="structure-img-non-indexed d-none d-xl-block"
srcset="/images/patterns/diagrams/memento/structure2-2x.png?id=aa7fb5d0f622d4344a2cb590f437f8c8 2x"
loading="lazy" width="560" alt="Memento without nested classes" /><img
src="/images/patterns/diagrams/memento/structure2-indexed.png?id=2c98b4f64b03f2a30e159de31ca9f718"
class="structure-img-indexed d-xl-none"
srcset="/images/patterns/diagrams/memento/structure2-indexed-2x.png?id=2fb637daef1110dfa89f15b2d4627894 2x"
loading="lazy" width="560" alt="Memento without nested classes" />
</figure>



1.  In the absence of nested classes, you can restrict access to the
    memento's fields by establishing a convention that caretakers can
    work with a memento only through an explicitly declared intermediary
    interface, which would only declare methods related to the memento's
    metadata.

2.  On the other hand, originators can work with a memento object
    directly, accessing fields and methods declared in the memento
    class. The downside of this approach is that you need to declare all
    members of the memento public.

#### Implementation with even stricter encapsulation

There's another implementation which is useful when you don't want to
leave even the slightest chance of other classes accessing the state of
the originator through the memento.



<figure class="image">
<img
src="/images/patterns/diagrams/memento/structure3.png?id=6c3ef6a916be8c8ec6d6659d19a6a79f"
class="structure-img-non-indexed d-none d-xl-block"
srcset="/images/patterns/diagrams/memento/structure3-2x.png?id=988c37f92059457153d26ba3458d371e 2x"
loading="lazy" width="590"
alt="Memento with strict encapsulation" /><img
src="/images/patterns/diagrams/memento/structure3-indexed.png?id=17e84b0ef89a41bb3fb844c8d7a445ad"
class="structure-img-indexed d-xl-none"
srcset="/images/patterns/diagrams/memento/structure3-indexed-2x.png?id=fef9ae2a0151c105976075aafb8939dd 2x"
loading="lazy" width="590" alt="Memento with strict encapsulation" />
</figure>



1.  This implementation allows having multiple types of originators and
    mementos. Each originator works with a corresponding memento class.
    Neither originators nor mementos expose their state to anyone.

2.  Caretakers are now explicitly restricted from changing the state
    stored in mementos. Moreover, the caretaker class becomes
    independent from the originator because the restoration method is
    now defined in the memento class.

3.  Each memento becomes linked to the originator that produced it. The
    originator passes itself to the memento's constructor, along with
    the values of its state. Thanks to the close relationship between
    these classes, a memento can restore the state of its originator,
    given that the latter has defined the appropriate setters.




##  Pseudocode

This example uses the Memento pattern alongside the
[Command](/design-patterns/command) pattern for storing snapshots of the
complex text editor's state and restoring an earlier state from these
snapshots when needed.

<figure class="image">
<img
src="/images/patterns/diagrams/memento/example.png?id=fb2196b065f374a1c2a64a0943463760"
srcset="/images/patterns/diagrams/memento/example-2x.png?id=41a73f3cc22bc3dd180f53e6968974d4 2x"
loading="lazy" width="600" alt="Structure of the Memento example" />
<figcaption><p>Saving snapshots of the text
editor’s state.</p></figcaption>
</figure>

The command objects act as caretakers. They fetch the editor's memento
before executing operations related to commands. When a user attempts to
undo the most recent command, the editor can use the memento stored in
that command to revert itself to the previous state.

The memento class doesn't declare any public fields, getters or setters.
Therefore no object can alter its contents. Mementos are linked to the
editor object that created them. This lets a memento restore the linked
editor's state by passing the data via setters on the editor object.
Since mementos are linked to specific editor objects, you can make your
app support several independent editor windows with a centralized undo
stack.

<figure class="code">
<pre class="code" lang="pseudocode"><code>// The originator holds some important data that may change over
// time. It also defines a method for saving its state inside a
// memento and another method for restoring the state from it.
class Editor is
    private field text, curX, curY, selectionWidth

    method setText(text) is
        this.text = text

    method setCursor(x, y) is
        this.curX = x
        this.curY = y

    method setSelectionWidth(width) is
        this.selectionWidth = width

    // Saves the current state inside a memento.
    method createSnapshot():Snapshot is
        // Memento is an immutable object; that&#39;s why the
        // originator passes its state to the memento&#39;s
        // constructor parameters.
        return new Snapshot(this, text, curX, curY, selectionWidth)

// The memento class stores the past state of the editor.
class Snapshot is
    private field editor: Editor
    private field text, curX, curY, selectionWidth

    constructor Snapshot(editor, text, curX, curY, selectionWidth) is
        this.editor = editor
        this.text = text
        this.curX = x
        this.curY = y
        this.selectionWidth = selectionWidth

    // At some point, a previous state of the editor can be
    // restored using a memento object.
    method restore() is
        editor.setText(text)
        editor.setCursor(curX, curY)
        editor.setSelectionWidth(selectionWidth)

// A command object can act as a caretaker. In that case, the
// command gets a memento just before it changes the
// originator&#39;s state. When undo is requested, it restores the
// originator&#39;s state from a memento.
class Command is
    private field backup: Snapshot

    method makeBackup() is
        backup = editor.createSnapshot()

    method undo() is
        if (backup != null)
            backup.restore()
    // ...</code></pre>
</figure>



##  Applicability



Use the Memento pattern when you want to produce snapshots of the
object's state to be able to restore a previous state of the object.



The Memento pattern lets you make full copies of an object's state,
including private fields, and store them separately from the object.
While most people remember this pattern thanks to the "undo" use case,
it's also indispensable when dealing with transactions (i.e., if you
need to roll back an operation on error).



Use the pattern when direct access to the object's
fields/getters/setters violates its encapsulation.



The Memento makes the object itself responsible for creating a snapshot
of its state. No other object can read the snapshot, making the original
object's state data safe and secure.





##  How to Implement {#checklist}

1.  Determine what class will play the role of the originator. It's
    important to know whether the program uses one central object of
    this type or multiple smaller ones.

2.  Create the memento class. One by one, declare a set of fields that
    mirror the fields declared inside the originator class.

3.  Make the memento class immutable. A memento should accept the data
    just once, via the constructor. The class should have no setters.

4.  If your programming language supports nested classes, nest the
    memento inside the originator. If not, extract a blank interface
    from the memento class and make all other objects use it to refer to
    the memento. You may add some metadata operations to the interface,
    but nothing that exposes the originator's state.

5.  Add a method for producing mementos to the originator class. The
    originator should pass its state to the memento via one or multiple
    arguments of the memento's constructor.

    The return type of the method should be of the interface you
    extracted in the previous step (assuming that you extracted it at
    all). Under the hood, the memento-producing method should work
    directly with the memento class.

6.  Add a method for restoring the originator's state to its class. It
    should accept a memento object as an argument. If you extracted an
    interface in the previous step, make it the type of the parameter.
    In this case, you need to typecast the incoming object to the
    memento class, since the originator needs full access to that
    object.

7.  The caretaker, whether it represents a command object, a history, or
    something entirely different, should know when to request new
    mementos from the originator, how to store them and when to restore
    the originator with a particular memento.

8.  The link between caretakers and originators may be moved into the
    memento class. In this case, each memento must be connected to the
    originator that had created it. The restoration method would also
    move to the memento class. However, this would all make sense only
    if the memento class is nested into originator or the originator
    class provides sufficient setters for overriding its state.



##  Pros and Cons {#pros-cons}



-    You can produce snapshots of the object's state without violating
    its encapsulation.
-    You can simplify the originator's code by letting the caretaker
    maintain the history of the originator's state.



-    The app might consume lots of RAM if clients create mementos too
    often.
-    Caretakers should track the originator's lifecycle to be able to
    destroy obsolete mementos.
-    Most dynamic programming languages, such as PHP, Python and
    JavaScript, can't guarantee that the state within the memento stays
    untouched.





##  Relations with Other Patterns {#relations}

-   You can use [Command](/design-patterns/command) and
    [Memento](/design-patterns/memento) together when implementing
    "undo". In this case, commands are responsible for performing
    various operations over a target object, while mementos save the
    state of that object just before a command gets executed.

-   You can use [Memento](/design-patterns/memento) along with
    [Iterator](/design-patterns/iterator) to capture the current
    iteration state and roll it back if necessary.

-   Sometimes [Prototype](/design-patterns/prototype) can be a simpler
    alternative to [Memento](/design-patterns/memento). This works if
    the object, the state of which you want to store in the history, is
    fairly straightforward and doesn't have links to external resources,
    or the links are easy to re-establish.



##  Code Examples {#implementations}

[![Memento in
C#](/images/patterns/icons/csharp.svg?id=da64592defc6e86d57c39c66e9de3e58){width="53"
height="53"
loading="lazy"}](/design-patterns/memento/csharp/example "Memento in C#"){.prog-lang-link}
[![Memento in
C++](/images/patterns/icons/cpp.svg?id=f7782ed8b8666246bfcc3f8fefc3b858){width="53"
height="53"
loading="lazy"}](/design-patterns/memento/cpp/example "Memento in C++"){.prog-lang-link}
[![Memento in
Go](/images/patterns/icons/go.svg?id=1a89927eb99b1ea3fde7701d97970aca){width="53"
height="53"
loading="lazy"}](/design-patterns/memento/go/example "Memento in Go"){.prog-lang-link}
[![Memento in
Java](/images/patterns/icons/java.svg?id=e6d87e2dca08c953fe3acd1275ed4f4e){width="53"
height="53"
loading="lazy"}](/design-patterns/memento/java/example "Memento in Java"){.prog-lang-link}
[![Memento in
PHP](/images/patterns/icons/php.svg?id=be1906eb26b71ec1d3b93720d6156618){width="53"
height="53"
loading="lazy"}](/design-patterns/memento/php/example "Memento in PHP"){.prog-lang-link}
[![Memento in
Python](/images/patterns/icons/python.svg?id=6d815d43c0f7050a1151b43e51569c9f){width="53"
height="53"
loading="lazy"}](/design-patterns/memento/python/example "Memento in Python"){.prog-lang-link}
[![Memento in
Ruby](/images/patterns/icons/ruby.svg?id=b065b718c914bf8e960ef731600be1eb){width="53"
height="53"
loading="lazy"}](/design-patterns/memento/ruby/example "Memento in Ruby"){.prog-lang-link}
[![Memento in
Rust](/images/patterns/icons/rust.svg?id=1f5698a4b5ae23fe79413511747e4a87){width="53"
height="53"
loading="lazy"}](/design-patterns/memento/rust/example "Memento in Rust"){.prog-lang-link}
[![Memento in
Swift](/images/patterns/icons/swift.svg?id=0b716c2d52ec3a48fbe91ac031070c1d){width="53"
height="53"
loading="lazy"}](/design-patterns/memento/swift/example "Memento in Swift"){.prog-lang-link}
[![Memento in
TypeScript](/images/patterns/icons/typescript.svg?id=2239d0f16cb703540c205dd8cb0c0cb7){width="53"
height="53"
loading="lazy"}](/design-patterns/memento/typescript/example "Memento in TypeScript"){.prog-lang-link}





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

[Observer []{.fa .fa-arrow-right}](/design-patterns/observer){.btn
.btn-primary rel="next"}



#### Return

[[]{.fa .fa-arrow-left} Mediator](/design-patterns/mediator){.btn
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

    
    [English](https://refactoring.guru/design-patterns/memento "English"){.dropdown-item
    .locale-link .active locale="en"}
    [Español](https://refactoring.guru/es/design-patterns/memento "Español"){.dropdown-item
    .locale-link locale="es"}
    [Français](https://refactoring.guru/fr/design-patterns/memento "Français"){.dropdown-item
    .locale-link locale="fr"}
    [日本語](https://refactoring.guru/ja/design-patterns/memento "日本語"){.dropdown-item
    .locale-link locale="ja"}
    [한국어](https://refactoring.guru/ko/design-patterns/memento "한국어"){.dropdown-item
    .locale-link locale="ko"}
    [Polski](https://refactoring.guru/pl/design-patterns/memento "Polski"){.dropdown-item
    .locale-link locale="pl"} [Português
    Brasileiro](https://refactoring.guru/pt-br/design-patterns/memento "Português Brasileiro"){.dropdown-item
    .locale-link locale="pt-br"}
    [Русский](https://refactoring.guru/ru/design-patterns/memento "Русский"){.dropdown-item
    .locale-link locale="ru"}
    [Українська](https://refactoring.guru/uk/design-patterns/memento "Українська"){.dropdown-item
    .locale-link locale="uk"}
    [中文](https://refactoringguru.cn/design-patterns/memento "中文"){.dropdown-item
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






