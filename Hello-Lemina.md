# Hello, Lemina\!

<small>Copyright © 2024-2026 Rex Young. All Rights Reserved.<br>
This paper is part of a repository governed by a [LICENSE](../LICENSE.md).<br>
Readers who obtain this file individually are bound by the same terms.<br>
Status: Working draft<br>
Contact: rex@fastmessenger.com</small>

**Part 1 — Programming's Evolving Path**  
**Part 2 — Lemina Programming Model**  
**Part 3 — Lemina Programming Model for Business Applications**  
**Part 4 — Lemina Business Application Development** 

# Part 1 — Programming's Evolving Path

Computer programming, a **remarkable craft**, is woven into the CPU's very operation. It shares developmental threads with machine-operating techniques like car driving. Both have evolved along parallel paths to achieve **operational efficiency**. This *human-centered evolution* of programming, a journey we all recognize—drives our discussion.

At the dawn of every newly invented machine, users had to adapt to its limitations. The first modern car, the *Benz Patent-Motorwagen No. 1*, built in 1885 by Karl Benz, forced people to use a centered steering crank instead of a steering wheel and a left-handed gas-and-brake handle instead of pedals to drive.

Over time, a wave of **human-centered features** emerged in car driving to align the car's operations with our natural reactions. For instance, General Motors introduced an automatic transmission in its Oldsmobiles in 1924, and Chrysler pioneered power steering in 1951\.

These features changed how cars operate, catering to drivers' desires for more intuitive and relatable driving machines. Other human-centered additions included **cruise control**, which allows the driver to set a constant speed without keeping their foot on the gas pedal, and **anti-lock braking systems**, which prevent the wheels from locking up during braking, improving the driver's control over the car during critical moments.

Today, car driving is approaching the end of its evolution. With merely an address, **self-driving cars** can take their passengers to their destinations without further human input.

As early automobiles began with simple mechanics, early programming began with **machine code**. Each machine code represents a CPU operation, which could be one of the following:

* Arithmetic operations (such as addition, subtraction, multiplication, and division) on two words (such as numbers within limited ranges)    
* Bitwise operations on one or two words    
* Jumping to another address in memory and executing stored machine code from there    
* Comparing two words and conditionally jumping based on the comparison result

A word is the size of CPU registers and memory units. The Intel CPU 8088, used by the first IBM personal computer released in 1981, was 8 bits, which could hold a number ranging from 0 to 255 (or from \-128 to 127 with a sign). If a number larger than 255 was needed in a program, the programmer had to write more machine code to use multiple words to achieve it. Unfortunately, programmers could not easily enlarge the word size for the CPUs of the time because physical circuits had to be laid on the chip to support every bit of the CPU's combined internal registers and memory units. Longer words required more circuits on the chip. As a result, personal computers have been equipped with 64-bit CPUs since 2000, such as the Intel Pentium 4 processor and the present-day Intel i9.

Most non-IT people observing modern devices—smartphones, gaming systems, Internet applications, cloud infrastructures, and now AI-enabled programs—can't believe CPUs remain so raw at a fundamental level. The **tedium** of working with dumb **machine code** drove programmers to pioneer a series of **human-centered features** in modern programming.

The first wave introduced **high-level programming languages**, such as FORTRAN (invented by IBM in 1957 as the first high-level language), COBOL, and BASIC. These languages allowed programmers to use user-friendly elements like English keywords, data types, variables, arithmetic expressions, and procedures (or functions).

A program written in a high-level programming language cannot be understood or executed directly by the CPU, so it must be translated into machine code. Thus, a high-level programming language is always equipped with a pre-execution compiler (which translates the entire program into machine code before execution) or a real-time interpreter (which translates the program line-by-line during execution) for the machine code translation.

This innovation led to two key benefits that would shape the future of programming. First, the compiler automated repetitive work for programmers, leading to a significant leap in efficiency. Before this innovation, programmers had to write extra machine code to utilize a number exceeding the size the CPU could handle. With the new high-level languages, the compiler's job was to support new data types and variables, leaving human coders with extra time for more demanding tasks. The second key benefit was that these procedures allowed programmers to group repeated and relevant parts of code for reuse, removing redundant coding labor from the process and further enhancing the workflows of human programmers.

The second wave introduced **object-oriented programming (OOP)**, backed by the object model, a term coined by Alan Kay in 1967\. An object is a programming element that encapsulates relevant and private state (data) and behavior (code) to which no outside access is allowed. Other objects or non-object codes can only operate the object through its predefined interfaces or "methods," which are procedures or functions owned and encapsulated by objects. OOP programming languages are also considered high-level and equipped with compilers or interpreters. Eventually, OOP programs were translated into machine code, allowing a range of users that was impossible before this innovative new process.

The innovations brought by the first two waves have fundamentally improved programming. Most of today's programming languages are high-level and object-based (object-based is broader than object-oriented). Unlike high-level languages, which automate repetitive work for programmers, objects address increasing code complexity by introducing a new building block for constructing programs. Objects profoundly impact programming because this building block is like a new "life element" in programs. It's as functionally significant to programmers as the first appearance of the division or specialization of labor in Adam Smith's *The Wealth of Nations* was for economists and business managers.

