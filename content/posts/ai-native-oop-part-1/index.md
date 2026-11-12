---
title: "[AI-native OOP] Part 1: The True Essence of OOP: Black Boxes and Message Passing"
date: 2026-11-10
draft: false
weight: 10
series: 
  - "AI-native OOP"
description: "Let's understand how OOP was developed and what its main principle actually is. Also, we will find out what the main purpose of OOP and what science should stand behind that."
tags:
  - OOP
  - AI-Native
  - Programming Paradigms
  - MOBBLOC
  - System Design
  - Black Boxes
  - Message Passing
  - Intent-Based Language
author: Stas Yankovskiy
showToc: true
TocOpen: false
hidemeta: false
comments: true
disableShare: false
disableHLJS: false
hideSummary: false
searchHidden: false
ShowCover: true
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
UseHugoToc: true
cover:
  image: cover.webp
  relative: true
slug: "ai-native-oop-part-1-black-boxes"
---

As many know, the first object-oriented language was Simula. Its goal was to model real systems: assembly lines, transport networks, and banks. Kristen Nygaard and Ole-Johan Dahl created this language in the late 1960s exactly for this purpose.

Today, people often criticize object-oriented programming for too many abstractions. These include bloated class hierarchies and the inheritance mechanism, which can break systems when changes happen.

Functional programming came out of the lambda calculus. Relational databases came out of Codd's relational algebra. Both started as mathematics and grew languages and engines on top of it.

OOP grew in the opposite direction. It started as an engineering practice for simulating complex systems, and it still has **no single, widely accepted scientific foundation**. 

What it has is a patchwork of theories, where each model covers its own aspect of the paradigm: type theory and Abadi and Cardelli's object calculi account for polymorphism and inheritance, coalgebra formalizes encapsulation and observable behavior, and the actor model describes message passing.

Each fragment is rigorous. None of them is the foundation, and together they do not add up to one. 

What is missing is the conceptual frame that ties them together — a frame that would tell an engineer where to draw the boundaries of a component and how to design the traffic between components.

{{< figure src="images/11-foundation-patchwork.webp" width="1600" height="900" alt="Two pavilions: one on a solid slab, one on patched blocks. Beside them, an empty dashed frame." caption="One foundation is a single slab. The other is a patchwork, and nothing holds it together." loading="lazy" >}}

In this article series, we will **reinvent object-oriented programming** from scratch. This is probably the best way to fix what is broken or works poorly.

The builders of Gothic cathedrals created complex and stable structures long before the science of material strength existed.

They used craft rules, intuition, and experience, and it worked. The invention of material strength science did not mean the cathedrals were built wrong. It just explained why they stood for centuries and allowed us to build more safely.

{{< figure src="images/02-cathedral-and-science.webp" alt="Section through a Gothic nave, with a line tracing the thrust of the vaults down into the foundations." caption="The cathedrals stood for centuries before anyone could calculate why." loading="lazy" >}}

The situation with OOP is similar. It is a powerful practice that developed for a long time **without a single scientific foundation**. I am not talking about the four "pillars" of OOP. They are not a scientific foundation, but sooner engineering practices and programming mechanisms for particular languages.

The question is: which science should be the foundation of OOP to give it a reliable base? There is no single opinion on this yet, and popular OOP books rarely mention it.

Our goal is not to call all past OOP experience "wrong." Our goal is to give it a **strong scientific foundation** so we can consciously design and grow complex systems.

Let me say right away that I will not claim the four pillars of OOP are completely false or useless. OOP works even in its current form, but modern practice shows it does not reach its full potential. I will explain why later.

The four pillars of OOP were created as engineering tools. Later, people tried to justify them with science, like type theory and category theory.

In this series, we will go in the opposite direction. First, we will define the science that is best for designing complex systems. Then, we will choose the programming tools that best apply these principles.

So, let us try to invent OOP from scratch.

## Inventing OOP from scratch

Imagine that object-oriented programming does not exist. It is simply not there. No one has invented it yet.

We have a task: to model a complex system. Let it be a toy factory. We have workshops, assembly lines, warehouses, and supply and sales departments. All of these parts interact with each other.

How would we build such a system if we did not have ready templates like "classes" and "inheritance"? How would we separate the components? How would they interact?

