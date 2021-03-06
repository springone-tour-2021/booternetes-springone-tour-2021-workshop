> I do not like work even when someone else is doing it. ― Mark Twain

We're with Mr. Twain on this one. We loathe work, especially undifferentiated work. Work that you have to do but that doesn't directly contribute to your project's success is undifferentiated work, and getting to production today means doing more of it than ever.

When we talk about _cloud native computing_, it refers not to any single technology but more to an approach that optimizes for frequent and fast releases, and the speed of iteration. Faster organizations learn and grow faster. There are many work queues for each new production release, which must be done and take wall-clock time. Some things like integration and integration testing must happen serially, after all the contributions to the codebase settle, while other work may be done concurrently. The smaller the size of the codebase, the more quickly all the serialized work finishes. The goal is to do as much work in parallel and reduce the amount of serialized work, to reduce wall clock time between releases. Microservices, with their smaller codebases and smaller teams, reduce the wall clock time between having an idea and seeing it deployed into production.

Microservices are not without costs.

In the world of microservices, the rare work (tedium!) of addressing non-functional requirements like security, rate limiting, observability, routing, containers, virtual machines, and cloud infrastructure has become an ongoing struggle that bedevils every new microservice.

Microservices introduce a lot of the complexity implied in building any distributed system. Things will fail in production at sufficient scale. In this workshop, you're going to look at different technologies that let us pay down some of the technical complexity and technical debt of scale.
