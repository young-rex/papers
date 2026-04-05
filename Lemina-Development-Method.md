# Lemina Development Method

<small>Copyright © 2026 Rex Young. All Rights Reserved.<br>
This paper is part of a repository governed by a [LICENSE](../LICENSE.md).<br>
Readers who obtain this file individually are bound by the same terms.<br>
Status: Working draft<br>
Contact: rex@fastmessenger.com</small>

## Abstract

Business application development suffers from fragmentation: requirements live in wikis, data structures in schemas, business logic in specifications, and source code in repositories — each managed by different tools and different people. This paper presents the Lemina Development Method, a practice built around three techniques: all-in-one Markdown documents that unify requirements, data structures, business logic, and source code in a single file; a Git repository that manages these documents with pull requests, bringing requirements management into the same workflow as code; and a build tool that assembles the documents into a runnable model implementation for manual verification and automated testing. Together, these techniques enable business people to develop functional reference implementations — complete in functional requirements, free of nonfunctional concerns — while IT teams independently build production implementations. The result is a division of labor that aligns with the natural strengths of each group.

## 1. Introduction

The Lemina programming model [Young 2025] provides a unified approach to building business applications through leminas, accounts, and events. The companion paper on business process modeling [Young 2026a] shows how leminas map onto BPMN lanes and UML actors, and introduces the Account and Event data model that gives business and IT teams a shared vocabulary.

This paper addresses a different question: given a Lemina-based business application model, how should teams develop it? The answer is the **Lemina Development Method** — a set of practices that streamline the path from requirements through implementation and testing.

### 1.1 Three-Step Modeling Recap

The Lemina model produces a business application model in three steps, described fully in [Young 2026a]:

1. **Create Lemina accounts** for data structures of business processes and domain subjects. An account is a placeholder and container of data items related to a particular business concern, such as a checking account or an order-processing admin account. Accounts have type names; instances have IDs. Events trigger changes against account instances and carry all necessary data to complete those changes. Events are immutable historical records.

2. **Use leminas to represent entities** in different contexts — as postal recipients identified by name, as individuals in a business context with skills mapped to attention names, or as account managers equipped with the knowledge to apply events to their associated accounts.

3. **Assemble the big picture**: behavior leminas perform activities in business processes, account leminas apply events to accounts, and the two groups interact in a many-to-many relationship. All business logic is associated with events, making accounts central to the Lemina model's view.

The remainder of this paper describes three techniques that turn this model into a working development method.

## 2. The All-in-One Document

The first technique is the **all-in-one document** — a single Markdown file that encompasses requirements, data structures, business logic, and the source code that brings them to life.

### 2.1 Why Markdown

Markdown is text-based, making Pull Request diffs straightforward to review. It is simple enough for anyone familiar with office software to learn in days. And it renders well in Git hosting platforms like GitHub and GitLab, providing a readable view without specialized tools.

### 2.2 Document Structure

An all-in-one document represents and describes a Lemina account type or event type. Every document contains these core sections:

- **A visual form** representing data items — mainly for human consumption (analogous to a U.S. Tax Return Form 1040). This form also serves to display data contents on screen in the model implementation.
- **A JSON structure** representing the same data items — mainly for computer consumption (data types in code). JSON is also accessible to most business analysts.
- **Detailed explanations** for every data item (analogous to Form 1040 Instructions).

### 2.3 Account-Type Documents

If the document describes an account type, it adds:

- A **list of event types** owned by this account type.

### 2.4 Event-Type Documents

If the document describes an event type, it adds:

- The **owning account type** for this event type.
- **Detailed business logic**, including natural language descriptions and pseudocode, for how to apply changes to the specified account instance.
- A **code file name** containing the actual source code for the business logic. (Code resides in a separate file until an IDE can extract code directly from an all-in-one document.)

### 2.5 Worked Example: Bank Checking Account

To illustrate, consider an all-in-one document for a checking account's "deposit" event type:

**Visual form:**

| Field | Value |
|---|---|
| Account Type | Checking Account |
| Account Instance ID | *(instance-specific)* |
| Event Type | Deposit |
| Event Instance ID | *(auto-generated)* |
| Deposit Amount | *(decimal, > 0)* |
| Deposit Date | *(date)* |
| Deposit Channel | Branch \| ATM \| Mobile \| Wire |

**JSON structure:**

```json
{
  "accountType": "checking-account",
  "accountInstanceId": "",
  "eventType": "deposit",
  "eventInstanceId": "",
  "depositAmount": 0.00,
  "depositDate": "",
  "depositChannel": ""
}
```

**Business logic (natural language):**
When a deposit event is received, retrieve the checking account instance specified by the account instance ID. Add the deposit amount to the account's current balance. Record the deposit date and channel in the account's transaction history. The event itself is stored as an immutable record.