{{< figure src="images/03-toy-factory.webp" alt="Cutaway of a toy factory: five separate department buildings with routes drawn between them." caption="Five departments and the routes between them. The gaps matter as much as the blocks." loading="lazy" >}}

## Which science to use as a foundation?

Before we model the toy factory as a program, we need to choose a foundation. What should we build on? Which discipline should be the base of our approach to designing complex systems?

We have three best candidates:

- general systems theory,
- graph theory,
- cybernetics.

To choose, let us agree on the rules. Any science that wants to be the foundation of a programming paradigm must answer four questions:

1. **Explanatory Power**: Does it explain system behavior in motion? Not just the structure, but how the system acts over time: how it reacts, adapts, or degrades.
2. **Operationalization**: Can we translate its concepts directly into code? Abstract philosophy is useless to an engineer if it does not map to classes, interfaces, methods, and memory structures.
3. **Verifiability**: Can we test if the system works correctly? We must be able to send an input signal and check the reaction without looking inside.
4. **Distinctiveness**: Does it separate our paradigm from others? If the same foundation works for functional and logic programming, it is not a foundation for OOP. It is just general math.

Let us test each candidate against these four questions.

{{< figure src="images/04-three-candidate-sciences.webp" alt="Three plinths carrying a branching organism, a node-and-edge graph, and a sealed box with a feedback loop." caption="Systems theory, graph theory, cybernetics. Only the third is about control and communication." loading="lazy" >}}

### First candidate: General Systems Theory

Ludwig von Bertalanffy founded General Systems Theory. It teaches us to see the whole where others see only parts. It shows that system properties are not just the sum of element properties. This is a valuable view, but it is too abstract.

Let us check the criteria:

- **Explanatory Power**: It exists, but it is general. The theory says the whole is greater than the sum of its parts, but it does not explain *how exactly* parts interact to create this whole.
- **Operationalization**: It is weak. Bertalanffy created his theory for biological organisms. These are open systems that exchange matter and energy with the environment. A program has no matter or energy, only information and logic. We cannot translate "energy flow" directly into code.
- **Verifiability**: It is low. The principles are too general to build specific tests.
- **Distinctiveness**: It exists, but this is not the main point.

Systems theory gives us philosophy, not a working tool. It tells us *what* a system is, but it does not tell an engineer *how* to build it so it does not fall apart.

### Second candidate: Graph Theory

Graph theory gives a useful language to describe connections: nodes are components, and edges are messages between them. It is beautiful, clear, and mathematically strict.

But let us check the criteria:

- **Explanatory Power**: It is low for dynamics. Classic static graph theory fixes the structure of connections. But without extra tools (like Petri nets), it does not describe *how exactly* nodes process messages and change state over time. This makes it less useful for direct OOP implementation.
- **Operationalization**: It is average. A graph is easy to translate into data structures, but it does not tell us *how* nodes should behave.
- **Verifiability**: It is good for structure, but blind to behavior.
- **Distinctiveness**: Graphs are used everywhere: in networks, databases, and functional programming. This is not a unique foundation for OOP.

A graph fixes the structure but stays blind to behavior. It answers the question "who is connected to whom?" but stays silent on "what do they do and why?".

### Third candidate: Cybernetics

Against this background, it becomes clear why we must choose the third discipline. From the very start, it focused exactly on *control* and *communication*. It treats them not as side effects, but as the core of any organized system.

Cybernetics is the science of control, communication, and information processing in complex systems. Its basic principles are the **black box** and **message passing**.

{{< figure src="images/01-black-boxes-and-messages.webp" alt="Seven sealed boxes of different sizes, joined by arrows that carry small message tokens." caption="A system is black boxes exchanging messages. From the outside, that is all there is to see." loading="lazy" >}}

Let us check the criteria:

- **Explanatory Power**: It is high. Cybernetics originally studies dynamic systems with feedback. It explains *why* an object changes state, how it keeps its integrity under load, how it filters noise, and how it reacts to stimuli.
- **Operationalization**: It is excellent. Cybernetics concepts map directly to code:
    - *black box* is encapsulation,
    - *stimulus* is a method call,
    - *feedback* is a state change and sending an outgoing message,
    - *homeostasis* is the invariants the object must maintain.
