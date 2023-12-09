


[[]{.cart-text} ](#checkout){.btn .cart .open-checkout} [
[]{.btn-text-span .d-none .d-sm-inline-block .d-lg-none
.d-hg-inline-block}](#checkout){.btn .btn-secondary .checkout
.open-checkout}








[](/){.home} / [UML](/uml){.type} / [Modeling Business
Systems](/uml/modeling-business-systems){.type}


# Constructing Use Case Diagrams {#constructing-use-case-diagrams .title}




The following checklist shows the steps necessary for the construction
of use case diagrams. After this, we will explain the individual steps
further.

> #### Checklist 3.1 Constructing Use Case Diagrams from the External View
>
> -   Collect information sources---How am I supposed to know that?
> -   Identify potential actors---Which partners and customers use the
>     goods and services of the business system?
> -   Identify potential business use cases---Which goods and services
>     can actors draw upon?
> -   Connect business use cases---Who can make use of what goods and
>     services of the business system?
> -   Describe actors---Who or what do the actors represent?
> -   Search for more business use cases---What else needs to be done?
> -   Edit business use cases---What actually has to be included in a
>     business use case?
> -   Document business use cases---What happens in a business use case?
> -   Model relationships between business use cases---What activities
>     are conducted repeatedly?
> -   Verify the view---Is everything correct?

We deliberately chose the order in which the steps are performed.
However, this order is not mandatory, since in practice, the individual
steps often overlap heavily.

On one hand, a general understanding of the business system and business
processes is important for the realization of each individual step. On
the other hand, for many steps it is also necessary to consult knowledge
carriers. It makes little sense to cling to the personal view of the
analyst, who knows too little about the area of application.

### Collecting Information Sources---How am I Supposed to Know That?

As a first step, it is important to find knowledge carriers, in order
for analysts and knowledge carriers to work out the basic principles
together. Such knowledge carriers are, for example:

-   People who are involved in performing, operating, and controlling
    business processes
-   Users of similar or related IT systems
-   Customers, who are often critical and creative knowledge carriers
-   Business partners
-   Domain experts
-   Management
-   External observers

Several helpful techniques have proven to be practical for the analysis
and understanding of business processes:

-   Observing employees at work
-   Participating in the business processes being investigated
-   Taking the role of an outsider (e.g., of a customer)
-   Giving out surveys
-   Performing interviews
-   Brainstorming with everyone involved
-   Discussing with domain experts
-   Reviewing existing forms, documentation, specifications, handbooks,
    and work tools
-   Describing organizational structure and workflow management
-   Reviewing organization charts and job descriptions

> -   Read through the introduction to the case study in *[Basic
>     Principles and Background](/uml/basic-principles)* once more. In
>     this introduction, we explain the basics of the case study, to
>     help with understanding its business processes.
> -   In your mind, run through all the roles that you can think of and
>     their business processes (passenger, clerk in the duty-free
>     shop, etc.).
> -   Which activities can you think of from the view of the passenger?
>     How would you try to freshen up your memory?

The result of this first step is often a collection of forms, work
instructions, completed surveys, existing process descriptions, business
objects such as tickets or boarding passes, etc. This overview is often
not yet complete, and will be further extended during the modeling
process.

### Identifying Potential Actors---Which Partners and Customers Use the Goods and Services of the Business System?

This step is all about identifying potential actors. Here, this rule
applies: the more the merrier. You can work with these actors in later
steps; or they can be reduced in number or combined.

More potential actors can be found by answering the following questions
(e.g., through consulting knowledge carriers). In doing this, it is
advisable to create groups of people and types of organizations by
abstracting directly from concrete examples of specific persons and
organizations:

-   Which customers are customers of the business system, and which are
    customers of the business processes?
-   Who are the external partners of the business system? Which goods
    and services do these external partners use?
-   Which in-house positions and organization units are partners of the
    business system and use its goods and services?
-   With what external business systems does the business system
    interact?

As a first step, the previous explanations of our case study result in
the following actors:

<figure class="image">
<img src="/files/sm/images/uml/img_28.jpg" />
<figcaption>Figure 3.10 Potential actors</figcaption>
</figure>

In addition to the passenger, who represents travelers, there is the
check-in representative. The *check-in representative* is a person who
is not the actual passenger, but an agent of the passenger. The check-in
representative has the task of performing the check-in with the ticket
of the passenger.

### Identifying Potential Business Use Cases---Which Goods and Services can Actors Draw Upon?

This step is about finding potential business use cases. The rule---the
more the merrier---applies here as well (in reasonable moderation).
Potential business use cases can be found by answering the following
questions:

-   Which goods or services are provided to and used by the customer?
-   Which goods or services are provided to and used by external
    partners?
-   Which goods and services that are provided by the business system
    involve suppliers (suppliers of goods and suppliers of services)?
-   What are the individual actors doing?
-   How and on what occasions does communication take place with other
    business systems or business partners?
-   Which events trigger what activities?

First considerations of our case study result in the following business
use cases:

<figure class="image">
<img src="/files/sm/images/uml/img_29.jpg" />
<figcaption>Figure 3.11 Potential business use cases</figcaption>
</figure>

Initially, the business use cases can only be described in a concise and
informal manner:

-   The *check-in* procedure includes submitting the ticket, baggage
    check-in, seat reservation, and issuing and handing over the
    boarding pass.
-   Passengers who only have hand luggage can use *express check-in*. No
    baggage check-in is performed.
-   During *boarding*, the boarding pass of the passenger is verified at
    the gate.
-   *Automated check-in* is conducted without the help of a check-in
    clerk, directly at a machine (screen). Baggage cannot be checked in.

#### Practical Tips

For us, in practice, the observation technique has proven effective for
identifying business use cases. By observing people involved in the
business processes, activity lists can be created. Following this, the
activities can be grouped by events that lead to the first business use
cases.

### Connecting Business Use Cases---Who Can Make Use of What Goods and Services of the Business System?

By assigning business use cases to actors, a first draft of the use case
diagram evolves (Figure 3.12). This is achieved by answering the
following question:

-   Which customers or business partners have what functionalities
    available to them?

<figure class="image">
<img src="/files/sm/images/uml/img_30.jpg" />
<figcaption>Figure 3.12 First draft of the use case diagram</figcaption>
</figure>

With this first draft we obtain the basis from which we can further edit
and refine the use case diagram.

The passenger can choose between a normal check-in, automated check-in,
and express check-in. The passenger walks to the gate and presents his
or her boarding pass. The check-in representative can perform a regular
check-in, but is not able to perform express check-in and automated
check-in.

### Describing Actors---Who or What do the Actors Represent?

An actor in a diagram has to be named in a way that clarifies the role
that is represented. Here, it is of utter importance that the
terminology of the domain area, meaning a business-oriented term, is
used. In addition to the name, an actor can be further defined with a
description. The question to this end is:

-   How can an actor be described further? For instance, this
    description can include an area of responsibility, requirements from
    the system, or a formal definition of his, her, or its role. Don't
    be afraid to add job descriptions or organizational profiles (for
    example of a catering company)---even if these are not represented
    in UML.

### Searching for More Business Use Cases---What else Needs to be Done?

Once you have found several business use cases, they can be used as
starting points for further questions. Starting from a particular
business use case, the following questions can be asked:

-   Is there anything that has to be done at some point beforehand,
    prior to accessing a particular functionality?
-   Is there anything that has to be done at some point afterwards,
    after performing a particular business use case?
-   Is there anything that needs to be done if nobody performs a
    particular business use case?

In doing so, it is important to consider the proper business system.
Many of the events that occur before or after a business use case take
place outside the business system under consideration. In our case
study, for instance, booking the flight or getting to the airport does
not belong to the system being considered.

If we take a closer look, we notice that a passenger often travels with
luggage, which he or she checks in. Baggage transportation is
responsible for loading luggage into the airplane. Baggage
transportation is carried out by an independent organization, known as a
handling agent. Consequently, it is considered an actor, more
specifically, an outside service provider. It does not matter for our
diagram that individual employees of the partner enterprise perform
these tasks.

Ten minutes before a flight leaves, baggage transportation requests a
passenger list from passenger services, which includes every passenger
who checked in, but did not board the airplane. On the basis of this
list all affected luggage will be unloaded again from the airplane. If
the flight is an international flight, the customs authorities of the
country in which the destination airport is located also request a
passenger list.

This results in two new actors: baggage transportation and the customs
authorities at the destination airport (Figure 3.13):

<figure class="image">
<img src="/files/sm/images/uml/img_31.jpg" />
<figcaption>Figure 3.13 Extended use case diagram</figcaption>
</figure>

### Editing Business Use Cases---What actually has to be Included in a Business Use Case?

Without a doubt, it is difficult to find the right amount of detail in
the modeling of business systems. If almost all the activities of an
actor in a business use case are combined, the use case diagram will
lose practically all of its significance. If the activities are itemized
too thoroughly, the use case diagram gets too complex and contains too
many activities with interrelationships that are hardly recognizable.

Fortunately, some criteria will help you determine the optimal scope of
a business use case. For this purpose, ask yourself the following
questions:

-   Does the business use case consist of a behaviourally related
    sequence of interactions that belong together (an interaction
    sequence)? Items that are included in a business use case have to be
    directly related. Issuing a boarding pass and searching for lost
    luggage are not related at all. Business use cases that violate this
    criterion have to be divided. This prevents the occurrence of
    oversized business use cases.
-   How many actors are involved in a business use case? Business use
    cases that have too many actors have to be divided. This also
    prevents oversized business use cases.
-   Does the business use case deliver tangible and relevant goods or
    services? A business use case is not supposed to describe incomplete
    steps, for example, counting pieces of luggage. Rather, at least in
    a regular case, it is supposed to produce a benefit that has meaning
    from a customer's perspective. Business use cases that violate this
    criterion have to be combined with other business use cases. This
    way, undersized business use cases are prevented.
-   Is the business use case never performed alone, but always in a
    sequence in combination with other business use cases? A business
    use case is not supposed to describe goods and services that are
    only used in combination with other goods and services. Business use
    cases that violate this criterion, have to be combined with other
    business use cases. This also prevents undersized business use
    cases.
-   Is the business use case initiated by an actor? Business use cases
    that are not initiated by an actor are not use cases but internal
    activities that are depicted in the internal view of the business
    system.

