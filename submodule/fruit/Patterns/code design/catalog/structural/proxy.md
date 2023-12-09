



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


# Proxy {#proxy .title}


##  Intent

**Proxy** is a structural design pattern that lets you provide a
substitute or placeholder for another object. A proxy controls access to
the original object, allowing you to perform something either before or
after the request gets through to the original object.

<figure class="image">
<img
src="/images/patterns/content/proxy/proxy.png?id=efece4647fb11e3f7539291796327666"
srcset="/images/patterns/content/proxy/proxy-2x.png?id=fb3d14e21c210a758d4777f4d93dce09 2x"
width="640" alt="Proxy design pattern" />
</figure>



##  Problem

Why would you want to control access to an object? Here is an example:
you have a massive object that consumes a vast amount of system
resources. You need it from time to time, but not always.

<figure class="image">
<img
src="/images/patterns/diagrams/proxy/problem-en.png?id=b36e65189e939de5dc809636c1946a43"
srcset="/images/patterns/diagrams/proxy/problem-en-2x.png?id=50393231365429384bd08c3fe3807f56 2x"
loading="lazy" width="510" alt="Problem solved by Proxy pattern" />
<figcaption><p>Database queries can be really slow.</p></figcaption>
</figure>

You could implement lazy initialization: create this object only when
it's actually needed. All of the object's clients would need to execute
some deferred initialization code. Unfortunately, this would probably
cause a lot of code duplication.

In an ideal world, we'd want to put this code directly into our object's
class, but that isn't always possible. For instance, the class may be
part of a closed 3rd-party library.



##  Solution

The Proxy pattern suggests that you create a new proxy class with the
same interface as an original service object. Then you update your app
so that it passes the proxy object to all of the original object's
clients. Upon receiving a request from a client, the proxy creates a
real service object and delegates all the work to it.

<figure class="image">
<img
src="/images/patterns/diagrams/proxy/solution-en.png?id=ab36b8b03fabf92c7dd10ad87507b78c"
srcset="/images/patterns/diagrams/proxy/solution-en-2x.png?id=06d3d96b36666ea5762250dbc8d5e624 2x"
loading="lazy" width="510" alt="Solution with the Proxy pattern" />
<figcaption><p>The proxy disguises itself as a database object. It can
handle lazy initialization and result caching without the client or the
real database object even knowing.</p></figcaption>
</figure>

But what's the benefit? If you need to execute something either before
or after the primary logic of the class, the proxy lets you do this
without changing that class. Since the proxy implements the same
interface as the original class, it can be passed to any client that
expects a real service object.



##  Real-World Analogy {#analogy}

<figure class="image">
<img
src="/images/patterns/diagrams/proxy/live-example.png?id=a268c57fdaf073ee81cf4dfc7239eae2"
srcset="/images/patterns/diagrams/proxy/live-example-2x.png?id=8b8083fa1954d2d92ca84a5a5636ead7 2x"
loading="lazy" width="540"
alt="A credit card is a proxy for a bundle of cash" />
<figcaption><p>Credit cards can be used for payments just the same
as cash.</p></figcaption>
</figure>

A credit card is a proxy for a bank account, which is a proxy for a
bundle of cash. Both implement the same interface: they can be used for
making a payment. A consumer feels great because there's no need to
carry loads of cash around. A shop owner is also happy since the income
from a transaction gets added electronically to the shop's bank account
without the risk of losing the deposit or getting robbed on the way to
the bank.



##  Structure



<figure class="image">
<img
src="/images/patterns/diagrams/proxy/structure.png?id=f2478a82a84e1a1e512a8414bf1abd1c"
class="structure-img-non-indexed d-none d-xl-block"
srcset="/images/patterns/diagrams/proxy/structure-2x.png?id=3d54eeca9af4aa373e989a73463539b5 2x"
loading="lazy" width="370"
alt="Structure of the Proxy design pattern" /><img
src="/images/patterns/diagrams/proxy/structure-indexed.png?id=e56d420f31925b3d41348c5036d3cd64"
class="structure-img-indexed d-xl-none"
srcset="/images/patterns/diagrams/proxy/structure-indexed-2x.png?id=ddf2b3b4807e52330c456c59fc52d504 2x"
loading="lazy" width="410"
alt="Structure of the Proxy design pattern" />
</figure>


