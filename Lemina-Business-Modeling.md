# Lemina for Business Process Modeling

<small>Copyright © 2026 Rex Young. All Rights Reserved.<br>
This paper is part of a repository governed by a [LICENSE](../LICENSE.md).<br>
Readers who obtain this file individually are bound by the same terms.<br>
Status: Working draft<br>
Contact: rex@fastmessenger.com</small>

## Abstract

Business process modeling tools such as BPMN and UML provide visual languages for describing how organizations carry out their work, yet a persistent gap separates these models from their software implementations. This paper shows that the Lemina programming model bridges that gap by providing a single vocabulary — leminas — that maps naturally onto the roles, lanes, and actors already present in business process diagrams. We introduce two complementary data concepts, Account and Event, that give business and IT teams a shared, incrementally refinable data model from the earliest stages of requirements analysis. The result is a modeling approach in which business process designs translate directly into implementable structures without the loss of fidelity that typically accompanies the handoff from analysts to engineers.

## 1. Introduction

### 1.1 Business Applications and Their Shared Trait

"Business applications" refers to enterprise applications or software solutions for information systems. They include applications that span multiple industries — content management, accounting, human resources — as well as those specific to particular domains, such as loan management or banking systems. Despite their diversity, these systems share a defining trait: they automate and improve business processes in their respective industries.

COBOL, designed in 1959, was the first programming language explicitly oriented toward business applications. Since then, many high-level programming languages have served enterprises in building applications for their industry-specific workflows. Today, modern business applications are Internet-based, typically structured in two or more tiers, and built with popular object-oriented languages like Java and JavaScript.

### 1.2 The Gap Between Process Models and Code

Businesses organize their activities as business processes and use tools such as BPMN (Business Process Model and Notation) and UML (Unified Modeling Language) to design and describe them. These notations are effective for communication among business stakeholders, but the translation from a BPMN pool diagram or UML activity diagram into running code introduces a representational gap. Roles become classes, lanes become modules, and the direct correspondence between the diagram and its implementation is lost.

The Lemina programming model [Young 2025] offers a path to close this gap. This paper demonstrates how leminas map onto the entities that business process diagrams already describe — roles, actors, and lanes — providing a continuous vocabulary from requirements through implementation.

## 2. Lemina as an Evolution Beyond OOP for Business

Each stage of programming's evolution enhances knowledge and functionality without fully replacing proven methods. High-level programming languages automate repetitive tasks atop machine code. The object model introduces a new code unit — as vital as the first cells sparking life's evolution — with logic rooted in high-level languages. The Lemina programming model advances this progression, teaching objects to collaborate and form **societies of objects**: the Lemina way of building programs.

By taking advantage of localization, one of the four core mechanisms of the Lemina model, a Lemina service can be implemented with backward compatibility to OOP languages. Therefore, the Lemina model in backward-compatible mode can be used to build business applications just like other OO languages.

However, backward compatibility is only part of the Lemina model's potential. Its real power comes from the mechanisms that make the model leap beyond the object model on programming's evolutionary path. With the Lemina model, businesses can personify leminas as employees or roles and apply their organizing skills seamlessly to leminas and employees in the early planning and design phases.

A lemina has a textual name and a list of attention names. When we name leminas with human or role names and use the naming convention of verb + noun for attention names, leminas clearly represent employees or roles in business processes. At the same time, an actual employee or role also appears as a name and a list of tasks in the business process. Thus, leminas and employees establish a one-to-one mapping relationship in the business process context.

## 3. Leminas Replacing BPMN Lanes and UML Actors

### 3.1 UML Activity Diagrams

UML's activity diagram contains activities and condition checks but does not specify who will perform them. To apply the Lemina model, the business process owner or manager refines the activity diagram into a **Lemina activity diagram** by denoting the number of leminas involved and marking each activity to its owning lemina. For example, in an order-processing workflow the activities "receive order," "validate payment," and "ship order" might be assigned to leminas named `order-clerk`, `payment-verifier`, and `shipping-team`, respectively.

### 3.2 UML Use Case Diagrams

In a UML use case diagram, actors represent external entities that interact with the system. Leminas can directly replace these actors. An actor named "Customer" becomes a lemina named `customer`; an actor named "Warehouse Manager" becomes a lemina named `warehouse-manager`. The use cases themselves correspond to attention names on the relevant leminas.

