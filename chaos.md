# Chaos Engineer

- **Top 5 Chaos Engineering myths debunked:** https://www.linkedin.com/pulse/top-5-chaos-engineering-myths-debunked-mikolaj-pawlikowski/?trackingId=lRB3LIdHvCpyQrCOyoiw9Q%3D%3D


# Netflix

Netflix’s Simian Army

Netflix distributes movies and television shows via both DVD and streaming video. Its streaming video service has been extremely successful. In fact, in 2018, Netflix’s streaming video accounted for 15 percent of the global Internet traffic. Naturally, high availability is important to Netflix.

Netflix hosts its computer services in the Amazon EC2 cloud, and the company utilizes a set of services that were originally called the “Simian Army” as a portion of its testing process. Netflix began with a Chaos Monkey, which randomly killed processes in the running system. This allows the monitoring of the effect of failed processes and gives the ability to ensure that the system will not fail or suffer serious degradation as a result of a process failure.

The Chaos Monkey acquired some friends to assist in the testing. The Netflix Simian Army included these, in addition to the Chaos Monkey:

• The Latency Monkey induced artificial delays in network communication to simulate service degradation and measured whether upstream services responded appropriately.

• The Conformity Monkey identified instances that did not adhere to best practices and shut them down. For example, if an instance did not belong to an auto-scaling group, it would not appropriately scale when demand went up.

• The Doctor Monkey tapped into health checks that ran on each instance as well as monitoring other external signs of health (e.g., CPU load) to detect unhealthy instances.

• The Janitor Monkey ensured that the Netflix cloud environment was running free of clutter and waste. It searched for unused resources and disposed of them.

• The Security Monkey was an extension of Conformity Monkey. It found security violations or vulnerabilities, such as improperly configured security groups, and terminated the offending instances. It also ensured that all SSL and digital rights management (DRM) certificates were valid and not coming up for renewal.

• The 10-18 Monkey (localization-internationalization) detected configuration and runtime problems in instances serving customers in multiple geographic regions, using different languages and character sets. The name 10-18 comes from L10n-i18n, a sort of shorthand for the words “localization” and “internationalization.”

Some members of the Simian Army used fault injection to place faults into the running system in a controlled and monitored fashion. Other members monitored various specialized aspects of the system and its environment. Both of these techniques have broader applicability than just for Netflix.

Given that not all faults are equal in terms of severity, more emphasis should be placed on finding the most severe faults than on finding other faults. The Simian Army reflected a determination by Netflix that the targeted faults were the most serious in terms of their impacts.

Netflix’s strategy illustrates that some systems are too complex and adaptive to be tested fully, because some of their behaviors are emergent. One aspect of testing in that arena is logging of operational data produced by the system, so that when failures occur, the logged data can be analyzed in the lab to try to reproduce the faults.

—LB




## Reference:

- https://medium.com/@adhorn/chaos-engineering-ab0cc9fbd12a
