This application uses [reactive programming](https://spring.io/reactive), which you may recognize from the telltale `Flux<T>`, `Mono<T>` and `Publisher<T>` types strewn about the codebase. Reactive programming requires the [the Reactive Streams](http://www.reactive-streams.org) specification. From the website: "Reactive Streams project is an initiative to provide a standard for asynchronous stream processing with non-blocking backpressure."

The [Reactor Project](https://projectreactor.io/) builds upon the Reactive Streams specification. It provides two specializations, `Flux<T>` (a container type for `0..N` values of type `T`) and `Mono<T>` (a container type for at-most one value). Types from `org.reactivestreams.*` are the Reactive Streams specification. In the Reactive Streams specification, a reactive stream `Publisher<T>` publishes data asynchronously. A `Subscriber<T>` consumes data from a `Publisher<T>`. A `Subscriber<T>` may request more data, or cancel the data altogether, using the `Subscriber<T>`. The `Subscriber<T>` regulates the flow of data; it supports flow control. Flow control is sometimes interchangeably referred to as _backpressure_.

The Reactive Streams `Publisher<T>` are a sort of inverted `Collection<T>`. Instead of pulling data out of the collection when you want it, the data is _pushed_ to you when the data is ready. The inverted approach supports better **scalability**; it means that [Spring Webflux](https://docs.spring.io/spring-framework/docs/current/reference/html/web-reactive.html), the reactive web framework that we're using, does not need to wait for an asynchronous value, or a stream of values, to resolve. The runtime can carry on doing other work while results arrive. No thread is ever parked - _idle_ - waiting for data to arrive, which means the runtime can repurpose those threads to handle other work, resulting in better scalability. In the cloud, scalability means less hardware being used to do the same job, translating into reduced data center spend. Scalability is a _Good Thing_. 

<!-- Reactive Programming gives ease of composition. and robustness -->

Reactive programming simplifies the work of **composition and integration**. All reactive Spring APIs use these Reactive Streams and Reactor types. Various projects (Spring Webflux, Spring Integration, Spring Security, Spring Data, Spring Cloud, Spring Boot, Spring Framework, and others we've surely forgotten) all have reactive programming support.  You can interoperate with other projects like RxJava, Akka Streams, Vert.x, or any other library that produces and consumes `Publisher<T>'s. It is possible to adapt `CompletableFuture<T>`, `Thread`, `Collection<T>`, arrays, `Iterable<T>`, and other types to Reactive Streams types, simplifying their composition. 

Things fail on the network. Statistically, the larger your system's surface area, the more likely some part of it will eventually fail. Reactive programming acknowledges that reality and strives to improve the *robustness* of our code, providing operators to support retries, timeouts, error handling, and more.

## RSocket 

While we love HTTP, broadly, and the REST constraint on HTTP, specifically, as much as the next cloud-native, it's not the only game in town when it comes to high speed, low-latency, highly scalable, interservice communication. There are many alternatives like GraphQL, GRPC, and - our perennial favorite - RSocket. RSocket is a binary protocol that reifies the concepts of the Reactive Streams in the wire protocol. RSocket understands supports critical components of reactive programming, including _backpressure_, and has ways to communicate that information on the wire itself. The protocol is, of course, platform, language, and payload agnostic. It follows that there is a fantastic Java client written on top of Project Reactor that we could use independent of Spring if we were so inclined. But, as luck would have it, Spring already integrates RSocket and provides a component model that makes trivial the work of standing up an RSocket based service. 