1.  The **Service Interface** declares the interface of the Service. The
    proxy must follow this interface to be able to disguise itself as a
    service object.

2.  The **Service** is a class that provides some useful business logic.

3.  The **Proxy** class has a reference field that points to a service
    object. After the proxy finishes its processing (e.g., lazy
    initialization, logging, access control, caching, etc.), it passes
    the request to the service object.

    Usually, proxies manage the full lifecycle of their service objects.

4.  The **Client** should work with both services and proxies via the
    same interface. This way you can pass a proxy into any code that
    expects a service object.




##  Pseudocode

This example illustrates how the **Proxy** pattern can help to introduce
lazy initialization and caching to a 3rd-party YouTube integration
library.

<figure class="image">
<img
src="/images/patterns/diagrams/proxy/example.png?id=ddb1402479562b9e2c776933cc861bed"
srcset="/images/patterns/diagrams/proxy/example-2x.png?id=40f22d12d183b9285a380e4a072efb16 2x"
loading="lazy" width="490"
alt="Structure of the Proxy pattern example" />
<figcaption><p>Caching results of a service with
a proxy.</p></figcaption>
</figure>

The library provides us with the video downloading class. However, it's
very inefficient. If the client application requests the same video
multiple times, the library just downloads it over and over, instead of
caching and reusing the first downloaded file.

The proxy class implements the same interface as the original downloader
and delegates it all the work. However, it keeps track of the downloaded
files and returns the cached result when the app requests the same video
multiple times.

<figure class="code">
<pre class="code" lang="pseudocode"><code>// The interface of a remote service.
interface ThirdPartyYouTubeLib is
    method listVideos()
    method getVideoInfo(id)
    method downloadVideo(id)

// The concrete implementation of a service connector. Methods
// of this class can request information from YouTube. The speed
// of the request depends on a user&#39;s internet connection as
// well as YouTube&#39;s. The application will slow down if a lot of
// requests are fired at the same time, even if they all request
// the same information.
class ThirdPartyYouTubeClass implements ThirdPartyYouTubeLib is
    method listVideos() is
        // Send an API request to YouTube.

    method getVideoInfo(id) is
        // Get metadata about some video.

    method downloadVideo(id) is
        // Download a video file from YouTube.

// To save some bandwidth, we can cache request results and keep
// them for some time. But it may be impossible to put such code
// directly into the service class. For example, it could have
// been provided as part of a third party library and/or defined
// as `final`. That&#39;s why we put the caching code into a new
// proxy class which implements the same interface as the
// service class. It delegates to the service object only when
// the real requests have to be sent.
class CachedYouTubeClass implements ThirdPartyYouTubeLib is
    private field service: ThirdPartyYouTubeLib
    private field listCache, videoCache
    field needReset

    constructor CachedYouTubeClass(service: ThirdPartyYouTubeLib) is
        this.service = service

    method listVideos() is
        if (listCache == null || needReset)
            listCache = service.listVideos()
        return listCache

    method getVideoInfo(id) is
        if (videoCache == null || needReset)
            videoCache = service.getVideoInfo(id)
        return videoCache

    method downloadVideo(id) is
        if (!downloadExists(id) || needReset)
            service.downloadVideo(id)

// The GUI class, which used to work directly with a service
// object, stays unchanged as long as it works with the service
// object through an interface. We can safely pass a proxy
// object instead of a real service object since they both
// implement the same interface.
class YouTubeManager is
    protected field service: ThirdPartyYouTubeLib

    constructor YouTubeManager(service: ThirdPartyYouTubeLib) is
        this.service = service

    method renderVideoPage(id) is
        info = service.getVideoInfo(id)
        // Render the video page.

    method renderListPanel() is
        list = service.listVideos()
        // Render the list of video thumbnails.

    method reactOnUserInput() is
        renderVideoPage()
        renderListPanel()