- **Verifiability**: It is high. We send a known stimulus to the black box input and check the reaction without looking inside. This is a direct path to unit testing and design by contract.
- **Distinctiveness**: It is absolute. Functional programming tries to *remove* mutable state and side effects. Cybernetics, on the contrary, *makes state and environmental reaction its main topic*. This is a unique niche that separates OOP from all other paradigms.

A program is pure information and pure control. It has no matter or energy to exchange, like in Bertalanffy's biological systems. But it has signals, states, goals, and feedback. This is exactly what cybernetics studies.

### Why exactly cybernetics

The **black box** gives us a way to isolate the complexity of a single component. **Messages** give us a way to connect components without turning them into a monolith.

A graph would describe who is connected to whom. Systems theory would remind us that the factory is more than the sum of its workshops. But only cybernetics explains *how exactly* the workshops communicate, how they react to each other, and how this message passing creates the behavior of the whole system.

Cybernetics is the most complete discipline for an OOP foundation. It includes type theory, automata theory, and modern systems theory also grew out of cybernetics.

A paradigm must be described by the most general principles. For OOP, these are the principles of designing and building complex systems.

Also, cybernetics is the most understandable and accessible of all the listed sciences. The main idea of this article series is to create simple and clear principles for designing systems. These principles must be clear to both technical experts and non-technical people. Based on them, we will create a system design language. This language will serve as a specification to generate code with AI.

Thus, cybernetics offers the most direct and practical foundation for OOP among the disciplines we reviewed. It focuses on behavior and interaction, not just the internal structure of system parts.

This is the foundation on which we will build our theory.

### What is cybernetics

Cybernetics appeared in 1948 thanks to the American mathematician Norbert Wiener. He noticed that control processes in living organisms, machines, and society follow the same laws.

His book "Cybernetics: Or Control and Communication in the Animal and the Machine" laid the foundation for studying any complex systems, from biological cells to economic markets.

The main idea of cybernetics is this: to understand a complex system, you do not need to know what is inside. You only need to observe how it reacts to external inputs and what it outputs. This is the "black box" principle.

{{< figure src="images/05-black-box-anatomy.webp" alt="One sealed box with a stimulus arrow going in, a response arrow coming out, and a feedback loop returning underneath." caption="Stimulus in, response out, feedback around, state inside. The boundary is the protocol, not the field list." loading="lazy" >}}

### Why cybernetics is the foundation of OOP

Because object-oriented programming solves the same problem as cybernetics: how to design a stable system from many components that interact with each other.

In cybernetics, a system is a set of black boxes exchanging messages. In OOP, a system is a set of objects exchanging messages. The difference is only in the terms, not in the essence.

When you design an object as a black box, you automatically get:

- **Autonomy**: The object manages its own state.
- **Loose coupling**: Objects do not know each other's internals.
- **Stability**: Changing the internal implementation does not break the system.

This is why cybernetics is not just a metaphor, but a strict scientific foundation for OOP. It gives us not just a set of rules ("make fields private"), but a whole methodology for designing complex systems.

We can model the departments of our toy factory as black boxes. Each department accepts a specific set of messages.

Now imagine the warehouse. It is also a black box. It receives a message from the supply department: "Materials are delivered." The warehouse decides itself how to place them, which cell to use, and how to update the records. Then it sends a message to the production department: "Materials are available for use."

The production department is another black box. It receives a message: "You can start producing a batch of 50 toys." Inside, it plans the schedule, assigns tasks to workers, and controls quality. Then it sends a message to the sales department: "The batch is ready for shipment."

{{< figure src="images/06-departments-message-chain.webp" alt="Supply, warehouse, production and sales drawn as four sealed buildings, with messages passing along the chain." caption="Only the envelopes cross the gaps. Nothing inside a building is visible to the next one." loading="lazy" >}}

### Why this works

Notice that no department looks inside another. The supply department does not know how the warehouse stores materials. The warehouse does not know how the production department plans the schedule. Each department is an autonomous unit that manages its own internal processes.

What happens if the supply department decides to change suppliers? Nothing. The other departments will not even notice, because the interaction protocol did not change. The supply department still accepts material requests and returns delivery messages.

What happens if the warehouse moves to a new accounting system? Nothing. The supply department still sends delivery messages, and the production department still receives material availability messages.

This is the core of the cybernetic approach: **every system component is an autonomous black box that receives messages, manages its own internal state, and returns results**.

