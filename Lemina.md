# Lemina: A Unified Object-Oriented Programming Model for Single-Process and Distributed Systems

<small>Copyright © 2025-2026 Rex Young. All Rights Reserved.<br>
This paper is part of a repository governed by a [LICENSE](../LICENSE.md).<br>
Readers who obtain this file individually are bound by the same terms.<br>
Status: Working draft (revised from preprint at https://doi.org/10.36227/techrxiv.175339121.11973602/v1)<br>
Contact: rex@fastmessenger.com</small>

# ABSTRACT

Modern software relies on objects, actors, and services, yet these paradigms fracture across process boundaries, leaving concurrency and distribution disjointed. Enter Lemina: a pioneering text-based interface that fuses their strengths into one seamless framework. Drawing from postal systems, Lemina names like "Admin\#Enroll" unify methods, mailboxes, and endpoints, backed by a frontend for synchronous/asynchronous calls and a backend executing across styles—native types within processes, JSON between them. Its inter-process edge excels in providing elegant, one-way async messaging, free of complex structures or protocols. Proof-of-concept implementations in JavaScript, Java, and C\# showcase its power: managing intra-process concurrency and scaling inter-process communication across the Internet. Beyond code, Lemina enables self-owned social media systems to run on today's Internet with user freedom at its core. For academics and engineers, this human-centered rethink demonstrates a viable path forward, offering potential from core programming to societal impact.

# 1\. INTRODUCTION

## 1.1 The Problem

### 1.1.1 The Question

Object-oriented programming (OOP) languages such as Python, Java, and JavaScript dominate modern software development \[Cass 2024\]. Objects emerged in the 1960s, with milestones like Simula 67 (1967) and Smalltalk-72 (1972) shaping their evolution \[Kay 1996\]. Yet, OOP’s enduring dominance prompts a critical question: Does it adapt to modern challenges like network distribution and multicore concurrency, or does it persist due to historical inertia? This section assesses OOP's adaptability to these challenges.

### 1.1.2 Networking

Networking, ignited by packet switching in 1965 and propelled by the Internet in the 1990s, transformed applications from intra-process programs into distributed systems requiring inter-process coordination. OOP excels within a single process, leveraging tightly coupled objects, but struggles across processes where this tight coupling becomes a liability (e.g., object references cannot span process boundaries). Distributed object systems like CORBA, RMI, and DCOM \[Plášil et al. 1998\] sought to extend OOP across processes but stumbled due to complexity and rigid coupling. In contrast, services—first Web services, then RESTful APIs—thrived with stateless designs and HTTP simplicity, now leading distributed programming \[Erl 2016\].

### 1.1.3 Multicore Processors

Multicore processors, introduced with IBM's POWER4 in 2001 and became widespread by the late 2000s \[Blake et al. 2009\], demand intra-process concurrency. Early attempts like concurrent objects \[Yonezawa et al. 1986\] and active objects \[Lavender et al. 1996\] faced complexity and inadequate tooling, failing to integrate smoothly into OOP. Multithreading, such as Java's threading constructs, serves as an add-on feature that is not core to the object model, leaving concurrency as an external tool rather than a native paradigm.

### 1.1.4 The Problem

OOP excels at intra-process logic, where encapsulation aids modular design, but fails to evolve into inter-process distribution (e.g., via distributed objects) or intra-process concurrency (multicore). The actor model, introduced in 1973 \[Hewitt et al. 1973\] and realized in Erlang by 1986 \[Armstrong 2007\], excels at both distribution and concurrency via message-passing and independence, yet its steep learning curve limits adoption. Modern services like RESTful APIs dominate inter-process communication but are inapplicable to intra-process programming, relying instead on OOP to construct their internal operations. This gap—where objects falter beyond single processes, actors intimidate with complexity, and services lack intra-process relevance—inspires the Lemina Model, which unifies intra- and inter-process programming seamlessly.

## 1.2 The Solution

This paper proposes the Lemina Programming Model to unify intra- and inter-process programming, addressing the gap left by objects, actors, and services.

Lemina—named to evoke human-centered design—is a text-based interface with a consistent structure: Lemina names (e.g., "*Admin*") map to objects, actors, or services, and attention names (e.g., "*Enroll*") specify methods, mailboxes, or operations. For example, "*Admin\#Enroll*" maps to admin.enroll() for objects, a mailbox for actors, or an endpoint for services.

The Lemina Service, inspired by real-world mail systems, realizes Leminas through a frontend and backend. The frontend exposes Leminas to callers via synchronous and asynchronous interactions:

* Result \= LeminaService.call ("Admin\#Enroll", args) // Synchronous.  
* LeminaService.send ("Admin\#Enroll", args) // Asynchronous.  
* LeminaService.send ("Admin\#Enroll", reply-to: "Admin\#PostEnroll", args) // Asynchronous with reply-to.

The backend implements Leminas using objects, actors, or services. This paper emphasizes objects—passive entities needing execution contexts (e.g., threads) to handle requests—while noting active entities like actors and services adapt with minimal changes.

For objects, the backend provides varied contexts to activate them, ensuring a seamless transition from traditional OOP to Lemina, alongside richer capabilities, such as the actor model's safe concurrency. Extending this, a network of Lemina Services supports inter-process calls by routing requests to remote backends using native types intra-process and JSON inter-process. Callers experience unified programming across boundaries, whether local (e.g., "*Admin\#Enroll*") or remote (e.g., a Java caller could invoke a C\# service’s Lemina with JSON arguments):

* JavaService.call ("Admin.CsharpService\#Enroll", jsonArgs)

## 1.3 Results

This section presents proofs of concept (POCs) in JavaScript, Java, and C\# that validate Lemina's unification of intra- and inter-process programming. It details backend implementations and highlights diverse execution styles, providing sufficient technical specifics for readers with standard skills to reproduce and verify the approach.

### 1.3.1 Single Lemina Service for Intra-Process

To process a request, the backend typically (1) locates the object and its configuration using a Map, (2) identifies the method via Reflection (in Java) or property key (in JavaScript), (3) selects an execution style, (4) executes the code, and (5) handles an optional reply-to by wrapping results into a new request with the reply-to address. Each object's configuration, stored alongside it in the Map, provides details like resolving ambiguous method signatures. While JavaScript's single-threaded nature limits its concurrency options, Java and C\# harness multithreading for flexible and creative execution styles, such as:

* Caller thread (object-style, synchronous).  
* Single-threaded per Lemina (actor-style, safe concurrency-focused).  
* Thread pool for multiple objects per Lemina (load balancer-style, capacity-focused).  
* GUI thread for GUI Leminas (specialized).

These styles highlight the Lemina Model's flexibility in managing passive objects behaviorally intra-process. The Java and C\# POCs demonstrate Lemina's ability to exploit multicore concurrency through varied threading strategies, while the JavaScript POC proves its adaptability to single-threaded environments.

### 1.3.2 Multiple Lemina Services for Intra-Process

Beyond execution styles, Lemina organizes objects structurally to mitigate tight coupling risks in large programs and prevent reference-based spaghetti code. Objects are grouped into Leminas (est. in the tens of objects), managed by individual Lemina Services (est. in the hundreds and thousands), and unified into an intra-process system (est. in the millions).

In Java and C\# POCs, Lemina Services register their names (e.g., "Alice") and objects into a ServicesMap. Lemina names distinguish local entities (e.g., "Admin") from non-local ones (e.g., "Admin.Bob"). A request like AliceService.call ("Admin.Bob\#Enroll", args) retrieves the BobService object via the ServicesMap for execution. This extensible naming and registration system supports hierarchical scaling for complex programs.

These POCs validate Lemina's scalability by efficiently managing thousands of Lemina Services within a single process on multicore architectures.

### 1.3.3 Multiple Lemina Services for Inter-Process

LAN-connected POCs (e.g., Bob at 192.168.0.15:9090) maintain a service name-to-IP mapping table for customized routing. A call like AliceService.call ("Admin.Bob\#Enroll", jsonArgs) routes the JSON request to 192.168.0.15:9090, where BobService listens and processes it locally as "Admin.Bob."

Lemina Services can leverage Internet infrastructure (e.g., DNS, routing) to eliminate customized routing by adopting a naming convention that embeds IP or domain into Lemina names (e.g., "Admin.192.168.0.15\#Enroll" or "Admin.Lemina.Edu\#Enroll"). A sending Lemina Service extracts the IP or domain, connects, and transmits the JSON request—enabling the Internet of Leminas, which is open to all participants, as the POCs demonstrate. Similar to websites, security can be implemented using SSL connections \[Thomas 2000\] between Lemina Services or between Leminas.

These inter-process POCs confirm Lemina's extensibility across distributed systems. Java and C\# leverage multicore concurrency for efficient local execution while all confirm adaptability to routed JSON-based requests.

### 1.3.4 Beyond—Reinventing Social Computing

Lemina, a text-based interface defined by a name and a set of attentions representing capabilities—actions it can perform—offers a foundation for directly representing real-world entities, such as business processes with their activities in BPMN \[von Rosing 2014\] or individuals with their capabilities in social computing.

In today's social computing landscape, individuals lack autonomy and independence. They depend on vendor-provided accounts from social media companies to establish their social identities and lack personal social "*bodies*" to embody their capabilities, relying instead on company-supplied applications to maintain an online presence.

Building on the Internet of Leminas, this design empowers individuals by casting them as Leminas with self-hosted identities and bodies (e.g., capabilities). Consider Joe, who secures the domain "The-Joe-Family.US" and claims “Joe.The-Joe-Family.US” as his social identity. By maintaining domain fees, he retains ownership, free from external control. Joe procures social media software from free markets or open-source communities and deploys it to his domain via a paid hosting service. Others can interact with Joe through Lemina calls like "Joe.The-Joe-Family.US\#ReadTimeline" to access his timeline, "Joe.The-Joe-Family.US\#CommentPost" to comment on a post, or message him via either "Joe.The-Joe-Family.US\#IM" or "Joe.The-Joe-Family.US\#Email". It shifts social computing from vendor-controlled silos to an ecosystem of self-owned, end-user-programmable personal platforms \[Blackwell 2002\]. Through this, Joe establishes a self-controlled social identity and digital body, extending Lemina into the social realm.

# 2\. LEMINA PROGRAMMING MODEL

## 2.1 Background

This section examines the influences, motivations, and design decisions shaping the Lemina Programming Model, offering insight into its foundational principles through a systemic worldview framed by Laszlo \[1996\]: *"Whereas traditional reductionism sought to find the commonality underlying diversity in reference to a shared substance, such as material atoms, contemporary systems theory seeks to find common features in terms of shared aspects of organization." (p. 17\)*

### 2.1.1 Lemina as a Text-Based Interface

This perspective reveals shared structural and behavioral patterns across programming abstractions—procedures, objects, actors, and services—and their real-world analogs. Structurally, these entities share a parent-child hierarchy: procedures encapsulate a single function, objects group multiple methods, actors manage a mailbox, and services provide operations. Beyond computation, this pattern reflects roles with responsibilities, businesses with operations, and individuals with capabilities, all similarly organized. Behaviorally, they share a common mechanism: invocation, where a caller triggers a callee, shifting to message delivery for active entities (actors, services, and autonomous agents like people), with a sender dispatching to a recipient. Lemina's text-based interface, supporting both synchronous and asynchronous operations, arises from these "common features" and builds on Liskov et al.'s \[1974\] principle that "a data type is defined by its operations." This approach abstracts operations (e.g., method calls, messages, endpoints) into a text-based form—such as "Admin\#Enroll"—unifying computational abstractions—such as objects, actors, and services—and spanning multiple languages, while also accommodating real-world entities like business processes or social activities, thus broadening its scope beyond traditional programming.

### 2.1.2 Native Requests for Intra-Process; Text-Based Requests for Inter-Process

This systemic inspiration shapes Lemina's approach to requests. Compared to natural systems described by Laszlo \[1996\], such as biological organization across cells, organisms, and societies, programming abstractions remain nascent. In biological organization, interaction types have evolved: subcellular materials forming cells and cells forming organs rely on proximity and biochemical reactions; physically separated organ systems employ hormones carried by the bloodstream for remote coordination; and human communication progresses from intra-body chemical signals to inter-body vocal or visual methods. This progression—from direct interaction to transport-mediated remote interaction to distinct external communication—inspires Lemina's dual strategy: native types for intra-process efficiency and text-based forms (e.g., JSON) for inter-process universality. Rejecting conventional serialization of objects across processes, Lemina confines objects to their native process, using native types internally and text-based, agnostic forms externally.

### 2.1.3 Turn Invocation from a Caller's Matter into a Public Service

Invocation varies across abstractions: objects require the caller to hold a direct reference and initiate execution; actors use logical identifiers (e.g., process IDs) resolved by systems like Erlang; REST services depend on flexible HTTP URLs, with callers managing connections. In traditional approaches, such as manually triggering a target's "START" button, the responsibility falls entirely on the caller—termed a "caller's matter"—except in actors, where the system delegates execution. It contrasts with postal services, as explored in The Postal Age \[Henkin 2019\] and The Division of Labor in Society \[Durkheim 2023\]: a sender names an address, and the system delivers, inspiring Lemina's scalable request-handling model. Lemina's Service provides a frontend for request collection and a backend for message delivery or invocation execution. Transportation is user-defined, utilizing existing methods like Internet connections (e.g., Section 1.3.3's POCs) and design patterns or architectures (see Sections 1.3.2 and 1.3.3).

Lemina's design mirrors the Industrial Revolution's transformative arc, as traced by Landes \[2003\]: it standardizes both its text-based interface and requests to unify callers and callees, unleashes their potential across intra- and inter-process boundaries, and scales this explosion of interactions through a public postal-like service. By synthesizing systemic patterns, Liskov's abstraction, and postal efficiency, Lemina mirrors the industrial shift from isolated production to interconnected systems, bridging computational and real-world domains.

## 2.2 Elements and Concepts

This section introduces the core elements and concepts—interface, request, service, namespace, and compliance—that define the Lemina Model’s operational framework.

Since the model applies a text-based interface across multiple contexts—including method invocation for intra-process, message passing for inter-process, and instant messaging for inter-person—terminologies from these contexts are interchangeable. For example, caller and sender are equivalent terms for the initiating source; invocation request and message represent the medium; and callee, receiver, and recipient interchangeably denote the target. This alignment extends to actions, such as a caller submitting requests equating to the Lemina frontend collecting them, unifying the model’s operational framework.

### 2.2.1 Text-Based Interface

Lemina is a text-based interface structured with a one-level hierarchy. The parent is Lemina itself, and its children, termed attentions, draw inspiration from envelope attention lines.

Lemina's name—aka address or identifier—is a textual value such as "Admin," while attention names are textual values like "Enroll" or "PostEnroll." Names consist of letters (case-insensitive), digits, dashes, and underscores. A qualified Lemina attention name combines Lemina's name and an attention name, separated by a pound sign (\#), as in "Admin\#Enroll." Lemina names can be multi-parts separated by dots (.) such as "Admin.Lemina.Edu"; however, the single-part names are preserved for local Leminas.

The model's one-level hierarchy can be extended to multiple levels (e.g., "Admin\#Enroll\#Json") as needs emerge.

### 2.2.2 Standardized Request

The model employs an interface to decouple a caller and a callee, connecting them via standardized requests defined as named tuples with three fields: *to*, *reply-to*, and *data*. The to field designates the recipient Lemina’s name. The optional reply-to field, also a Lemina’s name, identifies the recipient of asynchronous results post-processing, facilitating decoupled responses. The data stays private between source and target, supporting any form or format—plain or encrypted—as long as both parties understand it and it can be transported. Unknown fields might be specific to some Lemina Services and can be ignored by others.

The request excludes an invocation-type field (e.g., synchronous/asynchronous), treating this as a caller-side choice managed by the frontend. The frontend of the Lemina Service manages such features, sparing the backend involvement; using a calling thread to execute a callee, resembling classical OOP method invocation is treated as an implementation detail.

### 2.2.3 Lemina Service

The Lemina Service adapts real-world postal systems, which integrate mail collection and delivery for in-town service. It extends to inter-town transportation with target towns embedded in street addresses for a unified, multi-town system. Accordingly, a Lemina Service comprises a frontend collecting requests, a backend delivering requests, and a middle tier handling request transportation.

For intra-process scenarios, all three components—frontend, backend, and middle tier—reside within a single process. In inter-process scenarios, an inter-process transportation system allows the frontend to send requests to, and the backend to receive requests from, Lemina Services in other processes.

The model restricts inter-process Lemina Services to one-way asynchronous messages (i.e., requests). This limitation requires frontends to use two one-way asynchronous requests—leveraging the reply-to mechanism—to emulate a synchronous call for their callers.

### 2.2.4 Lemina Namespace

A Lemina Namespace (or address space) refers to a Lemina network (a collection of networked Lemina Services) and all of their Leminas, each of which can be invoked by a caller through any Lemina frontend. A standalone Lemina Service always has a local namespace, managing its local Leminas—those identified by single-part names (e.g., "Admin") within its direct control. Besides the local one, a Lemina Service may join multiple namespaces, such as an enterprise Lemina network or a public Internet Lemina network, allowing its Leminas to be invoked by callers from those networks.

Drawing from real-world postal systems, which use envelope addresses to route mail locally, to another town, or internationally, Lemina adopts a naming convention ensuring each name in a namespace is unique and includes location hints. Thus, a Lemina Service can join many Lemina networks, each with a different naming convention or vice versa. As for transportation, one transportation system may be shared by multiple namespaces.

Each frontend must recognize the naming conventions of its Lemina networks, resolving a recipient's name to either a local Lemina for backend delivery or a network-specific name for transportation elsewhere. For instance, a GatewayService bridges the Internet and an internal college network, listening at "Lemina.Edu" externally while connecting to the college's namespace internally. On the Internet, names follow the pattern "XY-L.\<domain-name\>" (e.g., "EA-Admin.Lemina.Edu\#Enroll"), where "E" is a team code (Enrollment), "A" is a department code (Admission), and "Admin" is the local Lemina name. The GatewayService resolves this to "Admin.Enrollment.Admission\#Enroll" per the college network's "L.\<team\>.\<dept\>" convention and forwards it via the college's transportation system. Conversely, a college service receiving "Joe.The-Joe-Family.US\#IM"—unrecognized locally—routes it to the GatewayService, which connects to "The-Joe-Family.US:9090" and transmits the request over the Internet.

### 2.2.5 Lemina Compliance

The sole compliance requirement is the use of the Lemina interface.

All other aspects—implementation, extensions, or mechanisms—can be customized to suit specific contexts. For example, a Java-based Lemina Service could provide callers with Future \[Welc 2005\] for asynchronous result retrieval:

* Future result \= LeminaService.send ("Admin\#Enroll", args) // Asynchronous.

Future can leverage standard Java thread-to-thread communication for intra-process calls. For inter-process calls, the service can implement a custom Future class that acts as a Lemina by registering with the Lemina Service using a unique name (e.g., a UUID), allowing it to receive results via the Model's reply-to mechanism. Similarly, exceptions can adopt this dual approach; however, since the standard request's data field is single-purpose, implementations may add a separate error field for inter-process error handling tailored to their needs.

The Lemina Model does not define any error-handling mechanism, which the paper will explain in the next chapter.

# 3\. DISCUSSIONS AND FUTURE WORK

## 3.1 Standalone Programs

This paper defines a *program* as code running in one process and an *application* as multiple programs. The object model and object-based languages, such as JavaScript and Java, remain the gold standard for program development. The Lemina Model enhances this paradigm as a library, not a language, sidestepping the complexity of new language design. It enables experienced developers to create implementations for their teams and businesses at low cost using standard skills, fostering diverse solutions that adapt to their needs, not vice versa. Developers are encouraged to customize Lemina to their language's native coding styles and features, such as Future or Exception (Section 2.2.5), making it a practical, flexible extension of OOP for standalone programs. POCs in JavaScript and Java (Section 1.3.1) illustrate this adaptability.

## 3.2 Inter-Process Applications

Inter-process applications face networking and coordination challenges (Section 1.1.2), spanning diverse architectures and DevOps ecosystems. Changing one program's behavior risks disrupting other components in these complex systems, such as enterprise setups with clustered servers and load balancers. The Lemina Model applies internally to programs within these applications, as in Section 3.1, enhancing them without forcing external adaptation.  
Unified namespaces, demonstrated in Section 1.3.3 with network transportation, extend this approach across processes. In enterprise environments, common data-transporting mechanisms like message brokers Kafka and AMQP \[John et al. 2017\] can serve as Lemina's transportation system, carrying its pure JSON requests.  
The Lemina Model encourages implementing local Lemina Services with native features, such as Exception for error handling and recommends adding an *error* field in requests for inter-process implementations (Section 2.2.5). *Fault tolerance*, however, requires further study, as enterprise servers under load balancing fail and reload frequently, necessitating this feature.

## 3.3 Social Computing

Unlike enterprise applications and general inter-process programming, Lemina-style social computing \[Section 1.3.4\] does not have any legacy constraints. Engineering work in this field can start immediately.

# 4\. RELATED WORK

No direct parallels to the Lemina Programming Model are known in programming abstraction literature. Early efforts extended objects to distributed objects \[Plášil et al. 1998\], e.g., CORBA and Java RMI, concurrent objects \[Yonezawa et al. 1986\] via ABCL/1, and active objects \[Lavender et al. 1996\], but these pre-2000s works waned. Recently, Akka/Java \[Roestenburg et al. 2016\] merges actors with object method calls, contrasting Lemina's name-based decoupling. Most recently, choreographies—a service-like abstraction—have been implemented by objects \[Giallorenzo et al. 2024\], unlike Lemina's postal service approach.

# 5\. CONCLUSIONS

Lemina emerges as a bold text-based interface, uniting objects, actors, and services to mend the fracture between intra- and inter-process programming—a gap unfilled by prior abstractions. Its postal-inspired design delivers seamless execution, validated by JavaScript, Java, and C\# proofs of concept that manage concurrency within processes and scale communication across the Internet with elegant simplicity. For academics, Lemina reimagines computational design; for engineers, it bridges process divides with a ready-to-run framework. Its inter-process finesse—one-way async messaging sans complexity—stands out, as does its leap beyond code to self-owned social media systems. Simplicity, extensibility, and unity are evident, with security and error handling poised as future strengths. This work cements Lemina’s viability, sparking a path for technical innovation and societal shifts alike.

# REFERENCES

Stephen Cass. (2024). *The Top Programming Languages 2024*. IEEE Spectrum. https://spectrum.ieee.org/top-programming-languages-2024  
‌  
Alan C. Kay. (1996). The early history of Smalltalk. In *History of programming languages---II* (pp. 511–598).

František Plášil, & Michael Stal. (1998). An architectural view of distributed objects and components in CORBA, Java RMI, and COM/DCOM. *Software-Concepts & Tools*, *19*, 14–28.

Thomas Erl. (2016). *Service-Oriented Architecture: Analysis and Design for Services and Microservices* (2nd ed.). Prentice Hall.

Geoffrey Blake, Ronald G. Dreslinski, & Trevor Mudge. (2009). A survey of multicore processors. *IEEE Signal Processing Magazine*, *26*(6), 26–37.

Akinori Yonezawa, Jean-Pierre Briot, & Etsuya Shibayama. (1986). Object-oriented concurrent programming in ABCL/1. *ACM SIGPLAN Notices*, *21*(11), 258–268.

R. Greg Lavender & Douglas C. Schmidt. (1996). Active object: an object behavioral pattern for concurrent programming. In *Pattern languages of program design 2* (pp. 483–499).

Carl Hewitt, Peter Bishop, & Richard Steiger. (1973). A Universal Modular ACTOR Formalism for Artificial Intelligence. Proceedings of the 3rd International Joint Conference on Artificial Intelligence. IJCAI 73\.

Joe Armstrong. (2007). A history of Erlang. In *Proceedings of the third ACM SIGPLAN conference on History of programming languages* (pp. 6–1).

Adam Welc, Suresh Jagannathan, & Antony Hosking. (2005). Safe futures for Java. In *Proceedings of the 20th annual ACM SIGPLAN conference on Object-oriented programming, systems, languages, and applications* (pp. 439–453).

Ervin Laszlo. (1996). *The Systems View of the World: A Holistic Vision for Our Time*. Hampton Press.

Emile Durkheim. (2023). The division of labor in society. In *Social Theory Re-wired* (pp. 15–34). Routledge.

David M. Henkin. (2019). *The Postal Age: The emergence of modern communications in nineteenth-century America*. University of Chicago Press.

Barbara Liskov, & Stephen Zilles. (1974). Programming with abstract data types. *ACM Sigplan Notices*, *9*(4), 50-59.

David S. Landes. (2003). *The unbound Prometheus: technological change and industrial development in Western Europe from 1750 to the present*. Cambridge University Press.

Raymond Roestenburg, Rob Williams, & Rob Bakker. (2016). *Akka in action*. Simon and Schuster.

Saverio Giallorenzo, Fabrizio Montesi, & Marco Peressotti. (2024). Choral: Object-oriented choreographic programming. *ACM Transactions on Programming Languages and Systems*, *46*(1), 1–59.

Stephen Thomas. (2000). *SSL and TLS essentials*. New York, Wiley.

Mark von Rosing, Henrik von Scheel, & August-Wilhelm Scheer. (2014). *The complete business process handbook: Body of knowledge from process modeling to BPM, Volume 1* (Vol. 1). Morgan Kaufmann.

Vineet John, & Xia Liu. (2017). A survey of distributed message broker queues. *arXiv preprint arXiv:1704.00411*.

Alan F. Blackwell. (2002). What is programming?. In *PPIG* (Vol. 14, pp. 204–218).

© Copyright 2025 Rex Young. All Rights Reserved.