// The application can configure proxies on the fly.
class Application is
    method init() is
        aYouTubeService = new ThirdPartyYouTubeClass()
        aYouTubeProxy = new CachedYouTubeClass(aYouTubeService)
        manager = new YouTubeManager(aYouTubeProxy)
        manager.reactOnUserInput()</code></pre>
</figure>



##  Applicability


There are dozens of ways to utilize the Proxy pattern. Let's go over the
most popular uses.


Lazy initialization (virtual proxy). This is when you have a heavyweight
service object that wastes system resources by being always up, even
though you only need it from time to time.



Instead of creating the object when the app launches, you can delay the
object's initialization to a time when it's really needed.



Access control (protection proxy). This is when you want only specific
clients to be able to use the service object; for instance, when your
objects are crucial parts of an operating system and clients are various
launched applications (including malicious ones).



The proxy can pass the request to the service object only if the
client's credentials match some criteria.



Local execution of a remote service (remote proxy). This is when the
service object is located on a remote server.



In this case, the proxy passes the client request over the network,
handling all of the nasty details of working with the network.



Logging requests (logging proxy). This is when you want to keep a
history of requests to the service object.



The proxy can log each request before passing it to the service.



Caching request results (caching proxy). This is when you need to cache
results of client requests and manage the life cycle of this cache,
especially if results are quite large.



The proxy can implement caching for recurring requests that always yield
the same results. The proxy may use the parameters of requests as the
cache keys.



Smart reference. This is when you need to be able to dismiss a
heavyweight object once there are no clients that use it.



The proxy can keep track of clients that obtained a reference to the
service object or its results. From time to time, the proxy may go over
the clients and check whether they are still active. If the client list
gets empty, the proxy might dismiss the service object and free the
underlying system resources.

The proxy can also track whether the client had modified the service
object. Then the unchanged objects may be reused by other clients.





##  How to Implement {#checklist}

1.  If there's no pre-existing service interface, create one to make
    proxy and service objects interchangeable. Extracting the interface
    from the service class isn't always possible, because you'd need to
    change all of the service's clients to use that interface. Plan B is
    to make the proxy a subclass of the service class, and this way
    it'll inherit the interface of the service.

2.  Create the proxy class. It should have a field for storing a
    reference to the service. Usually, proxies create and manage the
    whole life cycle of their services. On rare occasions, a service is
    passed to the proxy via a constructor by the client.

3.  Implement the proxy methods according to their purposes. In most
    cases, after doing some work, the proxy should delegate the work to
    the service object.

4.  Consider introducing a creation method that decides whether the
    client gets a proxy or a real service. This can be a simple static
    method in the proxy class or a full-blown factory method.

5.  Consider implementing lazy initialization for the service object.



##  Pros and Cons {#pros-cons}



-    You can control the service object without clients knowing about
    it.
-    You can manage the lifecycle of the service object when clients
    don't care about it.
-    The proxy works even if the service object isn't ready or is not
    available.
-    *Open/Closed Principle*. You can introduce new proxies without
    changing the service or clients.



-    The code may become more complicated since you need to introduce a
    lot of new classes.
-    The response from the service might get delayed.





##  Relations with Other Patterns {#relations}

-   With [Adapter](/design-patterns/adapter) you access an existing
    object via different interface. With
    [Proxy](/design-patterns/proxy), the interface stays the same. With
    [Decorator](/design-patterns/decorator) you access the object via an
    enhanced interface.

-   [Facade](/design-patterns/facade) is similar to
    [Proxy](/design-patterns/proxy) in that both buffer a complex entity
    and initialize it on its own. Unlike *Facade*, *Proxy* has the same
    interface as its service object, which makes them interchangeable.

-   [Decorator](/design-patterns/decorator) and
    [Proxy](/design-patterns/proxy) have similar structures, but very
    different intents. Both patterns are built on the composition
    principle, where one object is supposed to delegate some of the work
    to another. The difference is that a *Proxy* usually manages the
    life cycle of its service object on its own, whereas the composition
    of *Decorators* is always controlled by the client.



##  Code Examples {#implementations}