### Transition to the goal of OOP

To see how these abstract cybernetic principles work in practice, let us return to our toy factory.

What did we just do?

We did not just "model" a factory. We did not just "manage complexity." We **designed a system**. We separated the components (departments), defined their interaction (messages), and ensured the autonomy of each component (black boxes).

We created a complex system from simple, independent parts. And this system is stable to changes: we can change the internal implementation of any department without breaking the whole system.

This is the main goal of object-oriented programming: **designing, building, and growing complex systems**.

It is not modeling (we created entities that do not exist in reality, like the "supply department" as an abstract component). It is not managing complexity (that is a result, not a goal). It is exactly system design: separating components, defining their interaction, and ensuring stability.

> **OOP as a paradigm is inseparable from building systems.** This paradigm is meant to build systems, not just to manage complexity.

And this is why cybernetics, with its principle of black boxes and messages, is the ideal scientific foundation for OOP. It gives us not just a set of rules, but a whole methodology for designing complex systems.

> So, from here on, we accept this as a postulate: **the main goal of OOP is designing, building, and growing complex systems**. We will use this postulate to formulate the new scientific foundation of OOP.

{{< figure src="images/16-goal-design-build-grow.webp" width="1600" height="900" alt="Three stages of the same campus: a flat plan, blocks under scaffolding, then a larger campus with new wings." caption="Design, build, grow. The model does not change as the system gets bigger." loading="lazy" >}}

Now let us look at how the four pillars of OOP appeared and why they cannot serve as its foundation.

## The rise and fall of the four pillars of OOP

Simula is considered the first truly object-oriented language. It was developed to model complex real systems, like assembly lines, transport systems, banks, and seaports.

Simula laid the foundations for data encapsulation and inheritance. The final form of the "four pillars" appeared in the works of the 1980s and 1990s.

Grady Booch formulated these principles most clearly for the first time in his book "Object-Oriented Analysis and Design with Applications".

Here is what he writes in this book about the essential parts of object-oriented programming:

> For all things object-oriented, the conceptual framework is the object model.
> There are four major elements of this model:
>   1. Abstraction
>   2. Encapsulation
>   3. Modularity
>   4. Hierarchy

So, according to Grady Booch, OOP cannot exist without these four principles.

Let me explain right away that hierarchy means inheritance.
The only modern principle missing here is polymorphism.
Modularity is mentioned instead, but this is still one of the first attempts to formulate the foundation of OOP.

What science is the foundation of these four principles? Sadly, he does not explain.

Almost no one explains what science is the foundation of OOP.
But we will fix this soon and offer a scientific foundation for OOP.

Let us start by criticizing inheritance. Today, everyone criticizes inheritance in OOP.

## What is wrong with inheritance

From my own practice, the biggest problem with inheritance is this: if we change the parent class, the whole chain of child classes easily breaks. This creates problems. But there is a much more serious problem, and it is this:

> Many real and virtual systems (like social networks or microservices) are better described as graphs, not strict trees, because entities in them often interact with many other entities.

{{< figure src="images/07-inheritance-tree-vs-graph.webp" alt="A cracked three-level hierarchy of blocks on the left; an even mesh of nine identical cubes on the right." caption="Change the parent and the tree shifts. The mesh has no parent to break." loading="lazy" >}}

For example, social networks, the World Wide Web, the brain, and neural networks are graphs.

Trees are a special case of a graph, but real and virtual systems are rarely built exactly as trees.

The problem is deeper: most real and virtual systems are not trees. They form graphs because one entity interacts with many other entities in the system.

Classic theory says OOP is impossible without inheritance. There were attempts to fix this, and the "composition over inheritance" principle was invented. Still, the four pillars of OOP were not changed because of this.

People still think inheritance is an essential part of the four pillars. At the same time, many articles and conference talks advise against using inheritance and recommend using composition.

Inheritance might have narrow uses, but we can hardly say it is an essential part of OOP. It can be useful, but we cannot call it an essential part of OOP.

We cannot do this because even in classic object-oriented languages like Java or C#, you can easily write a large system using only composition, without inheritance. You can safely use dependency injection and do fine without inheritance.

For example, the Go language shows that you can successfully design complex systems using composition and interfaces without using the classic inheritance mechanism at all. This questions its status as an essential pillar of OOP.

