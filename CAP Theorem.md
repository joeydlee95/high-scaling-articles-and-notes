# CAP Theorem Summary
## When to use?
* Strong desire to scale system when addition resources are needed (compute, storage, etc) to compute workloads in a REASONABLE TIMEFRAME.

## What is it?
CAP Theorem - in a distributed system (collection of interconnected nodes that share data), you can only have 2 of the following 3 guarantees across a write/read pair: Consistency, Availability, and Partition Tolerance.

Consistency - A read is guaranteed to return the most recent write for a given client.
Availability - A non-failing node will return a reasonable response within a reasonable amount of time.
Partition Tolerance - The system will continue to function when network partition occurs. 

Mandatory to use Partition Tolerance because of a fallacy of distributed computing (networks are reliable), networks are not reliable. Networks go down frequently and unexpectedly. Network failures happen to your system and you don't get to choose when they occur. 

* Given that networks aren't completely reliable, you must tolerate partitions in a distributed system, you can choose when a partition occurs.

## Software Trade-off
* Consistency/Partition Tolerance
- Wait for response from a partitioned node which could result in a timeout error
- System can choose what to do in a timeout error
- Choose this when your business requirement dictates atomic reads and writes

* Availability/Partition Tolerance
- Returns the most recent version of data you have, which could be stale. Accepts writes that will be processed later.
- Choose this when your business requirements allow for some flexibility around when the data in the system synchronizes.
- Availability is also an option when system needs to continue to function in spite of external error (shopping carts, etc)

### [Robert Greiner Resource](http://robertgreiner.com/2014/08/cap-theorem-revisited/)