### 3.3 BPMN Pool Diagrams

BPMN's pool diagram is similar to UML's activity diagram but with two enhancements. First, a pool uses multiple **lanes** to represent employees or roles who perform the activities. Second, BPMN uses **gateways** to represent condition checks on splitting and merging. Since each lane already represents a role, leminas can directly replace lanes in the pool. All activities within a lane become the corresponding lemina's internal attention names.

### 3.4 Worked Example: Order Processing

Consider a simplified order-processing BPMN pool with three lanes:

| Lane | Activities |
|---|---|
| Customer Service | Receive order, Confirm order |
| Finance | Validate payment, Process refund |
| Warehouse | Pick items, Ship order |

Under the Lemina model, this maps to three leminas:

- **`customer-service`** with attentions: `#receive-order`, `#confirm-order`
- **`finance`** with attentions: `#validate-payment`, `#process-refund`
- **`warehouse`** with attentions: `#pick-items`, `#ship-order`

The BPMN sequence flows become messages between leminas. When `customer-service` completes `#receive-order`, it sends a message to `finance#validate-payment`. Upon successful validation, `finance` sends a message to `warehouse#pick-items`. The one-to-one correspondence between lanes and leminas, and between activities and attention names, preserves the structure of the original BPMN diagram throughout implementation.

## 4. The Account and Event Data Model

### 4.1 The Need for a Common Data Vocabulary

So far we have reviewed how the Lemina model can be used as an OO language to build business applications and model high-level business behaviors. We now turn to modeling business data in the Lemina way.

Starting from a pool that represents a business process: a pool may have one or more lanes, each representing an employee or role. Since we use a lemina to implement a lane, all activities in the lane become the lemina's internal attention names. The lemina will need two types of information to perform these activities.

The first is **administrative data** — information the lemina requires to coordinate itself, including overall status, each activity's status, and partial results. Admin data can exist at different scopes: lane, pool, and cross-pool.

The second is **domain data** — information regarding the targets to which the activities apply actions. For service businesses, the targets could be shopping carts or bank accounts. For manufacturers, the targets could be data generated by goods or manufacturing processes. This type of information typically goes beyond any single business process and belongs to the company's central business domain.

Admin data is usually private to its scope and has a one-to-one relationship with it. Domain data, on the other hand, has a many-to-many relationship with business processes: a single process may operate on multiple domain data items, and the same domain data may be used by multiple processes.

### 4.2 Account

There are hundreds, if not thousands, of industries worldwide, and companies have their own ways of doing business even within the same industry. This makes designing standard data models for each industry impossible. However, we still need a common vocabulary for discussing and working with data, because the only association between the reality of a business's operations and the functionality of its computers is the organization of its data.

A **Lemina account** is an arrangement — a group of relevant data items regarding a subject or concern. The subject could be an entity in the business domain (such as a bank account or an inventory account) or a representation of a business process's admin data (such as a place-order process account). An account is abstract until associated with a subject.

An account provides identification through two fields:

- **Account type** (or name)
- **Account instance ID** (or number)

This account-centered approach aligns business and IT people in breaking down data structures while modeling data, enabling business people to participate in data structure design from the start.

### 4.3 Event

A **Lemina event** triggers changes against account instances and carries all necessary data to complete those changes. Like accounts, events have the concepts of type and instance. An event instance specifies four fields:

- **Account type** — the type of account this event targets
- **Account instance ID** — the specific account instance to modify
- **Event type** — the kind of change being made
- **Event instance ID** — a unique identifier for this occurrence

A critical distinction between accounts and events: **events are immutable historical records** that cannot change after they occur, while accounts change throughout their lifespans as events are applied to them. An account instance without events is just a placeholder; events are what give accounts their history and current state.

### 4.4 Incremental Refinement

A useful analogy is using paper to record an account's data structure by writing the header section with identifications before details are available. This piece of paper serves as a placeholder providing referenceability. Now this account can participate in thought processes and help model business process behaviors. The detailed data items can be identified and refined incrementally throughout the modeling and design process.

## 5. Two Groups of Leminas

With business process behaviors modeled and accounts and events identified, we can assemble the full picture of how the Lemina model builds business applications.

