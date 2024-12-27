# OOP is just a mental model

Let’s face it: every time we write code in a “nice” language or follow a “clean” pattern, we’re really just creating illusions for ourselves. Behind all those lofty classes, pure functions, or carefully engineered microservices, there’s only machine code. In other words, the CPU doesn’t care whether your “rectangle” is a subclass of “shape,” or if you elegantly declared a function with no side effects. From the processor’s perspective, it’s all just instructions, addresses, and data moving around.

Do you remember having this experience? you simply sat at your computer, wrote a program in 1 or 2 files, tested it, and felt the joy of having created something useful that worked "just like that". You probably also started playing with it and started thinking of ways it could be more fun and useful... you had created something that _worked_, and it was marvelous!

That’s not to say these illusions are a waste of time. Quite the opposite. Code organization paradigms—whether procedural, object-oriented, or functional—are the mental scaffolding we use to keep from going insane. Each helps us decide where to place logic, how to handle data, and what to compose and reuse. If we tried to manage a system of any considerable size in raw assembly, we’d never get anything done. So yes, these paradigms are all imaginary—and that’s the point.

In the sections below, we’ll explore a wide array of these “mental models” (i.e., paradigms) and the subtle ways they shape both our design process and our final applications. We’ll also look at the overhead these abstractions can introduce, and why, despite the performance costs, we willingly embrace them.

---

## Section 1: Revisiting the “Big Three”

### 1. Procedural (Scripts)

#### What It Is
Procedural programming is the simplest form of code organization. You write routines—functions, subroutines, or scripts—that execute in a top-down sequence. It’s straightforward to understand: you do step A, then B, then C. This approach is great for small or medium tasks where advanced abstractions aren’t necessary. However, once projects become large and complex, everything can end up in one long chain of commands, and managing them grows unwieldy.

### 2. Object-Oriented Programming (OOP)

#### What It Is
Object-Oriented Programming groups code into classes (blueprints) and objects (instances), often leveraging inheritance and polymorphism. It provides a clear way to decide where logic should live, typically inside the objects themselves, and encourages reusability and composition through well-designed class structures.

#### The Real World vs. Code
OOP is still a mental tool rather than a perfect reflection of reality. Although we might think a square should be a subclass of a rectangle, real-world math suggests one thing, while OOP implementations may complicate the “is-a” relationship. **A rectangle has properties Width and Height, while a square only has one: the side Length.** Should Square inherit from Rectangle or the other way around? This discrepancy highlights the fact that code hierarchies are abstractions of convenience, not absolute truths. Think this is an "exception"? Try ellipsis and circle. These examples are very intentionally framed in mathematical concepts (archetypical hierarchies).

#### Trade-Offs
While OOP can bring clarity and reuse, overusing inheritance or virtual dispatch sometimes impairs performance. It might also feel like overkill for simpler tasks, so you have to strike a balance between the benefits of organization and the cost of complexity.

### 3. Functional Programming

#### What It Is
Functional Programming organizes code around pure functions that avoid side effects and mutable state. Each function is a clear input-to-output mapping, minimizing hidden interactions and making reasoning about your code simpler.

#### Why It’s Useful
The ability to compose smaller functions—like `map`, `filter`, and `reduce`—often leads to more concise code once you’re familiar with the style. It can also reduce bugs caused by inadvertently sharing or changing state in multiple places.

#### Potential Drawback
For those accustomed to imperative or OOP styles, functional programming can require a mindset shift. Strict immutability may introduce performance overhead in certain scenarios, such as large data structures or real-time constraints.

---

## Section 2: Additional Paradigms

Below are paradigms that go beyond the traditional “big three.” Each offers distinct ways to structure logic, data, or both.

### 2.1 Logic Programming (Prolog)

#### Key Idea
Logic programming involves stating facts and rules about your domain, then querying the system to see how those facts and rules unify. The system, rather than the developer, figures out how to reach an answer.

> Here’s a tiny Prolog program about family:

```prolog
parent(john, mary).
parent(mary, susan).

ancestor(X, Y) :- parent(X, Y).
ancestor(X, Y) :- parent(X, Z), ancestor(Z, Y).
```

> We have two facts: “john is a parent of mary” and “mary is a parent of susan.” We also define a rule for `ancestor(X, Y)`: either X is a parent of Y, or X is a parent of Z and Z is an ancestor of Y. When you query `?- ancestor(john, susan).`, Prolog says “true” because John → Mary → Susan. You didn’t write loops or function calls; you just stated truths and let Prolog do the work.

### 2.2 Declarative Paradigms

#### What They Are
Declarative paradigms focus on what the result should be rather than how to achieve it. HTML and CSS describe layout and styling, leaving the browser to handle rendering logic. SQL specifies the data you need and trusts the database engine to decide on the query execution plan.

### 2.3 No-/Low-Code Platforms

#### How They Work
No-/low-code platforms let you build applications visually, using drag-and-drop flows or forms, without writing much (or any) code. Under the hood, these tools often generate more traditional paradigms—like OOP or procedural code—but from the user’s perspective, the organization revolves around blocks and business logic instead of classes or functions.

### 2.4 Relational Model (Codd, Date, etc.)