Again, inheritance can be useful in some cases, but it is easy to prove it is not an essential part of OOP.

## Let us criticize abstraction

People usually consider abstraction the main principle of OOP. But all paradigms do this: procedures, types, and functions are all ways to hide details. So abstraction does not explain how the object approach is different from any other. This principle exists in every paradigm, and it is not unique to OOP.

> Abstraction exists in almost every programming paradigm and is not unique to OOP.

Let me repeat. Abstraction is part of OOP, but it is not a unique principle that separates OOP from functional, procedural, or any other paradigms.

When we formulate the fundamental principles of a paradigm, we must find the exact principles that uniquely separate it. We will do this later in this article.

## Polymorphism — close, but not quite

Polymorphism is when different objects answer the same call in different ways. A circle object calculates area using the radius. A rectangle object uses the sides. A composite figure adds the areas of all its parts. The call is the same, but the behavior is different.

{{< figure src="images/12-polymorphism-same-message.webp" width="1600" height="900" alt="Three boxes marked circle, rectangle and composite shape get the same message and return different answers." caption="The message is identical. What makes it identical for all three is the real question." loading="lazy" >}}

A small spoiler: this is indeed one of the core principles of OOP. But polymorphism is only a small part of something bigger and more important. Polymorphism itself does not answer *why* different objects can answer the same call at all, and *what* makes this call "the same" for all of them. The answer to this question is the true foundation of the object approach, and we will get to it soon.

## Encapsulation — our last hope

Encapsulation is truly the principle that separates OOP from other paradigms. Procedural programming also abstracts. Functional programming also abstracts. But only the object approach says: "here is a boundary you cannot cross." This is the essence: hide the internals, leave only the contract. But here is what is interesting. When we say "encapsulation", we usually think about private fields and getters.

This is only a surface sign of something deeper. Next, we will look at OOP from a different scientific view. We will not look through classes and hierarchies, but through how objects interact at all.

From this new view, encapsulation will turn out to be not just "data hiding", but something more fundamental. It is what makes objects truly independent. We will rename this principle to match the new foundation, and you will see it works very differently from what we are used to.

## The four pillars of OOP are not a system

If you can remove at least one of the four pillars, they are not a system. They do not form a complete set of principles. They do not flow from each other and do not follow each other.

But regarding these four principles: they are not just a broken system. They also contradict each other.

Here is a simple Java example:

```java
class User {
    protected String password; // had to open for child classes
}

class Admin extends User {
    public void resetPassword() {
        password = "12345"; // direct access to parent field
    }
}
```

If you have not used Java, `protected` means we opened access to this property for everyone who inherits from `User`.

This simple example shows that at least two of the four properties contradict each other. Yet somehow, these four pillars are still presented as the foundation of OOP.

Encapsulation says "hide fields" (make them `private`), but inheritance requires opening them (`protected`) so child classes can work. One principle says close, the other says open.

{{< figure src="images/08-four-pillars-not-a-system.webp" alt="A portico with four columns and a broken entablature; a fracture runs between two of the columns." caption="Encapsulation says close, inheritance says open. The fracture runs between them." loading="lazy" >}}

> Important note: when we formulate new principles for OOP, we do not ban the use of any of the four traditional pillars, including inheritance. The role of each of these four mechanisms will be clarified in the next article and will become part of broader new principles.

> When we define the foundation of any paradigm, we must choose the most general principles. Encapsulation, polymorphism, inheritance, and abstraction are specific engineering tools derived from practice and from languages like C++, Java, and Simula. They are not the most general and abstract principles. They are specific programming tools. The new foundation of OOP, which we will formulate in the next article, represents more general scientific principles. The four pillars of OOP are implementations of these principles. There are more such implementations. For example, the famous "composition over inheritance" principle is one way to implement a black box using composition instead of inheritance.

### The cargo cult of the four pillars

A cargo cult is when people copy the outer signs of something successful without understanding how it really works.

Sadly, the four pillars are somewhat of a cargo cult. The most interesting part is that the Smalltalk language already existed back then. It clearly had a message passing mechanism, but it was not mainstream.

Simula was more often the example to copy, because it focused on inheritance. Simula influenced the foundation of OOP and its principles much more than Smalltalk.

The industry took the "four pillars" from Grady Booch's works and turned them into a dogma. Booch mostly *described* existing practice, heavily influenced by C++.

