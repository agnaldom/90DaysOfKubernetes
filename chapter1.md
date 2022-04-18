# Chapeter 1. Introduction

Kubernetes is an open source archestrator for deploying containerized applications, It was originally deloped by Google, inspired by a decade of experience deploying scalable, reliable systems in containers via application-oriented APIs.

There are many reasons why people come to use containers and container APIs like Kubernetes, but we believe they can all be traced back to one of these benefits:

* Velocity
* Scaling (of both software and teams)
* Abstracting you infraestructure
* Efficiency

## Velocity

Velocity is the key component in nearly all software development today. The software industry has evolved from shipping products as boxed CDs or DVDs to software that is delivered over the network via web-based services that are updated hourly. This changing landscape means that the diference between you and your competitors is often the speed with which you can develop with which you can respond to innovations deloped by others. 

In this way, containers and Kubernets can provide the tools that you need to move quickly, while staying available. The core concepts that enable this are:

* Immutability
* Declarative configuration
* Online self-healing systems

### The Value of Immutability

Contianers and Kubernetes encourage developers to build distributed systems that addhere to the principles of immutable infraestructure systems that adhere to the principles of immutable infrastructure. With immutable infraestructure, once an artifact is created in the system it does not change via user modifications.

In an immutable system, rather than a series of incremental updates and changes, an entirely new, complete image is built, where the update simple replace the entire image with the newer image in a single operation. There are no incremental changes. As you can imagine, this is a significant shift from the more traditional world of configuration management.

To make this more concrete in the world of containers, consider two different ways to upgrade your software:

1. You can log in to a container, run a command to download your new software, kill the old server, and start the new one
2. You can build a new container image, push it to a container registry, kill the existing container, and start a new one.

The key differentiation is the artifact that you create, and the record of how you created it. These records make it easy to understand exactly the differences in some new version and, if something goes wrong, to determine what has changed and how to fix it.

Additionally, building a new image rather than modifying an existing one means the old image is still around, and can quickly be used for a rollback if an error accours. In contrast, onde you copy your new binary over an existing binary, such a rollback is nearly impossible.

Immutable container images are at the core of everything that you will build in Kubernetes. It is possible to imperatively change running containers, but this is an anti-pattern to be used only in extreme cases where there are no other options (e.g., if it is the only way to temporarily repair a mission-critical production system). And even then, the changes must also be recorded through a declarative configuration update at some later time, after the fire is out.

## Declarative Configuration

Immutability extends beyond containers running in your cluster to the way you describe your application to Kubernetes. Everything in Kubernetes is a declarative configuration object that represents the desired state of the system. It is the job of Kubernetes to ensure that the actual state of the world matches this desired state.

The idea of storing declarative configuration in source control is often referred to as "Infraestructure as code."

## Self-Healing Systems

Kubernetes is an online, self-healing system. When it receives desired state configuration, it does not simply take a set of actions to make the current state match the desired state a single time. It continuously takes actions to ensure that the current state matches the desired state. This means that not only will Kubernetes initialize your system, but it will guard it against any failures or perturbations that might destabilize the system and affect reliability

Online self-heling system improve developer velocity because the time and energy you might otherwise have spent on operations and maintence can instead be spent on developing and testing new features.

In a more advanced form of slf-healing, there has been significant recent work int he operator paradigm for Kubernetes. With operators, more advanced logic needed to maintain, scale, and heal a specfic piece of software (MySQl, for example) is encoded into an operator apllication that run as container in the cluster.

## Sacaling Your Service and Your Teams

As your product grows, it's invetitable that you will need to scale both your software and the teams that develop it. Fortunately, Kubernetes can gelp with bolth of these goals. Kubernetes archieves scalability by favoring decoupled architectures. 

### Decoupling

In a decourpled architecture, each component is separated from other components by defined APIs and service load balancers. APIs and load balancers isolate each piece of the saystem from the others. APIs provide a buffer between implementer and consumer, and load balancers provide a buffer between running instances of each services.

Decoupling components via load balancers makes it easy to scale the programs that make up your service, because increasing the size (and therefore the capacity) of the program can be done without adjusting or reconfiguring any of the other layers of your service.

Decoupling servers via APIs makes it easier to scale the develpment teams because each team can focus on a single smaller microservice with a comprehensible surface area. Crisp APIs between microservices limit the amount of cross-team communication overhead required to build and deploy software. This communication overhead is often the major restricting factor when scaling teams.

### Easy Scaling for Applications and Clusters

Concretely, when you need to scale your service, the immutable, declarative nature of Kubernetes makes this scalling trival to implement. Because your containers are immutable, and the number of replicas is merely a number in a declarative config, scaling your service upward is imply a matter of changing a number in a configuration file, asserting this new declarative state to Kubernetes, and letting it take care of the rest. Alternatively, you can set up autoscaling and let Kubernetes take care of it for you.

### Scalling Development Teams with Microservices

The common solution to this tension has been the development of decoupled, service-oriented teams that each build a single microservice. Each small team is responsible for the design and delivery of a service that is consumed by other small teams. The aggregation of all of these services ultimately provides the implementation of the overall product's surface area.

Kubernetes provides numerous abstractions and APIs, that make it easier to build these decoupled microservice architectures:

* Pods, or groups of containers, can group tagether container images develped by different teams into a single deployable unit.
* Kubernets services provide load balancing, naming, and discovery to isolate one microservice from another.
* Namespaces provide isolation and access control, so that each microservice con control the degree to which other services interact with it.
* Ingress objects provide an easy-to-use frontend that can combine multiple microservices into a single externalizad API surface area.

Finally, decoupling the application container image and machine means that different microservices can colocate on the same machine without interfering with one another, reducing the overhead and cost of microservice architectures. The health-checking and rollout features of Kubernetes guarantee a consistent approach to application rollout and reliability that ensure that a proliferation of different approaches to service production lifecycle and operations.

### Separation of Concerns for Consistency and Scaling

In addition to the consistency that Kubernetes brings to operations, the decoupling and separation of concerns produced by the Kubernetes stack lead to significantly greater consistency for the lower levels of you infraestructure. Thsi enables you to scale infrastructure operations to manage many machines with a single small, focused team.

### Abstracting Your Infrastructure

The move to application-oriented container APIs like Kubernetes has two concrete benefits. Firts, as we described previously, it separates developers from specific machines. This makes the machine-oriented IT role easier, since machines can simple be added in aggregate to scale the cluster, and in the context of the cloud it also enables a high degree of portability since developers are consuming a higher-level API that is implemented in terms of the specific cloud infrastructure APIs.

When your developers build their applications in terms of container images and deploy them in terms of portable Kubernetes APIs, tranferring your application between environments, or even running in hybrid enviroments, is simply a matter of sending the declarative config to a new cluster. Kubernetes has a number of plug-ins that can abstract you from a particular cloud.

### Efficiency

In addtion to the developer and IT management benefits that containers and Kubernetes provide, there is also a concrete economic benefit to the abstraction.

Efficiency can be mesured bu the ratio of the useful work perfomed by a machine or process to the total amount of energy spent doing so.

A further increase in efficiency comes from the fact that a developer's test environment can be quickly and cheaply created as a se of containers running in a personal view of shared Kubernetes cluster(usign a feture called namespaces). 