### 5.1 Behavior Leminas

The first group consists of **behavior leminas** — leminas that perform activities and condition checks in business processes. These are the leminas that replace BPMN lanes and UML actors, as described in Section 3.

### 5.2 Account Leminas

The second group consists of **account leminas** — leminas equipped with the knowledge and business logic required to apply events to their associated accounts. For each account type, we assign a lemina and associate the lemina's attention names with the account's event types. When an event arrives, the account lemina retrieves the relevant account instance, applies the change specified by the event, and records the event as an immutable part of the account's history.

### 5.3 Many-to-Many Interaction

These two groups of leminas interact in a **many-to-many relationship**. A behavior lemina may coordinate several account leminas to complete one activity. For example, after a toy-assembling activity, the behavior lemina needs to update the inventory for the toy and the ten component parts — eleven account instances if they all belong to the same account type. Conversely, a single account lemina may receive events from multiple behavior leminas across different business processes.

By coordinating behavior leminas and account leminas, the Lemina model can model business applications more directly than past programming methods, preserving the structure of business process diagrams all the way into implementation.

## 6. Related Work

Several lines of research and practice address the gap between business process modeling and software implementation.

**BPMN execution engines** such as Camunda and jBPM allow BPMN diagrams to be executed directly, but they impose their own runtime environment and often require process models to be adapted to engine-specific constraints [OMG 2013]. The Lemina approach differs by integrating process structure into the programming model itself rather than into a separate execution layer.

**Domain-Driven Design (DDD)** [Evans 2003] shares with the Lemina approach an emphasis on aligning software structure with business concepts. DDD's bounded contexts and aggregates parallel Lemina's accounts, and DDD's domain events parallel Lemina events. However, DDD does not prescribe a direct mapping from process diagrams to code-level entities, whereas the Lemina model provides this through the lemina-to-lane correspondence.

**Event sourcing and CQRS** [Young 2010] store state changes as immutable event sequences, closely resembling Lemina's event-driven account model. The Lemina approach extends this pattern by embedding it within a broader programming model that also addresses process coordination through behavior leminas.

**The actor model** [Hewitt et al. 1973], realized in languages like Erlang and frameworks like Akka, provides message-passing concurrency similar to Lemina services. Leminas differ from actors in their explicit business-oriented naming conventions, their direct correspondence with process diagram elements, and their separation into behavior and account groups — a structure tailored for business applications rather than general-purpose concurrency.

## 7. Conclusion

This paper has shown that the Lemina programming model provides a natural bridge between business process diagrams and their software implementations. By replacing BPMN lanes and UML actors with leminas, organizations gain a single vocabulary that carries from requirements analysis through implementation without the representational gap that typically accompanies this transition.

The Account and Event data model gives business and IT teams a shared, incrementally refinable structure for working with data from the earliest stages of analysis. The separation of leminas into behavior and account groups mirrors the natural division between process coordination and data management in business applications.

Together, these contributions enable a modeling approach where business process designs translate into implementable structures with direct, traceable correspondence — closing the gap between the diagram on the whiteboard and the code in production.

## References

- [Armstrong 2007] Armstrong, J. "A History of Erlang." *Proceedings of the Third ACM SIGPLAN Conference on History of Programming Languages*, 2007.
- [Evans 2003] Evans, E. *Domain-Driven Design: Tackling Complexity in the Heart of Software*. Addison-Wesley, 2003.
- [Hewitt et al. 1973] Hewitt, C., Bishop, P., and Steiger, R. "A Universal Modular ACTOR Formalism for Artificial Intelligence." *IJCAI*, 1973.
- [OMG 2013] Object Management Group. "Business Process Model and Notation (BPMN), Version 2.0.2." OMG Document formal/2013-12-09, 2013.
- [OMG 2017] Object Management Group. "Unified Modeling Language (UML), Version 2.5.1." OMG Document formal/2017-12-05, 2017.
- [Young 2010] Young, G. "CQRS Documents." 2010.
- [Young 2025] Young, R. "Lemina: A Unified Object-Oriented Programming Model for Single-Process and Distributed Systems." TechRxiv preprint, 2025. https://doi.org/10.36227/techrxiv.175339121.11973602/v1