Let me note that Grady Booch is an outstanding scientist and programmer, and one of the inventors of UML. He certainly relied on what was available in object-oriented programming at that time.

We must understand that it was the late 1980s and early 1990s. The foundation of OOP was just being formulated. There was not much experience in using object-oriented languages, and there was not the variety of languages we have today.

Today, much has changed. Languages like Go and Rust offer a different approach to OOP. We can formulate a new foundation for OOP based on accumulated experience.

In the past, some people believed the Earth was flat. To fully prove the Earth is a sphere, people had to fly high above it in a rocket and be 100% sure.

Now we can also rise high above the accumulated experience in programming and computer science to formulate a new approach to object-oriented programming.

But, as said at the beginning, we must not only consider all past experience to formulate a new foundation. We must also give a scientific foundation to the OOP paradigm, which we will do next.

## The main principle of OOP

### Two paths of OOP

Before we define the main principle of OOP, we need to understand what approaches to object-oriented programming exist at all.

When the first object-oriented language, Simula, appeared, one of its key ideas was inheritance and object hierarchy. But with the Smalltalk language, the world saw a new view of OOP: message passing between objects.

{{< figure src="images/09-two-paths-simula-smalltalk.webp" alt="A fork in a road: one branch leads to a pyramid of blocks marked Simula, the other to cells exchanging messages marked Smalltalk." caption="The industry paved the left branch, and cast the four pillars from it." loading="lazy" >}}

We can say these are two different philosophical paths that accidentally got the same name:

1. **The Simula Path (Data and Hierarchy).** The focus is on *what the object is*. This is the world of classification, inheritance trees, and shared fields. Here, an object is basically an improved data structure (struct) with attached functions. This path, through C++ and Java, became the industry standard and created the dogma of the "four pillars".
2. **The Smalltalk Path (Behavior and Messages).** The focus is on *what the object does*. Here, an object is an independent biological cell or network node. It has no "internals" you can access directly. You can only "negotiate" with it by sending a message. Inheritance is secondary or missing here. The main thing is the communication protocol.

In the end, our industry chose Simula and hierarchy with inheritance as the foundation of OOP, instead of the flexibility of Smalltalk and message passing. Message passing is possible in any language, even in Java and C++ through method calls. But here, the foundation and the approach to system design are what matter.

The problem is that the **four pillars, which do not form a connected system** and sometimes contradict each other, lie at the very foundation. This is a big problem.

Another problem is this: if inheritance is an essential part of OOP, we view all systems through hierarchy. But as said before, system parts are rarely built in a hierarchy. Usually, systems form a random graph, not a tree with a strict hierarchy.

> Usually, systems form a random graph, not a tree with a strict hierarchy.

But it is important that the foundation of OOP strongly influences software system design. This is our starting point. If we start from the four pillars, we do not get a complete system of principles.

Message passing between black boxes is a complete system of principles. First, it is easy to keep in mind and easy to visualize. Even a three-year-old child can understand black boxes sending messages to each other. This also strongly influences system design.

When you keep the four pillars in mind, you think about hierarchy, reusability, and sometimes unnecessary abstraction layers.

With message passing, the focus is on external interaction between objects. This should be the center of system design: how components interact with each other is the most important thing in system design, not what hierarchy they form.

> This should be the center of system design: how components interact with each other is the most important thing in system modeling, not what hierarchy they form.

If we design a factory with five departments (accounting, marketing, production, sales, and supply), we do not care much about their hierarchy at first. Overall, they are more or less self-sufficient units.

What matters is the interaction between them, what signals and messages they send to each other when they interact. This should be the center of system design. We should start from this.

Or take another example: a monolith that we have to split into microservices when it grows too big.
A microservice is exactly a black box that communicates with messages.

If you think in these terms from the start, you do not need to "transition" from a monolith to microservices. You just scale up the same model.

One object, ten objects, a hundred objects—the principle is the same. But if you think in hierarchies, everything breaks when you move to microservices, because inheritance does not work over a network.

{{< figure src="images/10-one-ten-hundred-boxes.webp" alt="The same cube drawn at three scales, labeled 1, 10, and 100, each set joined by message lines." caption="A microservice is the same black box. You scale the model; you don't rewrite it." loading="lazy" >}}