A review of the existing business use cases on the basis of these
questions can lead to the consolidation or division of business use
cases.

### Documenting Business Use Cases---What Happens in a Business Use Case?

To understand a business use case, the information from the use case
diagram is not sufficient. The chain of interactions and of the various
scenarios that are behind each business use case have to be described.
This means that the goods and services that the business system provides
have to be described, namely the chain of events from the perspective of
the customer or business partner.

In addition to purely verbal description, documentation in activity
diagrams and sequence diagrams has proven to be especially valuable. The
construction of these diagram types will be treated in the following
sections: *[Activity
Diagrams](/uml/modeling-business-systems/external-view/activity-diagrams)*,
and *[High-Level Sequence
Diagrams](/uml/modeling-business-systems/external-view/sequence-diagrams)*.

### Modeling Relationships between Business Use Cases---What Activities are Conducted Repeatedly?

If you realize that certain parts of an interaction are the same in
several business use cases, you can extract these similarities and
combine them into their own business use case. This new business use
case can be used in other business use cases with an *include
relationship*.

In our case study, the business use case *issuing boarding pass* has not
yet been assigned. We know that the boarding pass is generated and
issued during check-in. At some point during the business use cases
check-in, express check-in, and automated check-in, the boarding pass is
issued (see Figure 3.14):

<figure class="image">
<img src="/files/sm/images/uml/img_32.jpg" />
<figcaption>Figure 3.14 Extended use case diagram</figcaption>
</figure>

### Verifying the View---Is Everything Correct?

All diagrams and records have to be verified by the knowledge carriers.
What we should ask the knowledge carriers for every diagram or view is:

-   Is everything that is contained in the diagram correct and complete?

Even if knowledge carriers can read and understand diagrams themselves
(they can use the reading directions in this text), we should still read
the diagrams to them. Only with this last step is the circle completed.
This results in a verified view, which reflects a current shared
understanding of business systems and business processes.

The completed use case diagram can be verified with the following
checklist:

> #### Checklist 3.2 Verifying Use Case Diagrams from the External View
>
> -   *Completeness*: The use case diagram is complete if there are no
>     further business use cases in the system. All goods and services
>     that are available to customers and partners of the business
>     system are depicted in the form of business use cases (if
>     necessary, business use cases can be spread out into several
>     diagrams).
> -   *Extent*: All business use cases that are included in the use case
>     diagram are real business use cases, meaning they meet the
>     definition of a business use case.
> -   *Degree of detail*: The degree of detail of the business use cases
>     meets the following requirements: A business use case represents a
>     behaviorally coherent interaction sequence. A business use case is
>     initiated by an actor, and has only a few actors. A business use
>     case represents a functionality that is tangible and that yields a
>     relevant result.
> -   *Relationships between business use cases*: Include relationships
>     are applied properly.
> -   *Naming and describing*: The names of business use cases describe
>     the functionalities that the business system provides. The naming
>     was done in accordance with the normal terminology of the business
>     system.
> -   *Actors*: The actors in the use case diagram represent roles taken
>     up by outside persons, organizations, or other business systems
>     during interactions.

#### Practical Tips

When using use case diagrams for modeling business systems and business
processes, it is advisable to keep the level of abstraction low. For the
comprehensibility of the diagrams and for communication between the
involved parties, it is better to add redundancies than to abstract too
much.

It is of fundamental importance that the terminology of the business
processes or the organization is used, and that the descriptions of the
business use cases are chosen in a way that can be understood
intuitively.

Terminology from the field of Information Technology does not belong in
use case diagrams on the business-process level. The mixing of terms
from the business process and IT communities leads to poor results. In
reality, we often encounter use cases that are already very close to IT
on the business-process level, e.g., updating a customer index. This
leads to confusion in two aspects:

-   Users---meaning people who are involved in business processes, and
    who are not familiar with IT terminology---do not understand the
    business use cases. Since business use cases describe the
    performance requirements for a business system, the business system
    and business processes cannot be understood, and therefore cannot be
    verified. In a project with poorly formulated business use cases, an
    IT department presented the business use cases to users for
    verification and received just one short answer: "Men throwing
    arrows?!".
-   Technical details on the level of business use cases distract from
    the business-process specific requirements for a system.







#### Read next

[Activity Diagrams []{.fa
.fa-arrow-right}](/uml/modeling-business-systems/external-view/activity-diagrams){.btn
.btn-primary rel="next"}



#### Return

[[]{.fa .fa-arrow-left} Use Case
Diagrams](/uml/modeling-business-systems/external-view/use-case-diagrams){.btn
.btn-default rel="prev"}








[![](/images/csd/computer-science-distilled.png?id=a7b07d54e199c5add8b9d48a08321803)](/computer-science-distilled)





[ Computer Science Distilled](/computer-science-distilled){.btn
.btn-landing-ref .btn-hg .btn-block .btn-secondary
style="font-size: 16px; position: relative"}


Do you remember anything at all from your computer science class?
Quicksort, Graph traversal, Big\'O and other stuff? Revise your memories
with our new [book on Computer Science](/computer-science-distilled).

Psst! Did I mention that we\'re offering **sexy discounts** right now?










[![SourceMaking](/images/content-public/logos/logo.png?id=55f0872eb5fd4505a39679db5f702b58){width="250"
height="312"
srcset="/images/content-public/logos/logo-2x.png?id=fee3b4b0a14ba60dc0fe368695d78be9 2x"}](/){.menu-brand}


-   [ Premium Stuff](/store)
    -   [ Dive Into Design Patterns](/design-patterns-ebook)
    -   [ Dive Into Refactoring](/refactoring-course)
    -   [ Computer Science Distilled](/computer-science-distilled)
-   [ Design Patterns](/design_patterns)
    -   [Creational patterns](/design_patterns/creational_patterns)
        -   [Abstract Factory Design
            Pattern](/design_patterns/abstract_factory)
        -   [Builder Design Pattern](/design_patterns/builder)
        -   [Factory Method Design
            Pattern](/design_patterns/factory_method)
        -   [Object Pool Design Pattern](/design_patterns/object_pool)
        -   [Prototype Design Pattern](/design_patterns/prototype)
        -   [Singleton Design Pattern](/design_patterns/singleton)
    -   [Structural patterns](/design_patterns/structural_patterns)
        -   [Adapter Design Pattern](/design_patterns/adapter)
        -   [Bridge Design Pattern](/design_patterns/bridge)
        -   [Composite Design Pattern](/design_patterns/composite)
        -   [Decorator Design Pattern](/design_patterns/decorator)
        -   [Facade Design Pattern](/design_patterns/facade)
        -   [Flyweight Design Pattern](/design_patterns/flyweight)
        -   [Private Class Data](/design_patterns/private_class_data)
        -   [Proxy Design Pattern](/design_patterns/proxy)
    -   [Behavioral patterns](/design_patterns/behavioral_patterns)
        -   [Chain of
            Responsibility](/design_patterns/chain_of_responsibility)
        -   [Command Design Pattern](/design_patterns/command)
        -   [Interpreter Design Pattern](/design_patterns/interpreter)
        -   [Iterator Design Pattern](/design_patterns/iterator)
        -   [Mediator Design Pattern](/design_patterns/mediator)
        -   [Memento Design Pattern](/design_patterns/memento)
        -   [Null Object Design Pattern](/design_patterns/null_object)
        -   [Observer Design Pattern](/design_patterns/observer)
        -   [State Design Pattern](/design_patterns/state)
        -   [Strategy Design Pattern](/design_patterns/strategy)
        -   [Template Method Design
            Pattern](/design_patterns/template_method)
        -   [Visitor Design Pattern](/design_patterns/visitor)
-   [ AntiPatterns](/antipatterns)
    -   [Software Development
        AntiPatterns](/antipatterns/software-development-antipatterns)
        -   [The Blob](/antipatterns/the-blob)
        -   [Continuous
            Obsolescence](/antipatterns/continuous-obsolescence)
        -   [Lava Flow](/antipatterns/lava-flow)
        -   [Ambiguous Viewpoint](/antipatterns/ambiguous-viewpoint)
        -   [Functional
            Decomposition](/antipatterns/functional-decomposition)
        -   [Poltergeists](/antipatterns/poltergeists)
        -   [Boat Anchor](/antipatterns/boat-anchor)
        -   [Golden Hammer](/antipatterns/golden-hammer)
        -   [Dead End](/antipatterns/dead-end)
        -   [Spaghetti Code](/antipatterns/spaghetti-code)
        -   [Input Kludge](/antipatterns/input-kludge)
        -   [Walking through a
            Minefield](/antipatterns/walking-through-minefield)
        -   [Cut-And-Paste
            Programming](/antipatterns/cut-and-paste-programming)
        -   [Mushroom Management](/antipatterns/mushroom-management)
    -   [Software Architecture
        AntiPatterns](/antipatterns/software-architecture-antipatterns)
        -   [Autogenerated
            Stovepipe](/antipatterns/autogenerated-stovepipe)
        -   [Stovepipe Enterprise](/antipatterns/stovepipe-enterprise)
        -   [Jumble](/antipatterns/jumble)
        -   [Stovepipe System](/antipatterns/stovepipe-system)
        -   [Cover Your Assets](/antipatterns/cover-your-assets)
        -   [Vendor Lock-In](/antipatterns/vendor-lock-in)
        -   [Wolf Ticket](/antipatterns/wolf-ticket)
        -   [Architecture By
            Implication](/antipatterns/architecture-by-implication)
        -   [Warm Bodies](/antipatterns/warm-bodies)
        -   [Design By Committee](/antipatterns/design-by-committee)
        -   [Swiss Army Knife](/antipatterns/swiss-army-knife)
        -   [Reinvent The Wheel](/antipatterns/reinvent-the-wheel)
        -   [The Grand Old Duke of
            York](/antipatterns/the-grand-old-duke-of-york)
    -   [Project Management
        AntiPatterns](/antipatterns/software-project-management-antipatterns)
        -   [Blowhard Jamboree](/antipatterns/blowhard-jamboree)
        -   [Analysis Paralysis](/antipatterns/analysis-paralysis)
        -   [Viewgraph Engineering](/antipatterns/viewgraph-engineering)
        -   [Death By Planning](/antipatterns/death-by-planning)
        -   [Fear of Success](/antipatterns/fear-of-success)
        -   [Corncob](/antipatterns/corncob)
        -   [Intellectual Violence](/antipatterns/intellectual-violence)
        -   [Irrational Management](/antipatterns/irrational-management)
        -   [Smoke and Mirrors](/antipatterns/smoke-and-mirrors)
        -   [Project Mismanagement](/antipatterns/project-mismanagement)
        -   [Throw It over the
            Wall](/antipatterns/throw-it-over-the-wall)
        -   [Fire Drill](/antipatterns/fire-drill)
        -   [The Feud](/antipatterns/the-feud)
        -   [E-mail Is Dangerous](/antipatterns/e-mail-is-dangerous)