[![Proxy in
C#](/images/patterns/icons/csharp.svg?id=da64592defc6e86d57c39c66e9de3e58){width="53"
height="53"
loading="lazy"}](/design-patterns/proxy/csharp/example "Proxy in C#"){.prog-lang-link}
[![Proxy in
C++](/images/patterns/icons/cpp.svg?id=f7782ed8b8666246bfcc3f8fefc3b858){width="53"
height="53"
loading="lazy"}](/design-patterns/proxy/cpp/example "Proxy in C++"){.prog-lang-link}
[![Proxy in
Go](/images/patterns/icons/go.svg?id=1a89927eb99b1ea3fde7701d97970aca){width="53"
height="53"
loading="lazy"}](/design-patterns/proxy/go/example "Proxy in Go"){.prog-lang-link}
[![Proxy in
Java](/images/patterns/icons/java.svg?id=e6d87e2dca08c953fe3acd1275ed4f4e){width="53"
height="53"
loading="lazy"}](/design-patterns/proxy/java/example "Proxy in Java"){.prog-lang-link}
[![Proxy in
PHP](/images/patterns/icons/php.svg?id=be1906eb26b71ec1d3b93720d6156618){width="53"
height="53"
loading="lazy"}](/design-patterns/proxy/php/example "Proxy in PHP"){.prog-lang-link}
[![Proxy in
Python](/images/patterns/icons/python.svg?id=6d815d43c0f7050a1151b43e51569c9f){width="53"
height="53"
loading="lazy"}](/design-patterns/proxy/python/example "Proxy in Python"){.prog-lang-link}
[![Proxy in
Ruby](/images/patterns/icons/ruby.svg?id=b065b718c914bf8e960ef731600be1eb){width="53"
height="53"
loading="lazy"}](/design-patterns/proxy/ruby/example "Proxy in Ruby"){.prog-lang-link}
[![Proxy in
Rust](/images/patterns/icons/rust.svg?id=1f5698a4b5ae23fe79413511747e4a87){width="53"
height="53"
loading="lazy"}](/design-patterns/proxy/rust/example "Proxy in Rust"){.prog-lang-link}
[![Proxy in
Swift](/images/patterns/icons/swift.svg?id=0b716c2d52ec3a48fbe91ac031070c1d){width="53"
height="53"
loading="lazy"}](/design-patterns/proxy/swift/example "Proxy in Swift"){.prog-lang-link}
[![Proxy in
TypeScript](/images/patterns/icons/typescript.svg?id=2239d0f16cb703540c205dd8cb0c0cb7){width="53"
height="53"
loading="lazy"}](/design-patterns/proxy/typescript/example "Proxy in TypeScript"){.prog-lang-link}





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

[Behavioral Patterns []{.fa
.fa-arrow-right}](/design-patterns/behavioral-patterns){.btn
.btn-primary rel="next"}



#### Return

[[]{.fa .fa-arrow-left} Flyweight](/design-patterns/flyweight){.btn
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

    
    [English](https://refactoring.guru/design-patterns/proxy "English"){.dropdown-item
    .locale-link .active locale="en"}
    [Español](https://refactoring.guru/es/design-patterns/proxy "Español"){.dropdown-item
    .locale-link locale="es"}
    [Français](https://refactoring.guru/fr/design-patterns/proxy "Français"){.dropdown-item
    .locale-link locale="fr"}
    [日本語](https://refactoring.guru/ja/design-patterns/proxy "日本語"){.dropdown-item
    .locale-link locale="ja"}
    [한국어](https://refactoring.guru/ko/design-patterns/proxy "한국어"){.dropdown-item
    .locale-link locale="ko"}
    [Polski](https://refactoring.guru/pl/design-patterns/proxy "Polski"){.dropdown-item
    .locale-link locale="pl"} [Português
    Brasileiro](https://refactoring.guru/pt-br/design-patterns/proxy "Português Brasileiro"){.dropdown-item
    .locale-link locale="pt-br"}
    [Русский](https://refactoring.guru/ru/design-patterns/proxy "Русский"){.dropdown-item
    .locale-link locale="ru"}
    [Українська](https://refactoring.guru/uk/design-patterns/proxy "Українська"){.dropdown-item
    .locale-link locale="uk"}
    [中文](https://refactoringguru.cn/design-patterns/proxy "中文"){.dropdown-item
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