> If we put message passing between black boxes at the center of OOP, we already think at the paradigm level about how system components interact with each other, not what hierarchy they are in.

A strict hierarchy built on deep inheritance often creates strong coupling. This makes it hard to break down a monolith into independent microservices.

### Black boxes and OOP

Black boxes that communicate with each other through messages are based on a science: cybernetics.

Yes, cybernetics is exactly what divides a complex system into black boxes and the messages these black boxes receive and send.

To make this sound less like an abstract metaphor, let us look at the definition. Norbert Wiener, the founder of cybernetics, defined it as "the science of control and communication in the animal and the machine". W. Ross Ashby developed this idea. He focused on studying systems not through their internal structure, but through their **behavior**: their reaction to external inputs and their produced outputs.

In cybernetics, a system is viewed as a **"black box"**. We do not need to know what is inside (a mechanism, an algorithm, biological tissue) to interact with it.

**But wait, you might say, is this not just encapsulation?**

And you would be right. On a surface level, it really looks like encapsulation. But here lies the key difference between a *principle* and a *scientific foundation*.

**Encapsulation in the traditional sense is a technical tool.** It is a rule: "make fields private, add getters and setters." It is an instruction on *how* to hide data. But it does not answer the questions: *why* do we do this? *What* boundaries should we draw? *How* should objects interact to keep the system stable?

This is why we see code where everything is formally "encapsulated" (fields are private), but the system is built on deep inheritance. Classes are tightly connected through hierarchies, and changing a base class breaks dozens of child classes. This is "encapsulation without understanding"—a cargo cult.

**Cybernetics is not about hiding data. It is about system behavior.**

When we take cybernetics as a foundation, we do not just say "hide fields". We say:

- Every object is an **autonomous unit** that manages its own state.
- Objects interact only through **messages** (protocols), not through direct access to internals.
- The boundaries of an object are defined not by "which fields are private", but by **which messages it accepts and which answers it returns**.
- The system stays stable because changing the internal implementation of an object does not break those who interact with it (as long as the protocol is kept).

**Encapsulation is a result of the cybernetic approach, not its essence.**

{{< figure src="images/17-encapsulation-is-a-result.webp" width="1600" height="900" alt="A sealed block with messages at its ports, an arrow, then a smaller block with a plain padlock." caption="The lock arrives on its own. Start from the lock and all you get is locked data." loading="lazy" >}}

When you design an object as a "black box" (according to cybernetics), encapsulation happens automatically. You simply cannot open the internals because the object is an autonomous unit, not a data set with methods.

But if you start with encapsulation (as a principle), you might get "encapsulated data", but design a system through inheritance hierarchies. Objects will be tightly connected, and changing one class will break the whole system.

**Cybernetics gives us not just a rule to "hide data", but a whole scientific foundation for designing stable systems:**

- Ashby's Law of Requisite Variety (the object protocol must match the complexity of the environment).
- The feedback principle (objects react to changes in the system).
- The concept of homeostasis (the system keeps stability during changes).

This is why we take cybernetics, and not just "encapsulation". Because encapsulation without understanding *why* and *how* objects should interact is just a technical tool. Cybernetics is the science of how to build stable systems from autonomous components.

The black box principle is a broader and more universal system design principle. You can apply it anywhere, not just in programming, unlike encapsulation. Encapsulation is just a mechanism, a narrower mechanism, not a principle.

We only care about the **interaction protocol**: what signals (messages) the box accepts, how it changes its internal state, and what answers (messages) it sends back. If the internal structure changes, but the input and output protocol stays the same, nothing changes for the external system.

> This simple idea should be the foundation of object-oriented programming, and it immediately gets a clear scientific foundation because of this.

To understand how this works in practice, let us imagine a normal **coffee machine** in an office.

In cybernetics, a coffee machine is an ideal **"black box"**. When you want coffee, you do not open its back cover to personally check the water level, manually pour beans into the grinder, or turn on the heating element. It is much simpler: you send the machine a **message** (you press the "Cappuccino" button) and provide a resource (a coin or a card).

{{< figure src="images/13-coffee-machine-black-box.webp" width="1600" height="900" alt="A sealed coffee machine: message and coin in, a cup or an Add water card out." caption="You never open the back panel. You send a message and read the reply." loading="lazy" >}}