-   [ Refactoring](/refactoring)
    -   [Code Smells](/refactoring/smells)
        -   [Bloaters](/refactoring/smells/bloaters)
            -   [Long Method](/refactoring/smells/long-method)
            -   [Large Class](/refactoring/smells/large-class)
            -   [Primitive
                Obsession](/refactoring/smells/primitive-obsession)
            -   [Long Parameter
                List](/refactoring/smells/long-parameter-list)
            -   [Data Clumps](/refactoring/smells/data-clumps)
        -   [Object-Orientation Abusers](/refactoring/smells/oo-abusers)
            -   [Switch
                Statements](/refactoring/smells/switch-statements)
            -   [Temporary Field](/refactoring/smells/temporary-field)
            -   [Refused Bequest](/refactoring/smells/refused-bequest)
            -   [Alternative Classes with Different
                Interfaces](/refactoring/smells/alternative-classes-with-different-interfaces)
        -   [Change Preventers](/refactoring/smells/change-preventers)
            -   [Divergent Change](/refactoring/smells/divergent-change)
            -   [Shotgun Surgery](/refactoring/smells/shotgun-surgery)
            -   [Parallel Inheritance
                Hierarchies](/refactoring/smells/parallel-inheritance-hierarchies)
        -   [Dispensables](/refactoring/smells/dispensables)
            -   [Comments](/refactoring/smells/comments)
            -   [Duplicate Code](/refactoring/smells/duplicate-code)
            -   [Lazy Class](/refactoring/smells/lazy-class)
            -   [Data Class](/refactoring/smells/data-class)
            -   [Dead Code](/refactoring/smells/dead-code)
            -   [Speculative
                Generality](/refactoring/smells/speculative-generality)
        -   [Couplers](/refactoring/smells/couplers)
            -   [Feature Envy](/refactoring/smells/feature-envy)
            -   [Inappropriate
                Intimacy](/refactoring/smells/inappropriate-intimacy)
            -   [Message Chains](/refactoring/smells/message-chains)
            -   [Middle Man](/refactoring/smells/middle-man)
        -   [Other Smells](/refactoring/smells/other)
            -   [Incomplete Library
                Class](/refactoring/smells/incomplete-library-class)
    -   [Refactoring techniques](/refactoring/refactorings)
        -   [Composing Methods](/refactoring/composing-methods)
            -   [Extract Method](/refactoring/extract-method)
            -   [Inline Method](/refactoring/inline-method)
            -   [Extract Variable](/refactoring/extract-variable)
            -   [Inline Temp](/refactoring/inline-temp)
            -   [Replace Temp with
                Query](/refactoring/replace-temp-with-query)
            -   [Split Temporary
                Variable](/refactoring/split-temporary-variable)
            -   [Remove Assignments to
                Parameters](/refactoring/remove-assignments-to-parameters)
            -   [Replace Method with Method
                Object](/refactoring/replace-method-with-method-object)
            -   [Substitute
                Algorithm](/refactoring/substitute-algorithm)
        -   [Moving Features between
            Objects](/refactoring/moving-features-between-objects)
            -   [Move Method](/refactoring/move-method)
            -   [Move Field](/refactoring/move-field)
            -   [Extract Class](/refactoring/extract-class)
            -   [Inline Class](/refactoring/inline-class)
            -   [Hide Delegate](/refactoring/hide-delegate)
            -   [Remove Middle Man](/refactoring/remove-middle-man)
            -   [Introduce Foreign
                Method](/refactoring/introduce-foreign-method)
            -   [Introduce Local
                Extension](/refactoring/introduce-local-extension)
        -   [Organizing Data](/refactoring/organizing-data)
            -   [Self Encapsulate
                Field](/refactoring/self-encapsulate-field)
            -   [Replace Data Value with
                Object](/refactoring/replace-data-value-with-object)
            -   [Change Value to
                Reference](/refactoring/change-value-to-reference)
            -   [Change Reference to
                Value](/refactoring/change-reference-to-value)
            -   [Replace Array with
                Object](/refactoring/replace-array-with-object)
            -   [Duplicate Observed
                Data](/refactoring/duplicate-observed-data)
            -   [Change Unidirectional Association to
                Bidirectional](/refactoring/change-unidirectional-association-to-bidirectional)
            -   [Change Bidirectional Association to
                Unidirectional](/refactoring/change-bidirectional-association-to-unidirectional)
            -   [Replace Magic Number with Symbolic
                Constant](/refactoring/replace-magic-number-with-symbolic-constant)
            -   [Encapsulate Field](/refactoring/encapsulate-field)
            -   [Encapsulate
                Collection](/refactoring/encapsulate-collection)
            -   [Replace Type Code with
                Class](/refactoring/replace-type-code-with-class)
            -   [Replace Type Code with
                Subclasses](/refactoring/replace-type-code-with-subclasses)
            -   [Replace Type Code with
                State/Strategy](/refactoring/replace-type-code-with-state-strategy)
            -   [Replace Subclass with
                Fields](/refactoring/replace-subclass-with-fields)
        -   [Simplifying Conditional
            Expressions](/refactoring/simplifying-conditional-expressions)
            -   [Decompose
                Conditional](/refactoring/decompose-conditional)
            -   [Consolidate Conditional
                Expression](/refactoring/consolidate-conditional-expression)
            -   [Consolidate Duplicate Conditional
                Fragments](/refactoring/consolidate-duplicate-conditional-fragments)
            -   [Remove Control Flag](/refactoring/remove-control-flag)
            -   [Replace Nested Conditional with Guard
                Clauses](/refactoring/replace-nested-conditional-with-guard-clauses)
            -   [Replace Conditional with
                Polymorphism](/refactoring/replace-conditional-with-polymorphism)
            -   [Introduce Null
                Object](/refactoring/introduce-null-object)
            -   [Introduce Assertion](/refactoring/introduce-assertion)
        -   [Simplifying Method
            Calls](/refactoring/simplifying-method-calls)
            -   [Rename Method](/refactoring/rename-method)
            -   [Add Parameter](/refactoring/add-parameter)
            -   [Remove Parameter](/refactoring/remove-parameter)
            -   [Separate Query from
                Modifier](/refactoring/separate-query-from-modifier)
            -   [Parameterize Method](/refactoring/parameterize-method)
            -   [Replace Parameter with Explicit
                Methods](/refactoring/replace-parameter-with-explicit-methods)
            -   [Preserve Whole
                Object](/refactoring/preserve-whole-object)
            -   [Replace Parameter with Method
                Call](/refactoring/replace-parameter-with-method-call)
            -   [Introduce Parameter
                Object](/refactoring/introduce-parameter-object)
            -   [Remove Setting
                Method](/refactoring/remove-setting-method)
            -   [Hide Method](/refactoring/hide-method)
            -   [Replace Constructor with Factory
                Method](/refactoring/replace-constructor-with-factory-method)
            -   [Replace Error Code with
                Exception](/refactoring/replace-error-code-with-exception)
            -   [Replace Exception with
                Test](/refactoring/replace-exception-with-test)
        -   [Dealing with
            Generalisation](/refactoring/dealing-with-generalisation)
            -   [Pull Up Field](/refactoring/pull-up-field)
            -   [Pull Up Method](/refactoring/pull-up-method)
            -   [Pull Up Constructor
                Body](/refactoring/pull-up-constructor-body)
            -   [Push Down Method](/refactoring/push-down-method)
            -   [Push Down Field](/refactoring/push-down-field)
            -   [Extract Subclass](/refactoring/extract-subclass)
            -   [Extract Superclass](/refactoring/extract-superclass)
            -   [Extract Interface](/refactoring/extract-interface)
            -   [Collapse Hierarchy](/refactoring/collapse-hierarchy)
            -   [Form Template
                Method](/refactoring/form-template-method)
            -   [Replace Inheritance with
                Delegation](/refactoring/replace-inheritance-with-delegation)
            -   [Replace Delegation with
                Inheritance](/refactoring/replace-delegation-with-inheritance)