**Code file:** `checking-account--deposit.js`

This single document gives a business analyst the visual form and logic description they need, gives a developer the JSON structure and code reference they need, and gives a reviewer complete context in one place.

## 3. Git Repository as Requirements Management

The second technique places all-in-one documents in a **Git repository** hosted on a platform such as GitHub or GitLab.

### 3.1 Requirements as Code Changes

By storing all-in-one documents in Git, requirement changes are managed exactly like code changes — through Pull Requests (PRs). A PR that modifies a business rule will show changes to the natural language description, the pseudocode, and the source code side by side in a single diff. Reviewers see the full impact of the change without switching between tools.

### 3.2 Version History and Auditability

Git's version history provides a complete audit trail of every requirement change: who proposed it, who reviewed it, when it was merged, and what exactly changed. For regulated industries where traceability between requirements and implementation is mandatory, this is a significant advantage over traditional requirements management tools.

## 4. Build Tool and Model Implementation

The third technique is a **customized build tool** (e.g., built on Maven or Gradle) that pulls code files from all-in-one documents and assembles a model implementation.

### 4.1 Base Model Implementation

A base model implementation should be developed before the first all-in-one document exists. This base provides at least two sets of essential functions:

1. **Browsing and searching** — displaying and examining Lemina account and event contents by browsing account types, account instances of a selected type, and events of a selected account instance.
2. **Event application** — accepting one or more consecutive events and applying them to the specified account instance by executing their business logic.

### 4.2 Verification and Testing

Since business logic is invisible in execution, examining its correctness involves comparing the before-and-after contents of the account instances it impacted. The model implementation supports both:

- **Manual verification** — a business analyst submits an event and inspects the resulting account state.
- **Automated testing** — test cases specify an initial account state, a sequence of events, and the expected final state.

### 4.3 Continuous Integration

Once a PR has been reviewed, approved, and merged, the build tool pulls updated code from the all-in-one documents and deploys it into the running model implementation. Every merged PR results in a verifiable, testable increment.

## 5. Benefits

### 5.1 Situational Awareness

Since all information is stored in one Git repository, all participants remain aware of the full context of the business application. For applications developed simultaneously by dozens or hundreds of people, participants must understand what they are doing, what others are doing, and why. This situational awareness improves overall efficiency, increases the odds of project success, and reduces the risks of project failures and delays.

### 5.2 PR Conflict Prevention

The Git Pull Request mechanism prevents conflicts from being committed when PRs contain all related data items, business logic, and source code changes. The first defense against conflicts is designating well-arranged features or areas for each team. However, teams inevitably converge as development progresses:

- The application's features may not have precise edges.
- Deadlines approach, concentrating effort in overlapping areas.
- Idle teams join the project in areas already occupied.
- Teams step on each other's toes accidentally.

The PR mechanism does not prevent conflicts from arising, but it prevents them from being committed. Detecting and resolving such conflicts earlier saves money and mitigates the risk of downstream liabilities.

### 5.3 Feedback Loops

A unit of work — a PR by a team in a sprint — contains requirement elicitation or adjustment, design, coding, and testing. This covers the unit of work's entire lifecycle, making it more independent and forming a **feedback loop** that aligns with agile principles.

### 5.4 CVA — Continuously Variable Agility

Drawing from CVT (Continuously Variable Transmission), this fine-grained agility is termed **CVA** (Continuously Variable Agility). Each PR is a self-contained increment that can be as small or as large as the situation demands, providing continuously variable granularity in the development process.

## 6. Functional Reference Implementation

The Lemina Development Method aims to deliver a strategic benefit: enabling business people to complete the full development of their applications up to **functional reference implementations** without needing IT people, or keeping their involvement to a minimum.

### 6.1 What Is a Functional Reference Implementation?

A functional reference implementation is the model implementation equipped with features for all functional requirements but no features for nonfunctional requirements (performance, security, scalability, reliability, etc.). It demonstrates what the system does without addressing how it does it at production scale.

### 6.2 Forms Bridge Business and IT Mindsets

The use of forms bridges the gap between business and IT perspectives. Before computers existed, people performed business activities with universally understood forms. It is natural for business people to analyze business processes and activities and use forms to represent the data needed. On the other hand, forms and JSON have the same expressiveness regarding data and data structure, so they convert easily between the two representations.

### 6.3 Small, Well-Defined Contexts

Business logic is associated with activities in business processes, activities are associated with events, and events are associated with attention names in leminas. Therefore, **lemina attention is the context and unit of code** that handles an event and implements the event's business logic.

