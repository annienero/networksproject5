# High Level Approach

We began by reading the RAFT paper and understanding it at a high level. Then as we implemented each piece, we would read that portion of the paper more in depth to help us with the details of implementation.

We started with the leader election implementation, then moved to get/put request implementation, then to crash resilience, then implementing consistent logs+committing, then partition resilience, then fine tuning performance.

We have a main loop that handles messages and delegates to various helper functions. State is kept in global variables.

# Challenges

Our main challenges were in debugging and fine-tuning our implementation, and reasoning about what was going on in the network with only print statements to go off of. Because it was a complex system, it was often tough to reason out the underlying causes of errors when we did find them.

In particular we struggle with determining the causes of unanswered put/get requests.
They happen non-deterministically and we've had a lot of trouble figuring out exactly what causes them.
We identified certain ways to make them better, but we still have runs where we'll have an unusually high number of them.
We also struggled with identifying the causes of incorrect responses to gets.

# Testing

We tested our code with print statements that logged a bunch of what was happening, and then we read through the output.We used the run.py and test.py scripts to test.