-   [ UML](/uml)
    -   [Introduction](/uml/introduction)
    -   [Basic Principles and Background](/uml/basic-principles)
        -   [Introduction to the Case
            Study](/uml/basic-principles-and-background/introduction-to-the-case-study)
        -   [Models, Views, and
            Diagrams](/uml/basic-principles-and-background/models-views-and-diagrams)
        -   [Information Systems and IT
            Systems](/uml/basic-principles-and-background/information-systems-and-it-systems)
        -   [The Models of our Case
            Study](/uml/basic-principles-and-background/the-models-of-our-case-study)
        -   [History of UML: Methods and
            Notations](/uml/basic-principles-and-background/history-of-uml-methods-and-notations)
        -   [Requirement
            Specification](/uml/basic-principles-and-background/requirement-specification)
        -   [UML 2.0](/uml/basic-principles-and-background/uml2)
    -   [Modeling Business Systems](/uml/modeling-business-systems)
        -   [Business Processes and Business
            Systems](/uml/modeling-business-systems/business-processes-and-business-systems)
        -   [One Model---Two
            Views](/uml/modeling-business-systems/one-model-two-views)
        -   [External
            View](/uml/modeling-business-systems/external-view)
        -   [The Elements of a
            View](/uml/modeling-business-systems/the-elements-of-view)
        -   [Use Case
            Diagrams](/uml/modeling-business-systems/external-view/use-case-diagrams)
        -   [Constructing Use Case
            Diagrams](/uml/modeling-business-systems/external-view/constructing-use-case-diagrams)
        -   [Activity
            Diagrams](/uml/modeling-business-systems/external-view/activity-diagrams)
        -   [Constructing Activity
            Diagrams](/uml/modeling-business-systems/external-view/constructing-activity-diagrams)
        -   [Sequence
            Diagrams](/uml/modeling-business-systems/external-view/sequence-diagrams)
        -   [Constructing Sequence
            Diagrams](/uml/modeling-business-systems/external-view/constructing-sequence-diagrams)
        -   [High-Level Sequence
            Diagrams](/uml/modeling-business-systems/external-view/high-level-sequence-diagrams)
        -   [Sequence Diagrams for Scenarios of Business Use
            Cases](/uml/modeling-business-systems/external-view/sequence-diagrams-for-scenarios-of-business-use-cases)
        -   [Internal
            View](/uml/modeling-business-systems/the-internal-view)
        -   [Package
            Diagram](/uml/modeling-business-systems/internal-view/package-diagram)
        -   [Constructing Package
            Diagrams](/uml/modeling-business-systems/internal-view/constructing-package-diagrams)
        -   [Class
            Diagram](/uml/modeling-business-systems/internal-view/class-diagram)
        -   [Constructing Class
            Diagrams](/uml/modeling-business-systems/internal-view/constructing-class-diagrams)
        -   [Activity
            Diagram](/uml/modeling-business-systems/internal-view/activity-diagram)
    -   [Modeling IT Systems](/uml/modeling-it-systems)
        -   [External View](/uml/modeling-it-systems/external-view)
        -   [The User View or \"I don\'t care how it works, as long as
            it
            works.\"](/uml/modeling-it-systems/external-view/the-user-view-or-i-dont-care-how-it-works-as-long-as-it-works)
        -   [The Elements of a
            View](/uml/modeling-it-systems/external-view/the-elements-of-view)
        -   [Use Case
            Diagram](/uml/modeling-it-systems/external-view/the-elements-of-view/use-case-diagram)
        -   [Query Events and Mutation
            Events](/uml/modeling-it-systems/external-view/query-events-and-mutation-events)
        -   [Use Case Sequence
            Diagram](/uml/modeling-it-systems/external-view/use-case-sequence-diagram)
        -   [Constructing the External
            View](/uml/modeling-it-systems/external-view/constructing-the-external-view)
        -   [Structural View](/uml/modeling-it-systems/structural-view)
        -   [Objects and
            Classes](/uml/modeling-it-systems/structural-view/objects-and-classes)
        -   [Generalization, Specialization, and
            Inheritance](/uml/modeling-it-systems/structural-view/generalization-specialization-and-inheritance)
        -   [Static and Dynamic Business
            Rules](/uml/modeling-it-systems/structural-view/static-and-dynamic-business-rules)
        -   [Elements of the
            View](/uml/modeling-it-systems/structural-view/elements-of-the-view)
        -   [Class
            Diagram](/uml/modeling-it-systems/structural-view/class-diagram)
        -   [Constructing Class
            Diagrams](/uml/modeling-it-systems/structural-view/constructing-class-diagrams)
        -   [The Behavioral
            View](/uml/modeling-it-systems/the-behavioral-view)
        -   [The Life of an
            Object](/uml/modeling-it-systems/the-behavioral-view/the-life-of-an-object)
        -   [The Elements of the
            View](/uml/modeling-it-systems/the-behavioral-view/the-elements-of-the-view)
        -   [Statechart
            Diagram](/uml/modeling-it-systems/the-behavioral-view/statechart-diagram)
        -   [Constructing Statechart
            Diagrams](/uml/modeling-it-systems/the-behavioral-view/constructing-statechart-diagrams)
        -   [Interaction
            View](/uml/modeling-it-systems/interaction-view)
        -   [Seeing What Happens Inside the IT
            System](/uml/modeling-it-systems/interaction-view/seeing-what-happens-inside-the-it-system)
        -   [Elements of the
            View](/uml/modeling-it-systems/interaction-view/elements-of-the-view)
        -   [Communication
            Diagram](/uml/modeling-it-systems/interaction-view/communication-diagram)
        -   [Sequence
            Diagram](/uml/modeling-it-systems/interaction-view/sequence-diagram)
        -   [Constructing Communication
            Diagrams](/uml/modeling-it-systems/interaction-view/constructing-communication-diagrams)
        -   [Constructing Sequence
            Diagrams](/uml/modeling-it-systems/interaction-view/constructing-sequence-diagrams)
    -   [Modeling for System
        Integration](/uml/modeling-for-system-integration)
        -   [Terminology of System
            Integration](/uml/modeling-for-system-integration/terminology-of-system-integration)
        -   [Messages in
            UML](/uml/modeling-for-system-integration/messages-in-uml)
        -   [One Model---Two
            Views](/uml/modeling-for-system-integration/one-model-two-views)
        -   [Process
            View](/uml/modeling-for-system-integration/process-view)
        -   [The Business System Model as
            Foundation](/uml/modeling-for-system-integration/process-view/the-business-system-model-as-foundation)
        -   [Elements of the
            View](/uml/modeling-for-system-integration/process-view/elements-of-the-view)
        -   [Activity
            Diagrams](/uml/modeling-for-system-integration/process-view/activity-diagrams)
        -   [Sequence
            Diagram](/uml/modeling-for-system-integration/process-view/sequence-diagram)
        -   [Constructing Diagrams in the Process
            View](/uml/modeling-for-system-integration/process-view/constructing-diagrams-in-the-process-view)
        -   [The Static
            View](/uml/modeling-for-system-integration/the-static-view)
        -   [Elements of the
            View](/uml/modeling-for-system-integration/the-static-view/elements-of-the-view)
        -   [Class
            Diagram](/uml/modeling-for-system-integration/the-static-view/class-diagram)
        -   [Constructing Class
            Diagrams](/uml/modeling-for-system-integration/the-static-view/constructing-class-diagrams)
        -   [Transforming Data from the IT System to the Message
            \"passenger
            list\"](/uml/modeling-for-system-integration/the-static-view/transforming-data-from-the-it-system-to-the-mess)
        -   [Transformation of UML Messages into Various Standard
            Formats](/uml/modeling-for-system-integration/the-static-view/transformation-of-uml-messages-into-various-stan)



[ Log in](https://sourcemaking.com/login "Log in") [ Contact
us](https://feedback.sourcemaking.com/ "Contact us"){.userecho-public
rel="nofollow"}





[![SourceMaking](/images/content-public/logos/logo-min-xs.png?id=f4a48661fc32a3f349b76a075f28594c){srcset="/images/content-public/logos/logo-min-xs-2x.png?id=34fc05750336c33b7815e231a0f227df 2x"}](/){.navigation-brand}


[![](data:image/svg+xml;base64,PHN2ZyBzdHlsZT0id2lkdGg6IDI4cHg7IGhlaWdodDogMjhweDsgZmlsbDogY3VycmVudENvbG9yOyBkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IG1hcmdpbi10b3A6IC0xNHB4OyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIiB2aWV3Ym94PSIwIDAgNTEyIDUxMiI+PCEtLSEgRm9udCBBd2Vzb21lIFBybyA2LjMuMCBieSBAZm9udGF3ZXNvbWUgLSBodHRwczovL2ZvbnRhd2Vzb21lLmNvbSBMaWNlbnNlIC0gaHR0cHM6Ly9mb250YXdlc29tZS5jb20vbGljZW5zZSAoQ29tbWVyY2lhbCBMaWNlbnNlKSBDb3B5cmlnaHQgMjAyMyBGb250aWNvbnMsIEluYy4gLS0+PHBhdGggZD0iTTM1NiA2MGw2MCAyMC02MCAyMC0yMCA2MC0yMC02MEwyNTYgODBsNjAtMjBMMzM2IDBsMjAgNjB6TTQ2NCAyMDhsNDggMTYtNDggMTYtMTYgNDgtMTYtNDgtNDgtMTYgNDgtMTYgMTYtNDggMTYgNDh6bS0yNDMuOC05LjhsMzMgNjYuOSA3My44IDEwLjcgNTkuOCA4LjctNDMuMyA0Mi4yLTUzLjQgNTIuMSAxMi42IDczLjVMMzEzIDUxMmwtNTMuNS0yOC4xLTY2LTM0LjctNjYgMzQuN0w3My45IDUxMmwxMC4yLTU5LjYgMTIuNi03My41TDQzLjMgMzI2LjggMCAyODQuNmw1OS44LTguNyA3My44LTEwLjcgMzMtNjYuOUwxOTMuNSAxNDRsMjYuOCA1NC4yem0yNi4xIDExNC40bC0yNS0zLjYtMTEuMi0yMi42LTE2LjctMzMuOS0xNi43IDMzLjlMMTY1LjYgMzA5bC0yNSAzLjYtMzcuNCA1LjQgMjcuMSAyNi40IDE4LjEgMTcuNkwxNDQgMzg3bC02LjQgMzcuMyAzMy41LTE3LjYgMjIuMy0xMS43IDIyLjMgMTEuNyAzMy41IDE3LjZMMjQyLjkgMzg3bC00LjMtMjQuOSAxOC4xLTE3LjYgMjcuMS0yNi40LTM3LjQtNS40eiI+PC9wYXRoPjwvc3ZnPg==)
Shop Now!](/store){.btn .btn-md .btn-primary .btn-featured}


-   [ [Contact us]{.caption .d-none
    .d-xl-inline-block}](https://feedback.sourcemaking.com/?show_feedback_form_private=true "Contact us"){.userecho-private
    rel="nofollow"}
-   [ [Log in]{.caption .d-none
    .d-xl-inline-block}](https://sourcemaking.com/login "Log in")
-   






-   [Design Patterns](/design_patterns)
-   [AntiPatterns](/antipatterns)
-   [Refactoring](/refactoring)
-   [UML](/uml)



-   [My account](/home)
-   [Forum](https://sourcemaking.userecho.com/){.userecho-public
    rel="nofollow"}
-   [Contact
    us](https://sourcemaking.userecho.com/?show_feedback_form_private=true){.userecho-private
    rel="nofollow"}
-   [About us](/about-us)










© 2007-2023 [SourceMaking.com](/)[ / ]{.d-none .d-md-inline}\
All rights reserved.



[Terms](/terms) / [Privacy policy](/privacy-policy)











[[]{.cart-text} ](#checkout){.btn .cart .open-checkout} [
[]{.btn-text-span .d-none .d-sm-inline-block .d-lg-none
.d-hg-inline-block}](#checkout){.btn .btn-secondary .checkout
.open-checkout}








[](/){.home} / [UML](/uml){.type} / [Modeling Business
Systems](/uml/modeling-business-systems){.type}


# Constructing Use Case Diagrams {#constructing-use-case-diagrams-1 .title}




The following checklist shows the steps necessary for the construction
of use case diagrams. After this, we will explain the individual steps
further.

> #### Checklist 3.1 Constructing Use Case Diagrams from the External View
>
> -   Collect information sources---How am I supposed to know that?
> -   Identify potential actors---Which partners and customers use the
>     goods and services of the business system?
> -   Identify potential business use cases---Which goods and services
>     can actors draw upon?
> -   Connect business use cases---Who can make use of what goods and
>     services of the business system?
> -   Describe actors---Who or what do the actors represent?
> -   Search for more business use cases---What else needs to be done?
> -   Edit business use cases---What actually has to be included in a
>     business use case?
> -   Document business use cases---What happens in a business use case?
> -   Model relationships between business use cases---What activities
>     are conducted repeatedly?
> -   Verify the view---Is everything correct?

We deliberately chose the order in which the steps are performed.
However, this order is not mandatory, since in practice, the individual
steps often overlap heavily.

On one hand, a general understanding of the business system and business
processes is important for the realization of each individual step. On
the other hand, for many steps it is also necessary to consult knowledge
carriers. It makes little sense to cling to the personal view of the
analyst, who knows too little about the area of application.

### Collecting Information Sources---How am I Supposed to Know That?

As a first step, it is important to find knowledge carriers, in order
for analysts and knowledge carriers to work out the basic principles
together. Such knowledge carriers are, for example:

-   People who are involved in performing, operating, and controlling
    business processes
-   Users of similar or related IT systems
-   Customers, who are often critical and creative knowledge carriers
-   Business partners
-   Domain experts
-   Management
-   External observers

Several helpful techniques have proven to be practical for the analysis
and understanding of business processes:

-   Observing employees at work
-   Participating in the business processes being investigated
-   Taking the role of an outsider (e.g., of a customer)
-   Giving out surveys
-   Performing interviews
-   Brainstorming with everyone involved
-   Discussing with domain experts
-   Reviewing existing forms, documentation, specifications, handbooks,
    and work tools
-   Describing organizational structure and workflow management
-   Reviewing organization charts and job descriptions

> -   Read through the introduction to the case study in *[Basic
>     Principles and Background](/uml/basic-principles)* once more. In
>     this introduction, we explain the basics of the case study, to
>     help with understanding its business processes.
> -   In your mind, run through all the roles that you can think of and
>     their business processes (passenger, clerk in the duty-free
>     shop, etc.).
> -   Which activities can you think of from the view of the passenger?
>     How would you try to freshen up your memory?

The result of this first step is often a collection of forms, work
instructions, completed surveys, existing process descriptions, business
objects such as tickets or boarding passes, etc. This overview is often
not yet complete, and will be further extended during the modeling
process.

### Identifying Potential Actors---Which Partners and Customers Use the Goods and Services of the Business System?

This step is all about identifying potential actors. Here, this rule
applies: the more the merrier. You can work with these actors in later
steps; or they can be reduced in number or combined.

More potential actors can be found by answering the following questions
(e.g., through consulting knowledge carriers). In doing this, it is
advisable to create groups of people and types of organizations by
abstracting directly from concrete examples of specific persons and
organizations:

-   Which customers are customers of the business system, and which are
    customers of the business processes?
-   Who are the external partners of the business system? Which goods
    and services do these external partners use?
-   Which in-house positions and organization units are partners of the
    business system and use its goods and services?
-   With what external business systems does the business system
    interact?

As a first step, the previous explanations of our case study result in
the following actors:

<figure class="image">
<img src="/files/sm/images/uml/img_28.jpg" />
<figcaption>Figure 3.10 Potential actors</figcaption>
</figure>

In addition to the passenger, who represents travelers, there is the
check-in representative. The *check-in representative* is a person who
is not the actual passenger, but an agent of the passenger. The check-in
representative has the task of performing the check-in with the ticket
of the passenger.

### Identifying Potential Business Use Cases---Which Goods and Services can Actors Draw Upon?

This step is about finding potential business use cases. The rule---the
more the merrier---applies here as well (in reasonable moderation).
Potential business use cases can be found by answering the following
questions:

-   Which goods or services are provided to and used by the customer?
-   Which goods or services are provided to and used by external
    partners?
-   Which goods and services that are provided by the business system
    involve suppliers (suppliers of goods and suppliers of services)?
-   What are the individual actors doing?
-   How and on what occasions does communication take place with other
    business systems or business partners?
-   Which events trigger what activities?

First considerations of our case study result in the following business
use cases:

<figure class="image">
<img src="/files/sm/images/uml/img_29.jpg" />
<figcaption>Figure 3.11 Potential business use cases</figcaption>
</figure>

Initially, the business use cases can only be described in a concise and
informal manner:

-   The *check-in* procedure includes submitting the ticket, baggage
    check-in, seat reservation, and issuing and handing over the
    boarding pass.
-   Passengers who only have hand luggage can use *express check-in*. No
    baggage check-in is performed.
-   During *boarding*, the boarding pass of the passenger is verified at
    the gate.
-   *Automated check-in* is conducted without the help of a check-in
    clerk, directly at a machine (screen). Baggage cannot be checked in.

#### Practical Tips

For us, in practice, the observation technique has proven effective for
identifying business use cases. By observing people involved in the
business processes, activity lists can be created. Following this, the
activities can be grouped by events that lead to the first business use
cases.

### Connecting Business Use Cases---Who Can Make Use of What Goods and Services of the Business System?

By assigning business use cases to actors, a first draft of the use case
diagram evolves (Figure 3.12). This is achieved by answering the
following question:

-   Which customers or business partners have what functionalities
    available to them?

<figure class="image">
<img src="/files/sm/images/uml/img_30.jpg" />
<figcaption>Figure 3.12 First draft of the use case diagram</figcaption>
</figure>

With this first draft we obtain the basis from which we can further edit
and refine the use case diagram.

The passenger can choose between a normal check-in, automated check-in,
and express check-in. The passenger walks to the gate and presents his
or her boarding pass. The check-in representative can perform a regular
check-in, but is not able to perform express check-in and automated
check-in.

### Describing Actors---Who or What do the Actors Represent?

An actor in a diagram has to be named in a way that clarifies the role
that is represented. Here, it is of utter importance that the
terminology of the domain area, meaning a business-oriented term, is
used. In addition to the name, an actor can be further defined with a
description. The question to this end is:

-   How can an actor be described further? For instance, this
    description can include an area of responsibility, requirements from
    the system, or a formal definition of his, her, or its role. Don't
    be afraid to add job descriptions or organizational profiles (for
    example of a catering company)---even if these are not represented
    in UML.

### Searching for More Business Use Cases---What else Needs to be Done?

Once you have found several business use cases, they can be used as
starting points for further questions. Starting from a particular
business use case, the following questions can be asked:

-   Is there anything that has to be done at some point beforehand,
    prior to accessing a particular functionality?
-   Is there anything that has to be done at some point afterwards,
    after performing a particular business use case?
-   Is there anything that needs to be done if nobody performs a
    particular business use case?

In doing so, it is important to consider the proper business system.
Many of the events that occur before or after a business use case take
place outside the business system under consideration. In our case
study, for instance, booking the flight or getting to the airport does
not belong to the system being considered.

If we take a closer look, we notice that a passenger often travels with
luggage, which he or she checks in. Baggage transportation is
responsible for loading luggage into the airplane. Baggage
transportation is carried out by an independent organization, known as a
handling agent. Consequently, it is considered an actor, more
specifically, an outside service provider. It does not matter for our
diagram that individual employees of the partner enterprise perform
these tasks.

Ten minutes before a flight leaves, baggage transportation requests a
passenger list from passenger services, which includes every passenger
who checked in, but did not board the airplane. On the basis of this
list all affected luggage will be unloaded again from the airplane. If
the flight is an international flight, the customs authorities of the
country in which the destination airport is located also request a
passenger list.

This results in two new actors: baggage transportation and the customs
authorities at the destination airport (Figure 3.13):

<figure class="image">
<img src="/files/sm/images/uml/img_31.jpg" />
<figcaption>Figure 3.13 Extended use case diagram</figcaption>
</figure>

### Editing Business Use Cases---What actually has to be Included in a Business Use Case?

Without a doubt, it is difficult to find the right amount of detail in
the modeling of business systems. If almost all the activities of an
actor in a business use case are combined, the use case diagram will
lose practically all of its significance. If the activities are itemized
too thoroughly, the use case diagram gets too complex and contains too
many activities with interrelationships that are hardly recognizable.

Fortunately, some criteria will help you determine the optimal scope of
a business use case. For this purpose, ask yourself the following
questions:

-   Does the business use case consist of a behaviourally related
    sequence of interactions that belong together (an interaction
    sequence)? Items that are included in a business use case have to be
    directly related. Issuing a boarding pass and searching for lost
    luggage are not related at all. Business use cases that violate this
    criterion have to be divided. This prevents the occurrence of
    oversized business use cases.
-   How many actors are involved in a business use case? Business use
    cases that have too many actors have to be divided. This also
    prevents oversized business use cases.
-   Does the business use case deliver tangible and relevant goods or
    services? A business use case is not supposed to describe incomplete
    steps, for example, counting pieces of luggage. Rather, at least in
    a regular case, it is supposed to produce a benefit that has meaning
    from a customer's perspective. Business use cases that violate this
    criterion have to be combined with other business use cases. This
    way, undersized business use cases are prevented.
-   Is the business use case never performed alone, but always in a
    sequence in combination with other business use cases? A business
    use case is not supposed to describe goods and services that are
    only used in combination with other goods and services. Business use
    cases that violate this criterion, have to be combined with other
    business use cases. This also prevents undersized business use
    cases.
-   Is the business use case initiated by an actor? Business use cases
    that are not initiated by an actor are not use cases but internal
    activities that are depicted in the internal view of the business
    system.

A review of the existing business use cases on the basis of these
questions can lead to the consolidation or division of business use
cases.

### Documenting Business Use Cases---What Happens in a Business Use Case?

To understand a business use case, the information from the use case
diagram is not sufficient. The chain of interactions and of the various
scenarios that are behind each business use case have to be described.
This means that the goods and services that the business system provides
have to be described, namely the chain of events from the perspective of
the customer or business partner.

In addition to purely verbal description, documentation in activity
diagrams and sequence diagrams has proven to be especially valuable. The
construction of these diagram types will be treated in the following
sections: *[Activity
Diagrams](/uml/modeling-business-systems/external-view/activity-diagrams)*,
and *[High-Level Sequence
Diagrams](/uml/modeling-business-systems/external-view/sequence-diagrams)*.

### Modeling Relationships between Business Use Cases---What Activities are Conducted Repeatedly?

If you realize that certain parts of an interaction are the same in
several business use cases, you can extract these similarities and
combine them into their own business use case. This new business use
case can be used in other business use cases with an *include
relationship*.

In our case study, the business use case *issuing boarding pass* has not
yet been assigned. We know that the boarding pass is generated and
issued during check-in. At some point during the business use cases
check-in, express check-in, and automated check-in, the boarding pass is
issued (see Figure 3.14):

<figure class="image">
<img src="/files/sm/images/uml/img_32.jpg" />
<figcaption>Figure 3.14 Extended use case diagram</figcaption>
</figure>

### Verifying the View---Is Everything Correct?

All diagrams and records have to be verified by the knowledge carriers.
What we should ask the knowledge carriers for every diagram or view is:

-   Is everything that is contained in the diagram correct and complete?

Even if knowledge carriers can read and understand diagrams themselves
(they can use the reading directions in this text), we should still read
the diagrams to them. Only with this last step is the circle completed.
This results in a verified view, which reflects a current shared
understanding of business systems and business processes.

The completed use case diagram can be verified with the following
checklist:

> #### Checklist 3.2 Verifying Use Case Diagrams from the External View
>
> -   *Completeness*: The use case diagram is complete if there are no
>     further business use cases in the system. All goods and services
>     that are available to customers and partners of the business
>     system are depicted in the form of business use cases (if
>     necessary, business use cases can be spread out into several
>     diagrams).
> -   *Extent*: All business use cases that are included in the use case
>     diagram are real business use cases, meaning they meet the
>     definition of a business use case.
> -   *Degree of detail*: The degree of detail of the business use cases
>     meets the following requirements: A business use case represents a
>     behaviorally coherent interaction sequence. A business use case is
>     initiated by an actor, and has only a few actors. A business use
>     case represents a functionality that is tangible and that yields a
>     relevant result.
> -   *Relationships between business use cases*: Include relationships
>     are applied properly.
> -   *Naming and describing*: The names of business use cases describe
>     the functionalities that the business system provides. The naming
>     was done in accordance with the normal terminology of the business
>     system.
> -   *Actors*: The actors in the use case diagram represent roles taken
>     up by outside persons, organizations, or other business systems
>     during interactions.

#### Practical Tips

When using use case diagrams for modeling business systems and business
processes, it is advisable to keep the level of abstraction low. For the
comprehensibility of the diagrams and for communication between the
involved parties, it is better to add redundancies than to abstract too
much.

It is of fundamental importance that the terminology of the business
processes or the organization is used, and that the descriptions of the
business use cases are chosen in a way that can be understood
intuitively.

Terminology from the field of Information Technology does not belong in
use case diagrams on the business-process level. The mixing of terms
from the business process and IT communities leads to poor results. In
reality, we often encounter use cases that are already very close to IT
on the business-process level, e.g., updating a customer index. This
leads to confusion in two aspects:

-   Users---meaning people who are involved in business processes, and
    who are not familiar with IT terminology---do not understand the
    business use cases. Since business use cases describe the
    performance requirements for a business system, the business system
    and business processes cannot be understood, and therefore cannot be
    verified. In a project with poorly formulated business use cases, an
    IT department presented the business use cases to users for
    verification and received just one short answer: "Men throwing
    arrows?!".
-   Technical details on the level of business use cases distract from
    the business-process specific requirements for a system.







#### Read next

[Activity Diagrams []{.fa
.fa-arrow-right}](/uml/modeling-business-systems/external-view/activity-diagrams){.btn
.btn-primary rel="next"}



#### Return

[[]{.fa .fa-arrow-left} Use Case
Diagrams](/uml/modeling-business-systems/external-view/use-case-diagrams){.btn
.btn-default rel="prev"}








[![](/images/csd/computer-science-distilled.png?id=a7b07d54e199c5add8b9d48a08321803)](/computer-science-distilled)





[ Computer Science Distilled](/computer-science-distilled){.btn
.btn-landing-ref .btn-hg .btn-block .btn-secondary
style="font-size: 16px; position: relative"}


Do you remember anything at all from your computer science class?
Quicksort, Graph traversal, Big\'O and other stuff? Revise your memories
with our new [book on Computer Science](/computer-science-distilled).

Psst! Did I mention that we\'re offering **sexy discounts** right now?










[![SourceMaking](/images/content-public/logos/logo.png?id=55f0872eb5fd4505a39679db5f702b58){width="250"
height="312"
srcset="/images/content-public/logos/logo-2x.png?id=fee3b4b0a14ba60dc0fe368695d78be9 2x"}](/){.menu-brand}


-   [ Premium Stuff](/store)
    -   [ Dive Into Design Patterns](/design-patterns-ebook)
    -   [ Dive Into Refactoring](/refactoring-course)
    -   [ Computer Science Distilled](/computer-science-distilled)
-   [ Design Patterns](/design_patterns)
    -   [Creational patterns](/design_patterns/creational_patterns)
        -   [Abstract Factory Design
            Pattern](/design_patterns/abstract_factory)
        -   [Builder Design Pattern](/design_patterns/builder)
        -   [Factory Method Design
            Pattern](/design_patterns/factory_method)
        -   [Object Pool Design Pattern](/design_patterns/object_pool)
        -   [Prototype Design Pattern](/design_patterns/prototype)
        -   [Singleton Design Pattern](/design_patterns/singleton)
    -   [Structural patterns](/design_patterns/structural_patterns)
        -   [Adapter Design Pattern](/design_patterns/adapter)
        -   [Bridge Design Pattern](/design_patterns/bridge)
        -   [Composite Design Pattern](/design_patterns/composite)
        -   [Decorator Design Pattern](/design_patterns/decorator)
        -   [Facade Design Pattern](/design_patterns/facade)
        -   [Flyweight Design Pattern](/design_patterns/flyweight)
        -   [Private Class Data](/design_patterns/private_class_data)
        -   [Proxy Design Pattern](/design_patterns/proxy)
    -   [Behavioral patterns](/design_patterns/behavioral_patterns)
        -   [Chain of
            Responsibility](/design_patterns/chain_of_responsibility)
        -   [Command Design Pattern](/design_patterns/command)
        -   [Interpreter Design Pattern](/design_patterns/interpreter)
        -   [Iterator Design Pattern](/design_patterns/iterator)
        -   [Mediator Design Pattern](/design_patterns/mediator)
        -   [Memento Design Pattern](/design_patterns/memento)
        -   [Null Object Design Pattern](/design_patterns/null_object)
        -   [Observer Design Pattern](/design_patterns/observer)
        -   [State Design Pattern](/design_patterns/state)
        -   [Strategy Design Pattern](/design_patterns/strategy)
        -   [Template Method Design
            Pattern](/design_patterns/template_method)
        -   [Visitor Design Pattern](/design_patterns/visitor)
-   [ AntiPatterns](/antipatterns)
    -   [Software Development
        AntiPatterns](/antipatterns/software-development-antipatterns)
        -   [The Blob](/antipatterns/the-blob)
        -   [Continuous
            Obsolescence](/antipatterns/continuous-obsolescence)
        -   [Lava Flow](/antipatterns/lava-flow)
        -   [Ambiguous Viewpoint](/antipatterns/ambiguous-viewpoint)
        -   [Functional
            Decomposition](/antipatterns/functional-decomposition)
        -   [Poltergeists](/antipatterns/poltergeists)
        -   [Boat Anchor](/antipatterns/boat-anchor)
        -   [Golden Hammer](/antipatterns/golden-hammer)
        -   [Dead End](/antipatterns/dead-end)
        -   [Spaghetti Code](/antipatterns/spaghetti-code)
        -   [Input Kludge](/antipatterns/input-kludge)
        -   [Walking through a
            Minefield](/antipatterns/walking-through-minefield)
        -   [Cut-And-Paste
            Programming](/antipatterns/cut-and-paste-programming)
        -   [Mushroom Management](/antipatterns/mushroom-management)
    -   [Software Architecture
        AntiPatterns](/antipatterns/software-architecture-antipatterns)
        -   [Autogenerated
            Stovepipe](/antipatterns/autogenerated-stovepipe)
        -   [Stovepipe Enterprise](/antipatterns/stovepipe-enterprise)
        -   [Jumble](/antipatterns/jumble)
        -   [Stovepipe System](/antipatterns/stovepipe-system)
        -   [Cover Your Assets](/antipatterns/cover-your-assets)
        -   [Vendor Lock-In](/antipatterns/vendor-lock-in)
        -   [Wolf Ticket](/antipatterns/wolf-ticket)
        -   [Architecture By
            Implication](/antipatterns/architecture-by-implication)
        -   [Warm Bodies](/antipatterns/warm-bodies)
        -   [Design By Committee](/antipatterns/design-by-committee)
        -   [Swiss Army Knife](/antipatterns/swiss-army-knife)
        -   [Reinvent The Wheel](/antipatterns/reinvent-the-wheel)
        -   [The Grand Old Duke of
            York](/antipatterns/the-grand-old-duke-of-york)
    -   [Project Management
        AntiPatterns](/antipatterns/software-project-management-antipatterns)
        -   [Blowhard Jamboree](/antipatterns/blowhard-jamboree)
        -   [Analysis Paralysis](/antipatterns/analysis-paralysis)
        -   [Viewgraph Engineering](/antipatterns/viewgraph-engineering)
        -   [Death By Planning](/antipatterns/death-by-planning)
        -   [Fear of Success](/antipatterns/fear-of-success)
        -   [Corncob](/antipatterns/corncob)
        -   [Intellectual Violence](/antipatterns/intellectual-violence)
        -   [Irrational Management](/antipatterns/irrational-management)
        -   [Smoke and Mirrors](/antipatterns/smoke-and-mirrors)
        -   [Project Mismanagement](/antipatterns/project-mismanagement)
        -   [Throw It over the
            Wall](/antipatterns/throw-it-over-the-wall)
        -   [Fire Drill](/antipatterns/fire-drill)
        -   [The Feud](/antipatterns/the-feud)
        -   [E-mail Is Dangerous](/antipatterns/e-mail-is-dangerous)
-   [ Refactoring](/refactoring)
    -   [Code Smells](/refactoring/smells)
        -   [Bloaters](/refactoring/smells/bloaters)
            -   [Long Method](/refactoring/smells/long-method)
            -   [Large Class](/refactoring/smells/large-class)
            -   [Primitive
                Obsession](/refactoring/smells/primitive-obsession)
            -   [Long Parameter
                List](/refactoring/smells/long-parameter-list)
            -   [Data Clumps](/refactoring/smells/data-clumps)
        -   [Object-Orientation Abusers](/refactoring/smells/oo-abusers)
            -   [Switch
                Statements](/refactoring/smells/switch-statements)
            -   [Temporary Field](/refactoring/smells/temporary-field)
            -   [Refused Bequest](/refactoring/smells/refused-bequest)
            -   [Alternative Classes with Different
                Interfaces](/refactoring/smells/alternative-classes-with-different-interfaces)
        -   [Change Preventers](/refactoring/smells/change-preventers)
            -   [Divergent Change](/refactoring/smells/divergent-change)
            -   [Shotgun Surgery](/refactoring/smells/shotgun-surgery)
            -   [Parallel Inheritance
                Hierarchies](/refactoring/smells/parallel-inheritance-hierarchies)
        -   [Dispensables](/refactoring/smells/dispensables)
            -   [Comments](/refactoring/smells/comments)
            -   [Duplicate Code](/refactoring/smells/duplicate-code)
            -   [Lazy Class](/refactoring/smells/lazy-class)
            -   [Data Class](/refactoring/smells/data-class)
            -   [Dead Code](/refactoring/smells/dead-code)
            -   [Speculative
                Generality](/refactoring/smells/speculative-generality)
        -   [Couplers](/refactoring/smells/couplers)
            -   [Feature Envy](/refactoring/smells/feature-envy)
            -   [Inappropriate
                Intimacy](/refactoring/smells/inappropriate-intimacy)
            -   [Message Chains](/refactoring/smells/message-chains)
            -   [Middle Man](/refactoring/smells/middle-man)
        -   [Other Smells](/refactoring/smells/other)
            -   [Incomplete Library
                Class](/refactoring/smells/incomplete-library-class)
    -   [Refactoring techniques](/refactoring/refactorings)
        -   [Composing Methods](/refactoring/composing-methods)
            -   [Extract Method](/refactoring/extract-method)
            -   [Inline Method](/refactoring/inline-method)
            -   [Extract Variable](/refactoring/extract-variable)
            -   [Inline Temp](/refactoring/inline-temp)
            -   [Replace Temp with
                Query](/refactoring/replace-temp-with-query)
            -   [Split Temporary
                Variable](/refactoring/split-temporary-variable)
            -   [Remove Assignments to
                Parameters](/refactoring/remove-assignments-to-parameters)
            -   [Replace Method with Method
                Object](/refactoring/replace-method-with-method-object)
            -   [Substitute
                Algorithm](/refactoring/substitute-algorithm)
        -   [Moving Features between
            Objects](/refactoring/moving-features-between-objects)
            -   [Move Method](/refactoring/move-method)
            -   [Move Field](/refactoring/move-field)
            -   [Extract Class](/refactoring/extract-class)
            -   [Inline Class](/refactoring/inline-class)
            -   [Hide Delegate](/refactoring/hide-delegate)
            -   [Remove Middle Man](/refactoring/remove-middle-man)
            -   [Introduce Foreign
                Method](/refactoring/introduce-foreign-method)
            -   [Introduce Local
                Extension](/refactoring/introduce-local-extension)
        -   [Organizing Data](/refactoring/organizing-data)
            -   [Self Encapsulate
                Field](/refactoring/self-encapsulate-field)
            -   [Replace Data Value with
                Object](/refactoring/replace-data-value-with-object)
            -   [Change Value to
                Reference](/refactoring/change-value-to-reference)
            -   [Change Reference to
                Value](/refactoring/change-reference-to-value)
            -   [Replace Array with
                Object](/refactoring/replace-array-with-object)
            -   [Duplicate Observed
                Data](/refactoring/duplicate-observed-data)
            -   [Change Unidirectional Association to
                Bidirectional](/refactoring/change-unidirectional-association-to-bidirectional)
            -   [Change Bidirectional Association to
                Unidirectional](/refactoring/change-bidirectional-association-to-unidirectional)
            -   [Replace Magic Number with Symbolic
                Constant](/refactoring/replace-magic-number-with-symbolic-constant)
            -   [Encapsulate Field](/refactoring/encapsulate-field)
            -   [Encapsulate
                Collection](/refactoring/encapsulate-collection)
            -   [Replace Type Code with
                Class](/refactoring/replace-type-code-with-class)
            -   [Replace Type Code with
                Subclasses](/refactoring/replace-type-code-with-subclasses)
            -   [Replace Type Code with
                State/Strategy](/refactoring/replace-type-code-with-state-strategy)
            -   [Replace Subclass with
                Fields](/refactoring/replace-subclass-with-fields)
        -   [Simplifying Conditional
            Expressions](/refactoring/simplifying-conditional-expressions)
            -   [Decompose
                Conditional](/refactoring/decompose-conditional)
            -   [Consolidate Conditional
                Expression](/refactoring/consolidate-conditional-expression)
            -   [Consolidate Duplicate Conditional
                Fragments](/refactoring/consolidate-duplicate-conditional-fragments)
            -   [Remove Control Flag](/refactoring/remove-control-flag)
            -   [Replace Nested Conditional with Guard
                Clauses](/refactoring/replace-nested-conditional-with-guard-clauses)
            -   [Replace Conditional with
                Polymorphism](/refactoring/replace-conditional-with-polymorphism)
            -   [Introduce Null
                Object](/refactoring/introduce-null-object)
            -   [Introduce Assertion](/refactoring/introduce-assertion)
        -   [Simplifying Method
            Calls](/refactoring/simplifying-method-calls)
            -   [Rename Method](/refactoring/rename-method)
            -   [Add Parameter](/refactoring/add-parameter)
            -   [Remove Parameter](/refactoring/remove-parameter)
            -   [Separate Query from
                Modifier](/refactoring/separate-query-from-modifier)
            -   [Parameterize Method](/refactoring/parameterize-method)
            -   [Replace Parameter with Explicit
                Methods](/refactoring/replace-parameter-with-explicit-methods)
            -   [Preserve Whole
                Object](/refactoring/preserve-whole-object)
            -   [Replace Parameter with Method
                Call](/refactoring/replace-parameter-with-method-call)
            -   [Introduce Parameter
                Object](/refactoring/introduce-parameter-object)
            -   [Remove Setting
                Method](/refactoring/remove-setting-method)
            -   [Hide Method](/refactoring/hide-method)
            -   [Replace Constructor with Factory
                Method](/refactoring/replace-constructor-with-factory-method)
            -   [Replace Error Code with
                Exception](/refactoring/replace-error-code-with-exception)
            -   [Replace Exception with
                Test](/refactoring/replace-exception-with-test)
        -   [Dealing with
            Generalisation](/refactoring/dealing-with-generalisation)
            -   [Pull Up Field](/refactoring/pull-up-field)
            -   [Pull Up Method](/refactoring/pull-up-method)
            -   [Pull Up Constructor
                Body](/refactoring/pull-up-constructor-body)
            -   [Push Down Method](/refactoring/push-down-method)
            -   [Push Down Field](/refactoring/push-down-field)
            -   [Extract Subclass](/refactoring/extract-subclass)
            -   [Extract Superclass](/refactoring/extract-superclass)
            -   [Extract Interface](/refactoring/extract-interface)
            -   [Collapse Hierarchy](/refactoring/collapse-hierarchy)
            -   [Form Template
                Method](/refactoring/form-template-method)
            -   [Replace Inheritance with
                Delegation](/refactoring/replace-inheritance-with-delegation)
            -   [Replace Delegation with
                Inheritance](/refactoring/replace-delegation-with-inheritance)
-   [ UML](/uml)
    -   [Introduction](/uml/introduction)
    -   [Basic Principles and Background](/uml/basic-principles)
        -   [Introduction to the Case
            Study](/uml/basic-principles-and-background/introduction-to-the-case-study)
        -   [Models, Views, and
            Diagrams](/uml/basic-principles-and-background/models-views-and-diagrams)
        -   [Information Systems and IT
            Systems](/uml/basic-principles-and-background/information-systems-and-it-systems)
        -   [The Models of our Case
            Study](/uml/basic-principles-and-background/the-models-of-our-case-study)
        -   [History of UML: Methods and
            Notations](/uml/basic-principles-and-background/history-of-uml-methods-and-notations)
        -   [Requirement
            Specification](/uml/basic-principles-and-background/requirement-specification)
        -   [UML 2.0](/uml/basic-principles-and-background/uml2)
    -   [Modeling Business Systems](/uml/modeling-business-systems)
        -   [Business Processes and Business
            Systems](/uml/modeling-business-systems/business-processes-and-business-systems)
        -   [One Model---Two
            Views](/uml/modeling-business-systems/one-model-two-views)
        -   [External
            View](/uml/modeling-business-systems/external-view)
        -   [The Elements of a
            View](/uml/modeling-business-systems/the-elements-of-view)
        -   [Use Case
            Diagrams](/uml/modeling-business-systems/external-view/use-case-diagrams)
        -   [Constructing Use Case
            Diagrams](/uml/modeling-business-systems/external-view/constructing-use-case-diagrams)
        -   [Activity
            Diagrams](/uml/modeling-business-systems/external-view/activity-diagrams)
        -   [Constructing Activity
            Diagrams](/uml/modeling-business-systems/external-view/constructing-activity-diagrams)
        -   [Sequence
            Diagrams](/uml/modeling-business-systems/external-view/sequence-diagrams)
        -   [Constructing Sequence
            Diagrams](/uml/modeling-business-systems/external-view/constructing-sequence-diagrams)
        -   [High-Level Sequence
            Diagrams](/uml/modeling-business-systems/external-view/high-level-sequence-diagrams)
        -   [Sequence Diagrams for Scenarios of Business Use
            Cases](/uml/modeling-business-systems/external-view/sequence-diagrams-for-scenarios-of-business-use-cases)
        -   [Internal
            View](/uml/modeling-business-systems/the-internal-view)
        -   [Package
            Diagram](/uml/modeling-business-systems/internal-view/package-diagram)
        -   [Constructing Package
            Diagrams](/uml/modeling-business-systems/internal-view/constructing-package-diagrams)
        -   [Class
            Diagram](/uml/modeling-business-systems/internal-view/class-diagram)
        -   [Constructing Class
            Diagrams](/uml/modeling-business-systems/internal-view/constructing-class-diagrams)
        -   [Activity
            Diagram](/uml/modeling-business-systems/internal-view/activity-diagram)
    -   [Modeling IT Systems](/uml/modeling-it-systems)
        -   [External View](/uml/modeling-it-systems/external-view)
        -   [The User View or \"I don\'t care how it works, as long as
            it
            works.\"](/uml/modeling-it-systems/external-view/the-user-view-or-i-dont-care-how-it-works-as-long-as-it-works)
        -   [The Elements of a
            View](/uml/modeling-it-systems/external-view/the-elements-of-view)
        -   [Use Case
            Diagram](/uml/modeling-it-systems/external-view/the-elements-of-view/use-case-diagram)
        -   [Query Events and Mutation
            Events](/uml/modeling-it-systems/external-view/query-events-and-mutation-events)
        -   [Use Case Sequence
            Diagram](/uml/modeling-it-systems/external-view/use-case-sequence-diagram)
        -   [Constructing the External
            View](/uml/modeling-it-systems/external-view/constructing-the-external-view)
        -   [Structural View](/uml/modeling-it-systems/structural-view)
        -   [Objects and
            Classes](/uml/modeling-it-systems/structural-view/objects-and-classes)
        -   [Generalization, Specialization, and
            Inheritance](/uml/modeling-it-systems/structural-view/generalization-specialization-and-inheritance)
        -   [Static and Dynamic Business
            Rules](/uml/modeling-it-systems/structural-view/static-and-dynamic-business-rules)
        -   [Elements of the
            View](/uml/modeling-it-systems/structural-view/elements-of-the-view)
        -   [Class
            Diagram](/uml/modeling-it-systems/structural-view/class-diagram)
        -   [Constructing Class
            Diagrams](/uml/modeling-it-systems/structural-view/constructing-class-diagrams)
        -   [The Behavioral
            View](/uml/modeling-it-systems/the-behavioral-view)
        -   [The Life of an
            Object](/uml/modeling-it-systems/the-behavioral-view/the-life-of-an-object)
        -   [The Elements of the
            View](/uml/modeling-it-systems/the-behavioral-view/the-elements-of-the-view)
        -   [Statechart
            Diagram](/uml/modeling-it-systems/the-behavioral-view/statechart-diagram)
        -   [Constructing Statechart
            Diagrams](/uml/modeling-it-systems/the-behavioral-view/constructing-statechart-diagrams)
        -   [Interaction
            View](/uml/modeling-it-systems/interaction-view)
        -   [Seeing What Happens Inside the IT
            System](/uml/modeling-it-systems/interaction-view/seeing-what-happens-inside-the-it-system)
        -   [Elements of the
            View](/uml/modeling-it-systems/interaction-view/elements-of-the-view)
        -   [Communication
            Diagram](/uml/modeling-it-systems/interaction-view/communication-diagram)
        -   [Sequence
            Diagram](/uml/modeling-it-systems/interaction-view/sequence-diagram)
        -   [Constructing Communication
            Diagrams](/uml/modeling-it-systems/interaction-view/constructing-communication-diagrams)
        -   [Constructing Sequence
            Diagrams](/uml/modeling-it-systems/interaction-view/constructing-sequence-diagrams)
    -   [Modeling for System
        Integration](/uml/modeling-for-system-integration)
        -   [Terminology of System
            Integration](/uml/modeling-for-system-integration/terminology-of-system-integration)
        -   [Messages in
            UML](/uml/modeling-for-system-integration/messages-in-uml)
        -   [One Model---Two
            Views](/uml/modeling-for-system-integration/one-model-two-views)
        -   [Process
            View](/uml/modeling-for-system-integration/process-view)
        -   [The Business System Model as
            Foundation](/uml/modeling-for-system-integration/process-view/the-business-system-model-as-foundation)
        -   [Elements of the
            View](/uml/modeling-for-system-integration/process-view/elements-of-the-view)
        -   [Activity
            Diagrams](/uml/modeling-for-system-integration/process-view/activity-diagrams)
        -   [Sequence
            Diagram](/uml/modeling-for-system-integration/process-view/sequence-diagram)
        -   [Constructing Diagrams in the Process
            View](/uml/modeling-for-system-integration/process-view/constructing-diagrams-in-the-process-view)
        -   [The Static
            View](/uml/modeling-for-system-integration/the-static-view)
        -   [Elements of the
            View](/uml/modeling-for-system-integration/the-static-view/elements-of-the-view)
        -   [Class
            Diagram](/uml/modeling-for-system-integration/the-static-view/class-diagram)
        -   [Constructing Class
            Diagrams](/uml/modeling-for-system-integration/the-static-view/constructing-class-diagrams)
        -   [Transforming Data from the IT System to the Message
            \"passenger
            list\"](/uml/modeling-for-system-integration/the-static-view/transforming-data-from-the-it-system-to-the-mess)
        -   [Transformation of UML Messages into Various Standard
            Formats](/uml/modeling-for-system-integration/the-static-view/transformation-of-uml-messages-into-various-stan)



[ Log in](https://sourcemaking.com/login "Log in") [ Contact
us](https://feedback.sourcemaking.com/ "Contact us"){.userecho-public
rel="nofollow"}





[![SourceMaking](/images/content-public/logos/logo-min-xs.png?id=f4a48661fc32a3f349b76a075f28594c){srcset="/images/content-public/logos/logo-min-xs-2x.png?id=34fc05750336c33b7815e231a0f227df 2x"}](/){.navigation-brand}


[![](data:image/svg+xml;base64,PHN2ZyBzdHlsZT0id2lkdGg6IDI4cHg7IGhlaWdodDogMjhweDsgZmlsbDogY3VycmVudENvbG9yOyBkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IG1hcmdpbi10b3A6IC0xNHB4OyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIiB2aWV3Ym94PSIwIDAgNTEyIDUxMiI+PCEtLSEgRm9udCBBd2Vzb21lIFBybyA2LjMuMCBieSBAZm9udGF3ZXNvbWUgLSBodHRwczovL2ZvbnRhd2Vzb21lLmNvbSBMaWNlbnNlIC0gaHR0cHM6Ly9mb250YXdlc29tZS5jb20vbGljZW5zZSAoQ29tbWVyY2lhbCBMaWNlbnNlKSBDb3B5cmlnaHQgMjAyMyBGb250aWNvbnMsIEluYy4gLS0+PHBhdGggZD0iTTM1NiA2MGw2MCAyMC02MCAyMC0yMCA2MC0yMC02MEwyNTYgODBsNjAtMjBMMzM2IDBsMjAgNjB6TTQ2NCAyMDhsNDggMTYtNDggMTYtMTYgNDgtMTYtNDgtNDgtMTYgNDgtMTYgMTYtNDggMTYgNDh6bS0yNDMuOC05LjhsMzMgNjYuOSA3My44IDEwLjcgNTkuOCA4LjctNDMuMyA0Mi4yLTUzLjQgNTIuMSAxMi42IDczLjVMMzEzIDUxMmwtNTMuNS0yOC4xLTY2LTM0LjctNjYgMzQuN0w3My45IDUxMmwxMC4yLTU5LjYgMTIuNi03My41TDQzLjMgMzI2LjggMCAyODQuNmw1OS44LTguNyA3My44LTEwLjcgMzMtNjYuOUwxOTMuNSAxNDRsMjYuOCA1NC4yem0yNi4xIDExNC40bC0yNS0zLjYtMTEuMi0yMi42LTE2LjctMzMuOS0xNi43IDMzLjlMMTY1LjYgMzA5bC0yNSAzLjYtMzcuNCA1LjQgMjcuMSAyNi40IDE4LjEgMTcuNkwxNDQgMzg3bC02LjQgMzcuMyAzMy41LTE3LjYgMjIuMy0xMS43IDIyLjMgMTEuNyAzMy41IDE3LjZMMjQyLjkgMzg3bC00LjMtMjQuOSAxOC4xLTE3LjYgMjcuMS0yNi40LTM3LjQtNS40eiI+PC9wYXRoPjwvc3ZnPg==)
Shop Now!](/store){.btn .btn-md .btn-primary .btn-featured}


-   [ [Contact us]{.caption .d-none
    .d-xl-inline-block}](https://feedback.sourcemaking.com/?show_feedback_form_private=true "Contact us"){.userecho-private
    rel="nofollow"}
-   [ [Log in]{.caption .d-none
    .d-xl-inline-block}](https://sourcemaking.com/login "Log in")
-   






-   [Design Patterns](/design_patterns)
-   [AntiPatterns](/antipatterns)
-   [Refactoring](/refactoring)
-   [UML](/uml)



-   [My account](/home)
-   [Forum](https://sourcemaking.userecho.com/){.userecho-public
    rel="nofollow"}
-   [Contact
    us](https://sourcemaking.userecho.com/?show_feedback_form_private=true){.userecho-private
    rel="nofollow"}
-   [About us](/about-us)










© 2007-2023 [SourceMaking.com](/)[ / ]{.d-none .d-md-inline}\
All rights reserved.



[Terms](/terms) / [Privacy policy](/privacy-policy)