#### Key Idea
The relational model defines data as relations, not just “tables” in the casual sense. This concept was pioneered by E.F. Codd and further developed by researchers like C.J. Date. Data Definition Language (DDL) can be declarative, describing schemas and constraints, while Data Manipulation Language (DML) can be imperative if we consider stored procedures or triggers. Although the relational model focuses on data structure, real-world implementations often blend declarative statements (SQL queries) with procedural elements.

### 2.5 Graph/Pipeline-Based Approaches

#### Single Concept
Here we merge various “network-based,” “event-based,” or “actor/agent-based” ideas into a single conceptual umbrella, where code is organized as nodes and edges. Nodes do processing, and edges represent data flows or message passing. Microservices using HTTP or gRPC fit here, as do event-driven systems that react to signals or messages rather than running in a strict sequential order. Actor models like Erlang or Akka also follow this node-and-edge pattern, allowing asynchronous message-based communication for concurrency.

### 2.6 DSLs (Domain-Specific Languages)

#### What They Do
DSLs provide specialized syntaxes tailored to a particular domain (think Regex for pattern matching or LaTeX for document markup). Internally, DSLs typically compile or interpret down into one of the standard paradigms, but from the user’s point of view, it feels like an entirely different mental model.

---

## Section 3: Architectural and Design Patterns, Etc.

**Design Patterns** first gained mainstream attention through the “Gang of Four” (Gamma, Helm, Johnson, and Vlissides) in their book _Design Patterns: Elements of Reusable Object-Oriented Software_, which documented common solutions to recurring problems in software design. Later, Martin Fowler’s work on enterprise architecture patterns expanded the concept, covering broader concerns like database interactions, distribution, and more. Whether you’re writing pure OOP classes, functional pipelines, or event-driven actors, these patterns can drastically shape how you organize logic, data flows, and responsibilities. A pattern such as Strategy or Observer might slot right into functional code just as easily as it would in a deeply object-oriented system, while higher-level patterns like Model-View-Controller or Layers can guide how you split your codebase into separate modules or services. In essence, design and architectural patterns offer tried-and-true approaches to structuring code and components in ways that transcend any single paradigm, acting as a shared vocabulary for developers to tackle complexity together.

Whether you’re working in a purely object-oriented style, a functional setting, or a more pipeline- or graph-based paradigm, patterns act as a framework for organizing your code in a specific way. In OOP, you organize the code into specific classes and interfaces, depending on the pattern, to define interchangeable behaviors, whereas in a functional environment, you could achieve the same effect by passing around different functions. Even in pipelines, you could organize nodes within the flow to implement a specific pattern. 

These however introduce a new, higher layer of abstraction. They also introduce new ways of organizing the code: they are "organizing the code organization" (meta-organizing?): this time you aren't organizing lines of code into classes or functions, you're organizing classes and functions themselves following certain principles.

### Other Examples

#### 3.1 Aspect-Oriented Programming (AOP)
AOP often extends OOP by weaving in cross-cutting concerns, such as logging or security, at compile or runtime. You still have classes and methods at the core, but aspects intercept or inject behavior in places that otherwise require repetitive boilerplate.

#### 3.2 ECS (Entity-Component-System)
ECS is common in game development and breaks objects into data-only components plus separate systems acting on them. Entities are merely IDs referencing those components. While ECS can still be implemented with OOP constructs, it shifts thinking away from inheritance hierarchies toward a composition-first mindset. A single “PlayerEntity” might have a PositionComponent and a HealthComponent, with systems like MovementSystem or RenderingSystem operating on any entity that matches certain component sets.

---

## Inefficiencies, Overheads, and the CPU’s Point of View

Although each paradigm simplifies our development experience, the compiler or interpreter eventually reduces everything to machine instructions. Complex inheritance hierarchies can impede inlining, and splitting a system into microservices introduces network overhead from encoding, sending, and decoding messages. A single in-process function call would be more efficient from the CPU’s perspective, but we consciously sacrifice some performance in exchange for modularity, fault isolation, and easier collaboration. DSLs, similarly, require their own interpreters or compilation steps. 

We accept these overheads because they provide mental frameworks for large-scale applications. Even if microservices or node-and-edge pipelines seem artificial, they let us compartmentalize responsibilities and reason about an otherwise gigantic, monolithic codebase. The performance cost is usually worth it when weighed against the benefits in maintainability and clarity.

---

## Conclusion

All these paradigms—whether procedural, OOP, functional, logic-based, relational, declarative, no-/low-code, graph/pipeline-based, AOP, or ECS—exist to help you cope with complexity. They are not formal mathematical models you must follow; they’re convenience abstractions that let you and your teammates speak a common language about the code. Before you add another layer or create a deeper hierarchy, ask yourself: does this really make sense for the problem at hand? Could you have written those ten classes, sprawling across two microservices, in a single C file with twenty lines of code instead? Questioning the value of every abstraction is a necessary discipline. After all, every additional structure you introduce is something you’ll have to maintain, debug, and justify, so make sure it serves a clear purpose.


# Food for thought
Will AI need all these abstractions?

Appendix I: [Real Programmers wrote in machine code.](http://www.catb.org/jargon/html/story-of-mel.html)
