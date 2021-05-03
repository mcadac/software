# Resilience:

  How much money will we earn with it?
  Resilience is not about making money
  Resilience is about not losing money

  Lack of resilient software design 
    -> Reduce system availability
      -> Users cannot do what the intend to do
        -> Less transactions per time period 
          -> Immediate lost revenue
        -> Users get annoyed 
          -> Churn rate increases -> Delayed lost revenue 
        -> These are your resilience budget 



  Using resilience patterns
    -> Patterns are options not obligation
    -> Don't pick too many patterns
      -> Each pattern increase complexity (we need to balance that)
    -> Complexity is the enemy of robustness



## Retry Pattern:
  So what about the Retry pattern?

  Basically, the retry pattern is primarily used to handle the stability aspect of the system and .transitive faults.

  Transitive faults are errors that occur due to some temporary conditions such as network connection issues, temporary unavailability of a service, timeout of service, or infrastructure-levels faults.

  It improves the system's stability by enabling a service consumer to handled anticipated, temporary failures of the service by retrying to invoke the same service operation that has previously failed, keeping in mind how many retries attempts are made, and the length of time to wait in bettwen attempts.


  There are some considerations we should keep in mind when using the retry pattern:

  The application should retry only when there is clear indication that the fault in transient. if the indication is toward a non-transient fault, for example an authentication failure caused by invalid user credentials or a bad request send to service, such as HTTP status code 4xx recived from the service, the application should not try to retry, but abort the operation invocation and report a suitable exception.
  If the sepecific fault is unusual or rare, it may have been lo by extraordinary circumstances, sush as a network packet lost in transint. In this case, the application could immediatly retry the same request because the same failure is unlikely to happen again and the request will probably be successful.
  If the fault is caused by issues such as service being not fully responsive (e.g service busy), the service consumer should wait for a suitable time before retrying the request.

  Common retry interval types:
  Regular intervals: The software system waits the same amount of time in between each interval attempt.
  Incremental intervals: the system waits a short amount of time before the first retry, and the incrementally increases the amount of time before each subsequent retry. For example, retry attempts may occur at 2 seconds, 6 seconds, 12 seconds, and so on.
  Exponential backoff: The software system waits a short amount of time before the first retry, and then exponentially increases the amount of time before each subsequent retry.
  Immediate retry: A retry can take place immediately. However, there should not be multiple immediate retry attempts. If a single immediate retry attempt fails, then any subsequent attempts should use one of the other interval types.
  Randomization:  Any of the aforementioned interval types can be used in conjunction with randomization to prevent retry attempts from being sent at the same time from multiple instances of a client.


