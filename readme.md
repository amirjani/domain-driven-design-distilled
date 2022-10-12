# Domain Driven Design 

To understand the problem, you have to understand the context within which it exists—the organization’s business strategy, and what value it seeks to gain by building the software.

**Subdomain Types**
- Core: A core subdomain is what a company does differently from its competitors. This may involve inventing new products or services or reducing costs by optimizing existing processes. The core subdomain is the heart of the business.
- Supporting: As the name suggests, supporting subdomains support the company’s business. However, contrary to core subdomains, supporting subdomains do not provide any competitive advantage.
- Generic: Generic subdomains are business activities that all companies are performing in the same way. _generic subdomains do not provide any competitive edge for the company_ 

## Business Domain
A business domain defines a company’s main area of activity. Generally speaking, it’s the service the company provides to its clients.
_A company can operate in multiple business domains._ 

## Subdomain
To achieve its business domain’s goals and targets, a company has to operate in multiple subdomains. A subdomain is a fine-grained area of business activity. _The subdomains have to interact with each other to achieve the company’s goals in its business domain._ 

![Subdomain Types](./assets/subdomains-compare.png)

Contrary to the core subdomains, supporting subdomains do not change often. 

All subdomains are required for the company to work in its business domain. The subdomains are like foundational building blocks: take one away and the whole structure may fall. Since core subdomains’ requirements are expected to change often and continuously, the solution must be maintainable and easy to evolve. Thus, core subdomains require the implementation of the most advanced engineering techniques

![Subdomain Differ](./assets/subdomains-differ.png)

![Domain Schematic](./assets/domain-schematic.png)

> It’s developers’ (mis)understanding, not domain experts’ knowledge, that gets released in production.

domain experts: it’s their job to specialize in and comprehend all the intricacies of the business domain. By no means should we, nor can we, become domain experts. That said, it’s crucial for us to understand domain experts and to use the same business terminology they use.

> As Alberto Brandolini1 says, software development is a learning process; working code is a side effect. A software project’s success depends on the effectiveness of knowledge sharing between domain experts and software engineers. We have to understand the problem in order to solve it

Research into why software projects fail has shown that effective communication is essential for knowledge sharing and project success

![knowledge sharing](./assets/knowledge-sharing.png)

During the traditional software development lifecycle, the domain knowledge is “translated” into an engineer-friendly form known as an analysis model, which is a description of the system’s requirements rather than an understanding of the business domain behind it. While the intentions may be good, such mediation is hazardous to knowledge sharing. 

## Ubiquitous Language
Using a ubiquitous language is the cornerstone practice of domain-driven design. The idea is simple: if parties need to communicate efficiently, instead of relying on translations, they have to speak the same language.

- Domain knowledge into an analysis model
- Analysis model into requirements
- Requirements into system design
- System design into source code

The ubiquitous language must be precise and consistent. It should eliminate the need for assumptions and should make the business domain’s logic explicit.

- each term of the ubiquitous language should have one and only one meaning
- Two terms cannot be used interchangeably in a ubiquitous language.

## Model
A model is a simplified representation of a thing or phenomenon that intentionally emphasizes certain aspects while ignoring others. Abstraction with a specific use in mind. _A model is not a copy of the real world but a human construct that helps us make sense of real-world systems._ 

**All models have a purpose, and an effective model contains only the details needed to fulfill its purpose** In its essence, a model is an abstraction. The notion of abstraction allows us to handle complexity by omitting unnecessary details and leaving only what’s needed for solving the problem at hand.
> the purpose of abstracting is not to be vague but to create a new semantic level in which one can be absolutely precise.

Despite the obvious advantages of maintaining a glossary of project-related terminology, it has an inherent limitation. Glossaries work best for “nouns”: names of entities, processes, roles, and so on. Although nouns are important, capturing the behavior is crucial.

“jack of all trades, master of none.” Such models are supposed to be suitable for everything but eventually are effective for nothing.

## Bounded Context
The solution in domain-driven design is trivial: divide the ubiquitous language into multiple smaller languages, then assign each one to the explicit context in which it can be applied: its bounded context.


In a sense, terminology conflicts and implicit contexts are an inherent part of any decent-sized business. With the bounded context pattern, the contexts are modeled as an explicit and integral part of the business domain.

### Model Boundaries

A model cannot exist without a boundary; it will expand to become a copy of the real world.

Bounded contexts define the applicability of a ubiquitous language and of the model it represents. A language’s terminology, principles, and business rules are only consistent inside its bounded context. a ubiquitous language is ubiquitous only in the boundaries of its bounded context. 

A bounded context’s size, by itself, is not a deciding factor. Models shouldn’t necessarily be big or small. Models need to be useful. The wider the boundary of the ubiquitous language is, the harder it is to keep it consistent. The smaller they are, the more integration overhead the design induces.

Therefore, keep your models useful and align the bounded contexts’ sizes with your business needs and organizational constraints.

Having a one-to-one relationship between bounded contexts and subdomains can be perfectly reasonable in some scenarios. In others, however, different decomposition strategies can be more suitable.

As we discussed earlier, a bounded context can contain multiple subdomains. In such a case, the bounded context is a physical boundary, while each of its subdomains is a logical boundary. Logical boundaries bear different names in different programming languages: namespaces, modules, or packages.

It can be said that domain-driven design’s bounded contexts are based on the lexicographical notion of semantic domains. A semantic domain is defined as an area of meaning and the words used to talk about it. For example, the words monitor, port, and processor have different meanings in the software and hardware engineering semantic domains.


## Integrating Bounded Contexts
Moreover, models in different bounded contexts can be evolved and implemented independently. That said, bounded contexts themselves are not independent. Just as a system cannot be built out of independent components—the components have to interact with one another to achieve the system’s overarching goals—so, too, do the implementations in bounded contexts. Although they can evolve independently, they have to integrate. As a result, there will always be touchdowns between bounded contexts. These are called contracts.


- **Partnership**

Bounded contexts are integrated in an ad hoc manner.
![Partnership](./assets/partnership.png)
- **Shared kernel**

Two or more bounded contexts are integrated by sharing a limited overlapping model that belongs to all participating bounded contexts.

It’s crucial to stress that the shared model is designed according to the needs of all of the bounded contexts.

![shared kernel](./assets/shared-kernel.png)

The overarching applicability criterion for the shared kernel pattern is the cost of duplication versus the cost of coordination 

the shared kernel will naturally be applied for the subdomains that change the most: the core subdomains.

- **Conformist**
![Customer Supplier](./assets/customer-supplier.png)
The consumer conforms to the service provider’s model.
![Conformist](./assets/conformist.png)
- **Anticorruption layer**

The consumer translates the service provider’s model into a model that fits the consumer’s needs.

![Anticorruption](./assets/anticorruption.png)

- **Open-host service**

The service provider implements a published language—a model optimized for its consumers’ needs.

![open-host](./assets/open-host.png)

![open-host](./assets/open-host-2.png)
- **Separate ways**
It’s less expensive to duplicate particular functionality than to collaborate and integrate it.

# Context Map

After analyzing the integration patterns between a system’s bounded contexts, we can plot them on a context map. The context map is a visual representation of the system’s bounded contexts and the integrations between them. 

![context map](./assets/context-map.png)