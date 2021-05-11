# Architecture

## Event driven architecture 
Pros and Cons of Event-Driven Architecture

There are a few reasons why using an event driven architecture can be an advantage over alternative architectures.

- Loose coupling: Services do not need to be dependent on each other. This applies different factors such as transport protocol, availability (the service being online) and the data being sent. The consumer will still need to know how to interpret an event or message so a strict contract should still be used between the two services, but implementation details of the contract should not matter.

- Scalability: Since the services are no longer coupled, the throughput of service 1, no longer needs to meet the throughput of service 2. This can help reduce costs as services no longer need to be online 24/7 and it is possible to take advantage of serverless computing with infinite scaling.

- Asynchronicity: Since services are no longer dependent on a result being returned synchronously, a fire and forget model can be used, which can greatly speed up a process. This can have a downside, which will be outlined below.

- Point in time recovery: If events are backed by a queue or maintaining some kind of history, it is possible to replay events, or even go back in time and recover state.

There are drawbacks to using an event driven architecture as well.

- Over-engineering of processes: Sometimes a simple call from one service to another is enough. If a process uses event driven architecture, it usually requires much more infrastructure to support it, which will add costs (as it will need a queueing system)

- Inconsistencies: Because processes now rely on eventual consistency, it is not typical to support ACID (atomicity, consistency, isolation, durability) transactions, so handling of duplications, or out of sequence events can make service code more complicated, and harder to test and debug all situations.

## References

- Modular monolithic [https://www.youtube.com/watch?v=5OjqD-ow8GE]
- The lost of art software design [https://www.youtube.com/watch?v=qO73yObPYac]
- Evolving a Clean, Pragmatic Architecture [https://www.youtube.com/watch?v=tMHO7_RLxgQ&t=1444s]