This is a well-defined context that includes at least the event instance, the specified account instance, and other account instances that may be involved according to business logic. Programming business logic in such a clearly defined context is straightforward — even for people whose primary expertise is business rather than software engineering.

### 6.4 Two Parallel Implementations

While IT teams will not modify the functional reference implementation, they will assemble data structures and code from the Git repository to create a **production implementation** with nonfunctional features. The Lemina method expects these two implementations to run in parallel throughout their lifespans:

- **Business teams** maintain the functional reference implementation for verification and continuous development.
- **IT teams** maintain the production implementation with performance, security, scalability, and other nonfunctional capabilities.

### 6.5 Division of Labor

Adam Smith opens *The Wealth of Nations* with these words: "The greatest improvement in the productive powers of labour … seem to have been the effects of the division of labour." In the programming world, IT teams take the work of business people and build it into production applications. The Lemina method formalizes this division: business people develop the functional reference, IT people build the production system, and the Git repository serves as the shared foundation for both.

## 7. Limitations and Practical Challenges

### 7.1 Tooling Maturity

The Lemina Development Method depends on tooling that does not yet exist as off-the-shelf products: a customized build tool that extracts code from Markdown documents, a base model implementation, and IDE support for editing code within all-in-one documents. Until these tools mature, adopting teams must invest in building and maintaining them.

### 7.2 Adoption Barriers

The method requires business analysts to work with Git, write in Markdown, and understand JSON — skills that are increasingly common but not yet universal. Organizations must be willing to invest in training and cultural change.

### 7.3 When This Method Is Appropriate

The Lemina Development Method is best suited for business applications with complex, evolving requirements where the gap between business and IT understanding is a primary source of project risk. For applications with stable, well-understood requirements or those dominated by nonfunctional concerns (e.g., high-frequency trading systems), the overhead of all-in-one documents may not be justified.

### 7.4 Scaling Considerations

As the number of all-in-one documents grows into the hundreds or thousands, repository organization, navigation, and build performance become concerns that require deliberate architectural decisions.

## 8. Related Work

**Literate programming** [Knuth 1984] pioneered the idea of interleaving prose and code in a single document. The all-in-one document shares this philosophy but differs in purpose: literate programming targets code comprehension, while the all-in-one document targets requirements-implementation traceability across business and technical audiences.

**Requirements-as-code** approaches, such as Behavior-Driven Development (BDD) [North 2006] and executable specifications, bring requirements closer to code. BDD's Given-When-Then scenarios resemble the event-driven structure of Lemina's Account/Event model. However, BDD scenarios typically live alongside code rather than embedding it, and they do not encompass data structure definitions.

**Model-Driven Engineering (MDE)** [Schmidt 2006] generates code from models, similar to how the Lemina build tool assembles implementations from all-in-one documents. MDE typically relies on graphical models and specialized tooling, whereas the Lemina method uses plain text files in a standard Git repository, lowering the barrier to adoption and enabling standard code review workflows.

**Low-code/no-code platforms** aim to enable business users to build applications without traditional programming. The Lemina method shares this goal but takes a different approach: rather than abstracting away code behind a visual interface, it creates small, well-defined coding contexts where business logic is straightforward enough for non-specialists to implement.

**Event sourcing** [Young 2010] stores application state as a sequence of immutable events, closely paralleling Lemina's event-driven account model. The Lemina method extends this pattern into a full development methodology encompassing requirements, documentation, and team workflow.

## 9. Conclusion

The Lemina Development Method introduces three techniques — all-in-one documents, Git-based requirements management, and a build tool producing model implementations — that together create a development environment covering the full lifecycle from requirements through verification. By embedding requirements, data structures, business logic, and source code in a single Markdown document managed through pull requests, the method provides situational awareness, conflict prevention, and continuous feedback loops.

The strategic contribution is the functional reference implementation: a complete, business-maintained implementation of all functional requirements that runs alongside the IT team's production implementation. This division of labor allows each group to work within its strengths — business people defining what the system does, IT people ensuring it does so at scale — with the Git repository as their shared foundation.

## References

- [Knuth 1984] Knuth, D. E. "Literate Programming." *The Computer Journal*, 27(2), 1984.
- [North 2006] North, D. "Introducing BDD." *Better Software*, 2006.
- [Schmidt 2006] Schmidt, D. C. "Model-Driven Engineering." *IEEE Computer*, 39(2), 2006.
- [Young 2010] Young, G. "CQRS Documents." 2010.
- [Young 2025] Young, R. "Lemina: A Unified Object-Oriented Programming Model for Single-Process and Distributed Systems." TechRxiv preprint, 2025. https://doi.org/10.36227/techrxiv.175339121.11973602/v1
- [Young 2026a] Young, R. "Lemina for Business Process Modeling." Working draft, 2026.