The emergence of the object concept and model has allowed programmers to evolve from designing each step of a computational task (e.g., high-level code or low-level CPU operations) to organizing a group of specialized objects that contain relevant data and behaviors. Thus, programming itself has evolved into a new twofold technique: programmers design detailed steps to form specialized objects and then organize them to create programs.

People who pay attention to lists of the most popular programming languages every year know that OOP will still be mainstream in 2024\. Does this mean programming has stopped evolving for the last 60 years since the late 1960s? Surprisingly, we have not made any meaningful breakthroughs in **general-purpose programming** since the OO revolution.

Despite this, the IT industry has not been dormant for 60 years. Instead, it has expanded its territory into every corner of people's lives, shaping our daily experiences and interactions. Its new battles take place in these areas:

* Participation in programming and computing has expanded from a niche population in academia, research, and scientific communities to a giant IT industry.    
* Computers have expanded from mainframes to personal computers, handheld devices (e.g., POS scanners), smartphones, and anything with a CPU that can run programs.    
* Programming and computing environments have expanded from processors with a single CPU to multi-CPU (aka multi-core) processors, networked computers (e.g., programs running on a company's network or cloud), and the Internet, which connects everything (with a CPU) and everyone (via a device and a program) 24/7.

This shift implies several things. First, there were two eras—the former focused on invention and the latter on applying programming techniques in broader domains. Second, the meaning of programming has changed from programming a simple computer to programming many multi-core and networked computers (essentially, "programming the Internet").

Let us use automobiles as an analogy once more. The programming industry has gone from inventing the car to exploring what a single car can do for people. Now, it controls the actions of multiple vehicles from a coordinated business objective.

Therefore, we need to reevaluate the evolving path of programming and recalibrate its direction by examining two fronts: whether OOP is sufficient for **programming the Internet** and what (other than OOP) has kept us moving forward to more complex, efficient applications.

Programming the Internet requires techniques for concurrent and distributed programming. Although modern OOP languages have added more user-friendly features to support multi-threading, the object model behind OOP lacks a mechanism for concurrency. Efforts were made in the past, such as Carl Hewitt's Actor model in 1973 and Greg Lavender and Douglas Schmidt's Active Object pattern in 1996, but mainstream programmers have yet to adopt them.

The object model also lacks a mechanism for distributed programming. Similarly, efforts such as the Common Object Request Broker Architecture (CORBA), Distributed Component Object Model (DCOM), and Java Remote Method Invocation (RMI) were made but have yet to be widely utilized. As a result, hardware and software architectures, frameworks, and patterns—such as middleware and microservices with RESTful APIs as interfaces—have kept us moving forward with programming the Internet.

Based on these observations about potential bottlenecks in programming the Internet in 2024 and beyond, it's clear that we need a **unified programming model** that can handle concurrency, intra-process programming (e.g., at the level of a programming language), and inter-process programming (e.g., at the level of many programs running on many computers). The model should be human-centered, meaning intuitive and instinctive to people. We already have the steering crank; the goal is to invent the steering wheel.

# Part 2 — Lemina Programming Model

In Part 1, we explored programming's current state and its future direction. This insight helps us judge whether a new technique aligns with the evolutionary path and guides us in crafting new ones. To develop a **unified programming model**, I analyzed the core behaviors and mechanisms of existing techniques, comparing them to how people collaborate in social and business settings. Then, I adapted models from human social behavior to design a programming model reflecting these principles. The result was the **Lemina Programming Model**.

In a fundamental sense, a CPU executes a program by executing one statement (or line of code) at a time. To illustrate program execution to non-IT people, we can use the train, track, and sleeper analogy. A train represents a CPU, a track represents a program, and a sleeper represents machine code or a line of code. A train running over sleepers under the track represents a CPU executing code in the program.

In the early days of programming, even in the late 1940s, a computer might not support the concept of a subroutine or procedure. For example, the Manchester Baby (the first electronic stored-program computer, built at the University of Manchester in 1948\) only supported eight instructions, none of which included calling a subroutine. These rudimentary programs can be viewed as one-dimensional (1D) in structure because all their code lies linearly as a one-dimensional line, with all sleepers under the main track.

Programs using procedures can be viewed as two-dimensional (2D) since each has a track parallel to the main track, lying in a two-dimensional area. The train runs down the main track, teleports to the procedure's track, and continues running when it encounters a "call procedure" sleeper on the main track. The train then stores the position next to the call procedure sleeper on the main track in the stack so it can teleport back to where it left off when it finishes the procedure's track. We use "teleport" to describe the move when a CPU "jumps" instantly to the beginning address of another track, though there's no analogous function in an actual train.

Now, let us add objects to the picture. An object in the program can be viewed as several tracks (the methods owned by the object), with private data enclosed by a fence. However, programs with objects are still 2D programs.

Multi-core CPUs bring multiple trains to execute the same program simultaneously, a requirement for most modern programs. Having a train for each procedure track expedites lengthy calculations since more hands on deck speed up the entire program. Another typical example of needing multi-core CPUs is when programs run as servers that support many simultaneous clients.

Having multiple trains in a program adds a new dimension. We can view programs with multi-threading at runtime as "3D programs." However, this also leads to new programming challenges. When one train does everything, it knows and has all the information. But how do multiple trains interact when they perform functions simultaneously? Should the main train wait or continue while the procedure train is running? If the main train doesn't wait and the procedure train has new results to report, how can it receive them mid-process?

In programming, these interactions are called synchronous and asynchronous procedure invocations. On the one hand, a caller can obtain a callee's results for a sync invocation because it waits on the spot. However, for an async invocation, the caller immediately moves forward. Thus, it's difficult for the caller to obtain the callee's results because there should be a new arrangement in another time and space for the results to change hands. Popular solutions for getting async results include Future, Promise, and Callback with Closure. These solutions work as expected, but their styles are more tech-oriented and less intuitive than many modern programmers would prefer.

In Part 1, we considered objects a new life element in the programming world. Objects have addressed the structural aspect of the issues caused by code complexity but have yet to address the behavioral aspect of the problems caused by concurrency (on the same or different computers). In other words, objects are revolutionary but still half-baked, requiring improvements to behave more like independent life elements in the modern programming world.

These analyses point to one solution direction: a unified, human-centered design for handling sync and async procedure invocations within and across programs (and computers).

I started to find this direction by examining the similarities between 3D programs and human societies. People live on the Earth's surface, which can be viewed as a 2D space. Within that space, everyone carries out their own decisions and actions with their bodies, which can be viewed as the third dimension—the dimension of thinking and action. Thus, both programs and societies similarly define the 3D context. Recognizing this, I examined how people interact in societies to perform social and business activities. I became convinced that the real-world postal service model can serve as an infrastructure for 3D programs in a new unified programming model.

Thus, I borrowed models and concepts from real-world postal services to create the new **Lemina programming model**, which introduces two programming elements: **Lemina (postal) services** and **leminas**. Real-world postal services send mail to registered recipients on behalf of anonymous senders. Lemina services behave similarly by delivering messages to registered recipients on behalf of anonymous senders, where senders could be any code, including leminas.

I intentionally chose "lemina," a personified name, over a traditional name in programming, like an object or actor, for several reasons:

* To pay tribute to real-world models and concepts    
* To indicate that the Lemina model is a human-centered design    
* To emphasize that leminas are not objects or actors but could be implemented by objects, actors, or even procedures as long as they comply with the Lemina model

The Lemina model aims to replace procedure invocation with **message passing**. Procedure invocation is deeply rooted in the mindset that one thread of execution (e.g., a train) performs actions on both the caller and callee sides, while the mentality of message passing is between two independent entities (e.g., humans or programming elements). "Procedure" in this context also means functions, methods, subprograms, subroutines, etc. These terms are interchangeable in this discussion.

Procedure invocation is a low-level, technical mechanism of how the CPU works. We cannot replace it with the Lemina model, which is a higher abstraction. "Replacing" means that procedure invocation has overreached into unsuitable places in programming. Therefore, we replace it in these situations with the Lemina model.

The procedure invocation works this way: caller → procedure. The Lemina model inserts a middleman between the caller and procedure: caller → outbox → Lemina service → inbox → lemina, where lemina represents a procedure.

The Lemina model requires a Lemina service to provide a public outbox for every user and a private inbox for each lemina, as the outbox and inbox are part of the Lemina service. The outbox and inbox are named from the sender's and lemina's perspectives, respectively. Thus, the original procedure invocation is replaced by two separate invocations: one between the caller and the Lemina service (via outbox) and the other between the Lemina service and lemina (via inbox).

For programming the Internet, the Lemina model works through networked Lemina services: caller → outbox → source Lemina service → {networked Lemina services} → target Lemina service → inbox → lemina. Thus, the caller, lemina, and programming style remain unchanged across different configurations of Lemina services.

In summary, the invocation model (which is supported by high-level, object-oriented languages for intra-process programming):

* Caller → procedure

Is successfully converted to the Lemina model (for intra-process and inter-process programming):

* Caller → outbox → {Lemina service(s)} → inbox → lemina

It can be further abstracted as a one-way message-passing model where one message passing between the sender, and lemina comprises two invocations: one between the caller and outbox and the other between the inbox and lemina:

* Sender → {Lemina service(s)} → lemina

The **Lemina Programming Model** leverages four foundational mechanisms to meet its design goals:

* **Textual ID**    
* **Reply-to**    
* **Localization**    
* **Namespace**

## Textual ID

In the real world, recipients registered with postal services use addresses for delivery instead of their real names. Addresses, tied to houses (or, more precisely, the lots they're built on), are **deliverable** where names aren't. In contrast, there is no difference between names and addresses in the digital world. Thus, lemina ID, name, and address are interchangeable terms in the Lemina model.

The Lemina model defines lemina IDs as **textual**. Textual ID is the cornerstone of the Lemina model, enabling or improving several key factors:

* Referenceability    
* Reachability    
* Human-style reply-to mechanism

**Referenceability** enables all people, not just those with IT knowledge, to use lemina names directly in their thought processes. People can talk about lemina names, pass lemina names to others via phone, design business processes with lemina names, etc.

**Reachability** ensures successful message delivery to leminas, whether in the same program or over the Internet. Notably, messages should also be textual to be delivered across different programming languages, computers, networks, etc. Textual content is not a technical requirement for cross-internet delivery but is compatible with all existing protocols and infrastructures.

**The human-style reply-to mechanism** is for async messages (e.g., two-way messages that return results). People perform async interactions by asking someone to do work and leaving a reply-to address for the person to return the results. Textual ID ensures the reachability of reply-to messages.

A lemina could represent or be implemented by a procedure, multiple procedures, an object with methods, or even multiple objects. In the case of representing multiple entities, further internal addressing is needed to target a particular entity. The Lemina model further defines an **attention name mechanism** for lemina internal addressing, inspired by real-world addressing on an envelope with "attention." Attention names are separated from the lemina name by a pound sign "\#," for example, "Alice\#place-order," "Alice\#cancel-order," and "shipping-team\#ship-order." On that note, lemina names should be case-insensitive to avoid being prone to human usage errors.

## Reply-to

The Lemina model's core function is one-way message passing. A sender can send a message by name using outbox. The syntax below is for illustration purposes, as outbox details will be implementation-dependent:

* outbox.send("Alice\#place-order", \<message\>)

Notably, outbox messages are one-way. From the sender's point of view, they act in a send-and-forget style.

Our earlier analysis concluded that performing async invocation is easy while getting results is difficult. The Lemina model introduces the **reply-to mechanism** to replace current technical solutions such as Future, Promise, and Callback with Closure.

The reply-to mechanism adds a reply-to address to the outgoing message so that the lemina (or its parent Lemina service) wraps its results in a new message sent to the reply-to address:

* outbox.send("send-to: Alice\#place-order", "reply-to: shipping-team\#ship-order", \<message\>)

Remember that lemina ID, lemina name, and lemina address are interchangeable terms that refer to the same thing. Therefore, users should treat the send-to and reply-to labels above as comments that are not part of the definition of the Lemina model.

This way, the "shipping-team" lemina will receive the results at the attention "ship-order." But what if a programmer has legacy code or wants to obtain the results in place? Put another way, how can you serve a sync message on a lemina?

The Lemina model doesn't support any sync function at its core, so the burden is placed on the outbox by design. The outbox will handle a sync invocation like this:

* \<results\> \= outbox.await("Alice\#place-order", \<message\>)

The outbox's implementation can achieve the await() by using two one-way messages. For example, an outbox receiving an await() call can internally create a new lemina, register it with its parent Lemina service, add the new lemina name to the message, and convert it to a reply-to message. When the new lemina receives a return message, the outbox then passes the results in the return message back to the waiting caller.

## Localization

The Lemina model's core component is the Lemina service: caller → outbox → Lemina service → inbox → lemina. Implementing the Lemina service also covers the outbox and inbox because they are part of the Lemina service as defined by the Lemina model.

Modern programmers have hundreds of languages available, each of which may implement the Lemina service. Additionally, programmers may have different designs within the same language. Since the total number of implementations is nearly limitless, the Lemina model cannot provide a one-size-fits-all design or definition for every possibility. Thus, it is where **locality** comes in.

Locality refers to the principle that programmers can implement Lemina services however they prefer, provided the results align with the Lemina model's core principle. This principle can be summarized: if a caller has a lemina name and access to an outbox, then the caller can send the lemina a one-way message. Of course, the compatibility of individual messages can lead to new challenges. Let us use a real-world example. You can write someone a letter in English if you know their address, but the recipient may only understand French. That won't be the postal service's fault since the sender should know the recipient. The same is true for leminas.

For example, let us explore two different designs for implementing a Lemina service using the same programming language, Java, to illustrate how locality helps everyone participate in the Lemina world to solve existing and emerging programming challenges.

There is a legacy class, "Sales," with methods like "placeOrder," "cancelOrder," etc.

To illustrate these methods, let us design two Lemina services in Java, one for sync invocation and the other for async invocation.

The former will demonstrate that the Lemina model can maintain the legacy program in the same style; the latter will prove that the Lemina model can convert legacy code to concurrency.

### Design for sync invocation

The Lemina service offers an outbox as usual but doesn't provide inboxes for leminas because the Lemina service and leminas work privately and locally. The Lemina service internally uses a map to store all mappings between lemina names and Java object instances (namely, leminas).  
Legacy code:

* sales.placeOrder(\<parameters\>)

Converted Lemina style for sync invocations:

* outbox.call("sales\#placeOrder", \<parameters\>)

After receiving this call via the outbox, the Lemina service lets the caller's thread continue executing the following internal logic:

* Retrieve the sales instance from the mapping by the name "sales."    
* Retrieve the method instance on the sales instance using the Java reflection feature based on the attention "placeOrder" as the method name.    
* Invoke the method sales.placeOrder(\<parameters\>) with parameters.

Thus, the caller's thread executes all implementation logic, and the overall invocation remains synchronous.

### Design for async invocation

The Lemina service offers an outbox for the public and a private inbox for each lemina. A lemina's mapping will include the lemina name, inbox, and a Java object instance.  
Legacy code:

* sales.placeOrder(\<parameters\>)

Converted Lemina style for async invocations (minus the results to make the example simpler):

* outbox.call("sales\#placeOrder", \<parameters\>)

In this implementation, the caller's thread retrieves the mapping by the lemina name, puts parameters in the inbox, and returns immediately, allowing the caller to complete an async invocation.

Notably, the Lemina service uses a thread from its internal thread pool and loops the inbox for this lemina. For every loop, the service thread retrieves a set of parameters in the order of their arrivals and executes the Java object sales.placeOrder(\<parameters\>) until the inbox is empty.

### Design for a combination of both sync and async

We can further merge the two implementations into one by localizing the method names of the outbox:

* outbox.syncCall("sales\#placeOrder", \<parameters\>)    
* outbox.asyncCall("sales\#placeOrder", \<parameters\>)

## Namespace

A Lemina service can work alone, and it can also work with other Lemina services through a connection called networked Lemina services. The Lemina model doesn't define any network topology or structure for networked Lemina services because the model doesn't want to promote a one-size-fits-all design. However, networked Lemina services create a potential challenge when a caller wants to call or message a lemina with the same name as other leminas registered with different Lemina services.

Therefore, the Lemina model defines a concept of **namespace** to address these duplicate name issues. A namespace is a scope:

* Consisting of one or more networked Lemina services    
* In which a specific lemina name structure or pattern is used    
* Where all lemina names have the same reachability through any Lemina service in the scope

**Example 1**: One namespace for a single Lemina service that contains the names "Alice" and "Bob."

A caller can reach all names registered with the Lemina service:

* outbox.send("Alice", \<message\>)    
* outbox.send("Bob", \<message\>)

**Example 2**: Three namespaces for the networked Lemina services "s1" and "s2," where s1 contains "Alice" and "Bob," and s2 contains "Charlie" and "David."

In this example, there are three namespaces:

* Namespace s1 contains Lemina service s1 and leminas Alice and Bob    
* Namespace s2 contains Lemina service s2 and leminas Charlie and David    
* Namespace s1s2 contains Lemina services s1 and s2 and leminas Alice, Bob, Charlie, and David

The Lemina service s1 understands namespaces s1 and s1s2 but doesn’t understand namespace s2:

* s1.outbox.send("Alice", \<message\>) → it works    
* s1.outbox.send("Bob", \<message\>) → it works    
* s1.outbox.send("Charlie", \<message\>) → it doesn’t work    
* s1.outbox.send("s2/David", \<message\>) → it works

The Lemina service s1 is part of namespace s1s2, so it understands the name pattern "s2/David."

**Example 3**: One namespace for the networked Lemina services "s1" and "s2," where s1 contains names "Alice" and "Bob," and s2 contains names "Charlie" and "David." Unlike in Example 2, Lemina services s1 and s2 decide to share a single namespace, which means they will share names and ensure no duplicate names when registering a new lemina on either side.

In this example, a caller can reach all leminas by their native lemina names via either Lemina service s1 or s2. There is no name pattern, as there is only one layer between Lemina services and leminas.

**Example 4**: A global namespace

Everyone is familiar with the Internet, but not everyone understands it from a network perspective. The same network protocols that create the Internet could be used to power more Internet instances. Other Internet instances utilize the same network protocols on a smaller scale, often designed for specific organizations, such as a business's employee intranet.

Similarly, we can use these network protocols and technologies to build a global instance of the Lemina namespace where everyone can participate. The advantage of this approach is that we don't have to start from scratch. We can use domain names as the top layer in the lemina name structure. For example, Amazon may publish a lemina name for public use:

* lemina://amazon.com/account/shopping-cart\#add-item

Again, we can name the global Lemina namespace a personified name: *Lemina World*. Thus, "Hello, Lemina\!" and "Lemina World" are inspired by the "Hello, World\!" program.

# Part 3 — Lemina Programming Model for Business Applications

"**Business applications**" refers to enterprise applications or software solutions for information systems. They include those that can be used across multiple industries, such as content management or accounting systems and those that apply only to certain types of companies, such as loan management or banking systems. These systems differ in application but share an ability to automate and improve business processes in their respective industries.

COBOL, designed in 1959, was the first programming language for business applications and a "common business-oriented language," as its name suggests. Since COBOL, many high-level programming languages have been used by businesses to build applications and improve their industry-specific workflows.

Today, modern business applications are Internet-based, structured in two tiers (e.g., a frontend and a backend), and usually built with popular OO languages like Java and JavaScript. These traits define the programming languages most commonly used by businesses as well as the skills most frequently desired in job postings for software engineers, including:

* An ability to write programs in popular object-oriented programming languages such as Java and JavaScript (AngularJS for the frontend and Node.js for the backend)    
* An ability to design applications that comply with the microservices architecture with RESTful APIs    
* An ability to deploy applications to one of the major cloud service providers (e.g., AWS, Azure, Google Cloud, etc.)

Parts 1 and 2 illustrated how programming evolved from the framework of a single computer to a network of computers and finally to modern Internet applications. In the past, high-level programming languages and the object model (OOP) were sufficient to accomplish basic and advanced programming tasks. However, in the age of Internet programming, the Lemina model offers a solution to the deficiencies in using current programming languages to create applications at the Internet scale.

Each stage of programming's evolution enhances knowledge and functionality without fully replacing proven methods. **High-level programming languages** automate repetitive tasks atop **machine code**. The object model introduces a new code unit—as vital as the first cells sparking life's evolution—with logic rooted in high-level languages. In other words, all OO languages are high-level. The **Lemina Programming Model** advances this process, teaching objects to collaborate and form **societies of objects**, dubbed the Lemina way of building programs.

Part 2 also demonstrated that by taking advantage of localization, one of the four core mechanisms of the Lemina model, we could implement a Lemina postal service that is backward compatible with OOP languages. Therefore, the Lemina model in backward-compatible mode can be used to build business applications like other OO languages.

However, backward compatibility is only part of the full context of the Lemina model's potential. Its real power comes from the mechanisms that make the model leap over the object model on programming's evolutionary path. With the Lemina model, businesses can personify leminas as employees or roles and apply their organizing skills seamlessly to leminas and employees in the early planning and design phases.

A lemina has a textual name and a list of attention names. We name leminas with human or role names and use the naming convention of verb \+ noun for its attention names to more clearly represent employees or roles in business processes. At the same time, an actual employee or role also appears as a name and a list of tasks in the business process. Thus, leminas and employees establish a one-to-one mapping relationship in the business process context.

Businesses organize their activities as business processes and use tools such as BPMN (Business Process Model and Notation) or UML (Unified Modeling Language) to design and describe business processes.

UML has two behavior diagrams: the activity diagram and the use case diagram. The activity diagram contains activities and condition checks but doesn't specify who will perform them. In this case, the business process owner or manager should refine the activity diagram into a Lemina activity diagram by denoting the number of leminas involved and marking each activity to its owning lemina. Conversely, leminas can directly replace the actors in the use case diagram.

BPMN has only one pool diagram, which is similar to UML's activity diagram but with two enhancements. First, a pool uses multiple lanes to represent employees or roles who will perform the activities. Second, BPMN uses gateways to represent condition checks on splitting and merging. Thus, leminas can directly replace lanes in the pool.

So far, we have reviewed how the Lemina model can be used as an OO language to build business applications and model high-level business behaviors. In the rest of Part 3, we will focus on modeling business data in the Lemina way.

Let us start with a pool, which represents a business process. A pool may have one or more lanes, each representing an employee or role. Since we use a lemina to implement a lane, all activities in the lane will become the lemina's internal attention names.

Thus, the lemina will need two types of information to perform the activities. The first is the information activities required for the lemina to coordinate itself, including overall status, each activity's status, partial results, etc. We can call this kind of information administrative data, and it can exist at different scopes, including lane, pool, and cross-pool diagrams.

The second is information regarding the targets to which the activities apply actions. For businesses providing services, the targets could be shopping carts or bank accounts. For companies manufacturing goods, the targets could be data generated by goods or manufacturing processes. Usually, this type of information goes beyond business processes and belongs to the company's central business domain.

The admin data is usually private to its scope and has a one-to-one relationship with it. On the other hand, a business process is generally independent of the domain data and has a one-to-many relationship: a business process or an activity may operate on multiple domain data items. For example, a worker must update the assembly line inventory for ten parts (minus one for each) and the toy (plus one) when assembling a toy with ten parts on an assembly line. At the same time, other business processes may use the same domain data. Hence, at a broader scope, it is a many-to-many relationship between business processes and domain data.

There are hundreds, if not thousands, of industries worldwide. Companies have their ways of doing business, even within the same industry. For example, one bank offers a checking account that doesn't charge a monthly fee, while another may waive the fee if the account's daily balance is over $500. This situation makes designing standard data models or structures for each industry impossible since every industry and business would require new parameters for program functions to accommodate.

However, we still need a commonality when discussing and working with data because the only association between the reality of a business's operations and the functionality of its computers is the organization of its data. When things happen in the real world, computers learn about them through data generated by or for the events. Similarly, when computers (programmed by people, of course) want to impact the world, they create data to let people react (e.g., passively, such as a report) or drive devices (e.g., actively, such as an industrial robot) to perform physical actions.

I created two data concepts, **Account** and **Event**, to allow us to reference relevant data before complete data structures become available while modeling business process behaviors.

"Account" is an overloaded term with many meanings. When joined with another noun in a noun-noun collocation, such as a bank account, customer account, email account, or Google account, the *Merriam-Webster* dictionary defines it in two ways:

* Entry 3-a-(1) — A formal business arrangement providing for regular dealings or services (such as banking, advertising, or store credit) and involving the establishment and maintenance of an account    
* Entry 3-b — An arrangement in which a person uses the Internet or email services of a particular company

The arrangements defined in the two entries are the same, as both refer to an arrangement between an account provider and holder, where the holder could be a subject (e.g., a person, a thing, etc.) or a concern.

A Lemina account is such an arrangement since it is abstract until associated with a subject, which could be an entity in the business domain, such as a bank account or an inventory account, or a representation of a business process's admin data, such as a place-order process account.

More specifically, a Lemina account's arrangement refers to a group of relevant data items regarding a subject or concern. These data items will change based on Lemina events throughout the account's lifespan.

Abstract Lemina accounts and events provide identification information. An account contains two fields:

* Account type or name    
* Account instance ID or number

An event contains four fields, two of which point to the parent account instance:

* Account type    
* Account instance ID    
* Event type    
* Event instance ID

A good analogy is using paper to record an account's data structure by writing the header section with identifications before we have details. This piece of paper serves as a placeholder to provide referenceability. Now, this account can participate in our thought processes and help us model business process behaviors.

This **account-centered approach** also aligns business and IT people in breaking down data structures while modeling data. Thus, business people can participate in data structure design as well.

Before closing Part 3, let us assemble a picture of how the Lemina model builds business applications.

First, we use BPMN or UML to model business process behaviors and refine them by replacing BPMN lanes or UML actors with leminas (it is also possible to model the behaviors directly with leminas). In this portion, leminas perform activities and condition checks in the business processes.

Once the process is established, we identify accounts and events. For identified accounts and events, we can start with the primary identification information (e.g., type and ID) and refine the data structure throughout the modeling and design process.

For each account, we can assign a lemina and equip the lemina with the knowledge or business logic required to apply changes to the account based on the received events.

Thus, we have a group of leminas that perform activities and another group of leminas that perform bookkeeping against accounts. As mentioned earlier, these leminas interact in a many-to-many relationship. A behavior lemina may coordinate several account leminas to complete one activity; for example, after the toy-assembling activity, the behavior lemina needs to update the inventory for the toy and the other ten parts, which are eleven account instances if they all belong to the same account type.

By coordinating, Lemina groups can model business applications more efficiently than past programming methods. However, the development process for business applications comes with unique challenges that we will address in Part 4\.

# Part 4 — Lemina Business Application Development

The Lemina programming model can model business applications in three steps.

Step 1 is to create Lemina accounts for data structures of business processes and domain subjects. A Lemina account is a placeholder and container of data items related to a particular business concern or arrangement, such as a checking account, customer account, or business process admin account. Usually, we start to identify and realize data items late during the business requirement elicitation and analysis phases. Therefore, we need placeholders for reference before data items come to life.

An account has a type name, and an instance of that type will have an instance ID. Some accounts may contain constants. For example, an account instance with the type name "business holidays" and instance ID "2024" includes all business-recognized holidays in 2024 for receiving payments, which would remain unchanged.

However, most accounts will change throughout their lifespans, and Lemina's accounts cannot change without a trace. Lemina events are designed to trigger changes against account instances and carry all necessary data to complete the account changes. Similarly, a Lemina event has the concepts of type and instance. An event instance specifies an account type name, an account instance ID, an event type name, and an event instance ID. A significant difference between accounts and events is that events are historical records that cannot change after they occur, while accounts can.

Step 2 is to utilize the lemina's flexibility to represent various entities in different contexts. The native context is a Lemina postal service in which a lemina is a recipient uniquely identified by its name. In this context, a lemina represents an individual. In a slightly extended context, a lemina represents an organization, as a lemina further supports internal addressing by specifying attention.

Outside the postal service, a lemina can represent an individual in a business context. Businesses hire people based on skills relevant to their positions (such as taking an order or canceling an order) rather than irrelevant skills (such as fishing or hunting). In such a context, an individual is viewed in a computer model as an entity identified by name with a list of skills, behaviors, or actions. Thus, leminas can represent individuals in business when skills are associated with attention.

Let's switch to a third context where leminas can represent Lemina accounts. More precisely, a lemina represents an individual with the knowledge and skills to apply all events to the associated account. When we associate the lemina with the account and the lemina's skills with the account's events, we effectively use the lemina to represent the Lemina account.

Please note that a lemina represents a type of account. When applying a specific event, the lemina will retrieve the account instance specified by the event and operate on that instance. It is the typical way to use leminas to model accounts, but there could be other ways. Remember, the Lemina model opens the door to how people behave and socialize by using societal patterns.

Step 3 is to reveal the big picture of a business application model. A business application, or any software application, consists of behaviors and data. Business behaviors are usually modeled as business processes, each containing a set of business activities. The details of behaviors are laid out in each activity as business logic. Together with a set of domain data structures, all the details provide a raw view of the business application.

Step 1 refines the above raw view by introducing Lemina accounts and events for business processes and domain subjects. Thus, business logic is transferred into events. For example, placing an order is an activity in a business process that is then converted into an event against the business process admin account representing the business process. This event knows the business logic for charging the customer against the customer's payment account and reducing the inventory against the product's inventory account. Then, this event will issue two more events against the domain accounts: the customer's payment account and the product's inventory account. Similarly, the two domain events know the business logic for updating their accounts accordingly.

Step 2 further refines the updated model from Step 1 using leminas to represent business process admin and business domain accounts. As a result of these two steps, the Lemina model can produce a general business application model comprising a set of leminas representing business process admin accounts and a separate set of leminas representing business domain accounts. Notably, all business logic is associated with events, so all accounts are central to the Lemina model's view.

A general model enables a general model implementation, which provides at least two sets of essential functions. The first set displays and examines Lemina's account and event contents by browsing and searching account types, account instances of a selected account type, and events of a selected account instance.

The second set accepts one or more consecutive events and applies them to the specified account instance by executing their logic (remember, business logic is associated with events). As business logic is invisible, examining its correctness involves comparing the before-and-after contents of the account instances it impacted. Thus, the model implementation can support manual verification and automated testing.

The Lemina method for business application development creates an environment that can streamline any new addition or update (including data items, business logic, business process flows, test cases, etc.). In the real world, there are already development environments for software engineers called CI/CD, which stands for Continuous Integration and Continuous Deployment. However, the Lemina development environment further covers requirement management with its unique process automation and streamlining features.

The **Lemina method** employs three techniques to meet its goals. The first is an **all-in-one document**, encompassing requirements, data structures, business logic, and the source code that brings it to life. Ideally, it's written in *Markdown syntax*—text-based (easing Pull Request diffs) and simple enough for anyone familiar with office software to grasp in days. An all-in-one document represents and describes a Lemina account type or event type with multiple sections:

* A form that visually represents data items    
  * Mainly for people's consumption (e.g., U.S. Tax Return Form 1040\)    
  * To display data contents on the screen  
* A JSON structure that represents data items    
  * Mainly for computer consumption (e.g., data types in code)    
  * JSON is also friendly to people (most business analysts understand JSON)  
* Detailed explanation for every data item (e.g., Form 1040 Instructions)

If it is an account type, it has extra sections:

* A list of event types owned by this account type

If it is an event type, it has extra sections:

* An account type owning this event type    
* Detailed business logic, including natural language and pseudocode, for how to apply changes to the specified account instance    
* A code file name that contains the actual source code for the business logic (unfortunately, code will be in a separate file until an IDE can extract code from an all-in-one document)

The second technique is a Git repository from a vendor such as GitHub or GitLab. The Git repository stores all-in-one documents for all Lemina accounts and events. Thus, we manage requirement changes like code changes through PRs (Pull Requests).

The third technique is a customized build tool (e.g., Maven or Gradle) that pulls code files from all-in-one documents and creates a model implementation. A base model implementation should be developed before the first all-in-one document exists.

With these techniques, the Lemina method provides some immediate benefits. First, since all information is stored in one Git repository, all users remain aware of the full context of the business application. For a business application to be developed simultaneously by dozens or hundreds of people, users must understand what they are doing, what other users are doing, and why everyone is collectively performing specific actions at specific times. This situational awareness of the application's functions and goals improves overall efficiency, increases the odds of project success, and reduces the risks of project failures and delays.

Second, the Git Pull Request (PR) mechanism prevents conflicts by overlapping across teams as a last resort when a PR contains all related data items, business logic, and source code changes. Usually, the first defense to avoid such conflicts is to designate well-arranged features or areas for each team to work on. However, teams will get closer as progress enters the late stages due to different reasons:

* The nature of the application may not have precise edges among its features.    
* The deadline is approaching, so more teams are working in the same area.    
* Some teams are idle and would benefit from joining the project.    
* Teams step on each other's toes accidentally.

The PR mechanism doesn't prevent conflicts from happening beforehand but prevents them from being committed. Fixing such conflicts earlier saves the business money and mitigates the risk of liabilities.

Finally, a unit of work (e.g., a PR by a team in a sprint) will contain work regarding requirement elicitation or adjustment, design, coding, and testing, which covers the unit of work's entire life cycle. As a result, the unit of work is more independent and forms a feedback loop. This situation perfectly demonstrates agile principles.

Drawing from *CVT* (continuously variable transmission), I've named the Lemina method's fine-grained agility *CVA* (A for agility).

The Lemina development method for business applications delivers benefits in process efficiency and performance management. Yet, the Lemina method aims to bring additional benefits to enterprises at the strategic level. It can be summed up as enabling business people to complete the full development of their applications up to functional reference implementations without needing IT people (or keeping them to a minimum). A **functional reference implementation** refers to the model implementation equipped with features for all functional requirements but no features for nonfunctional requirements, which will be left to IT people.

Here is a brief explanation of how everything mentioned above makes this possible using the Lemina development method.

### Use forms to represent data structures.

The use of forms bridges the gap between business and IT mindsets. Before computers were invented, people performed business activities with universally understood forms. It is natural for business people to analyze business processes and activities and use forms to represent the data needed for those processes and activities.

On the other hand, forms and JSON have the same expressiveness regarding data and data structure, so they can easily be converted.

### Create small and well-defined contexts for implementation.

Business logic is associated with activities in the business processes, activities are associated with events, and events are associated with attention in leminas. So, lemina attention is the context and unit of code that handles an event and implements the event's business logic.

Lemina attention is a well-defined context that includes at least the event instance, the specified account instance, and other account instances that may be involved according to business logic.

Programming business logic in a clearly defined context is straightforward, even for non-IT people. Computer programming has been taught in colleges for all majors since the 1990s, so it is safe to claim that most business analysts, who are specialized business people, know how to program in this situation.

### Utilize functional reference implementations.

The ideal development environment should provide a base model implementation and a customized build tool before development starts. Thus, once it has been reviewed, approved, and merged, every PR containing changes for requirements, data items, business logic, and source code will be built and deployed into the running model implementation for manual verification and automated testing. When equipped with business features and functions, the model implementation becomes a functional reference implementation.

Adam Smith opens *The Wealth of Nations* with these words: "The greatest improvement in the productive powers of labour … seem to have been the effects of the division of labour." In the programming world, the original model of the lone programmer creating the building blocks of applications and networks has given way to teams of people with various experience levels coding smaller programs within the broader context of the project. Today, IT teams take the work of business people and wire it together into final production applications, adding features for nonfunctional requirements like performance, security, usability, reliability, and scalability.

While IT teams won't touch the functional reference implementation, they will assemble data structures and code from the Git repository to create a production implementation with nonfunctional features. The Lemina method expects these two implementations to run in parallel throughout their lifespans to ensure business people have a dedicated implementation they can reference for verification or continuous development, even as their operations scale in size and objective. Further division or specialization of labor is the next step on the programming evolutionary path, requiring a consolidated solution like the Lemina model to integrate the business reference implementation with IT finalization for the next generation of Internet applications.  


© Copyright 2024 Rex Young. All Rights Reserved.