Then the magic of cybernetics happens: the machine *itself* decides how to process this message. It checks the milk level, heats the water to the right temperature, and whips the foam. You do not need to know how its internal mechanism works. You only care about the result: it either gives you a cup of coffee (a successful answer), or writes "Add water" on the screen (an error message).

This is exactly the essence of the cybernetic approach in programming: **an object must be a black box that receives messages, manages its hidden state, and returns a result**. This allows us to change the internal logic of the object as much as we want, without breaking the rest of the system that interacts with it.

### Alan Kay's OOP

One of the developers of the Smalltalk language, Alan Kay, took this idea as a foundation. Here is what he said about object-oriented programming:

> The big idea is "messaging"

Moreover, even Steve Jobs, who was not a programmer, understood this:

> Here’s an example: If I’m your laundry object, you can give me your dirty clothes and **send me a message** that says, “Can you get my clothes laundered, please.” I happen to know where the best laundry place in San Francisco is. And I speak English, and I have dollars in my pockets. So I go out and hail a taxicab and tell the driver to take me to this place in San Francisco. I go get your clothes laundered, I jump back in the cab, I get back here. I give you your clean clothes and say, “Here are your clean clothes.”

{{< figure src="images/14-laundry-object.webp" width="1600" height="900" alt="A sealed crate takes crumpled clothes and a message, returns folded clothes and a reply." caption="Jobs's laundry object. The taxi, the dollars and the best laundry in San Francisco stay inside." loading="lazy" >}}

Alan Kay did not say he took cybernetics specifically as the foundation of OOP. He was inspired by biological cells, considering biology his source of inspiration. Any biological organism is a complex system, and cybernetics can study such systems, just like systems theory. Kay, the creator of Smalltalk, only highlighted a special case of a complex system: the interaction between biological cells.

Now we will explicitly take cybernetics as the foundation of object-oriented programming. We will use this to formulate new principles going forward.

## Why exactly AI-native OOP?

Why is the article series called **AI-native OOP**?

Regarding artificial intelligence, we are presenting a simple set of principles for designing complex systems to the whole IT community. These principles will be clear not only to programmers, but also to analysts, testers, and managers.

Because of this, all of them can take part in designing complex systems. Today, with the help of artificial intelligence, not only programmers can write code. At least, almost anyone can create prototypes of software systems.

Systems thinking, along with the ability to design and understand complex systems, is a skill of the 21st century. It is a skill of the AI era, because today AI already knows how to program quite well and build the systems humans describe.

{{< figure src="images/15-spec-to-code.webp" width="1600" height="900" alt="A sheet with a box-and-message diagram, an arrow, and a sheet with a handwritten code skeleton." caption="The drawing is the specification. The code is what the machine writes from it." loading="lazy" >}}

We are left with system design in general, especially in business and enterprise applications. The new principles of object-oriented programming, formulated in the next article based on black boxes and message passing (that is, cybernetics), will help with this.

In my view, cybernetics is more relevant today than ever as a science of complex systems. At the same time, it gives simple and clear tools for this. These tools will be clear to anyone, including non-technical specialists like managers, accountants, economists, systems analysts, and CEOs.

## Conclusion

In this article, we did the following:

1. We derived the postulate that the main goal of OOP is designing, building, and growing complex systems (not just modeling them).
2. We understood why the four pillars (encapsulation, polymorphism, inheritance, and abstraction) cannot serve as the foundation for OOP.
3. Starting from the main goal of designing, building, and growing complex systems, we arrived at the scientific foundation of OOP: cybernetics.
4. The main principle of cybernetics when studying complex systems is dividing the system into "black boxes" and the messages they receive and send.

## Sources
1. [The Development of the SIMULA Languages, 1978](https://www.cs.tufts.edu/comp/150FP/archive/kristen-nygaard/hopl-simula.pdf )
2. Grady Booch. Object-Oriented Analysis and Design With Applications, 1993
3. Ashby, W. R., _An introduction to cybernetics_. Chapman & Hall, 1957
4. [Steve Jobs in 1994: The Rolling Stone Interview ](https://www.rollingstone.com/culture/culture-news/steve-jobs-in-1994-the-rolling-stone-interview-231132/)
5. [Alan Kay On Messaging](https://wiki.c2.com/?AlanKayOnMessaging)
