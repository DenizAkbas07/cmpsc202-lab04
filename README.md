# Lab 4: Concept Review

This lab reviews the foundational concepts of algorithms and data structures that we have covered in the first half of the course. 

**Instructions:** To complete this lab, you may work in groups, but you must write your solutions yourself. Choose two of the topics below that you need to review and complete the corresponding problems. Where relevant, you are given the answer and must provide the justification as your solution. Once you have completed the lab, push your changes to your forked repository.

**Topics:** asymptotic analysis, data structures, empirical comparison of algorithms, pseudocode, greedy algorithms. 

## Asymptotic Analysis

1. Use the rules from lecture 07 to prove that $T(n) = 5 \log n + 7n$ is $\mathcal{O}(n)$.
Answer:
T_1= (5/logn)
T_2= (7n)
T=T_1+T_2
T_1= (1/logn) drop the constants
T_2= (n) drop the constants
Summing is a max -> T=max{n, 1/logn} =n
so $T(n) is $\mathcal{O}(n)$.

2. True/False/Possibly: $T(n)$ is $\mathcal{O}(n^2)$?

**Answer**: Yes

**Justification**: We know that the quadratic time grow faster than linear time and therefore it is a upper-bound for it. We know that as linear time gets larger and larger it has to be capped by the quadratic time as in growth rate. Therefore quadratic time is an upper bound to linear time. 

3. True/False/Possibly: $T(n)$ is $\Omega(n \log n)$?

**Answer**: No

**Justification**: Statement is that log linear time is slower than linear time. Which we know is not true because loglinear time has a faster growth rate than linear time therefore can not be a lower-bound to it, instead it will be a upperbound. We know this because we are multiplying logn with n which is certainly going to have a higher growth rate than n on its own. 

4. For any algorithm, we can give a trivial lower bound. What is that lower bound?

**Answer**: $\Omega(1)$

**Justification**: For any algorithm to run it at least has to be have 1 step in it to perform an action. Therefore that makes it that any algorithm can not run faster, (have a slower growth rate) than constant time. So for every possible cas constant time makes sure that it is a lower bound to its growth rate. 

5. Is there a corresponding trivial upper bound? Why or why not?

**Answer**: No

**Justification**: Because the algorithms can become huge regarding its executions or steps so there can not be a trivial single time for an algorith is headed for infinity. We can give a time that is an upper bound to a lot of different algorithms but there is certainly one algorithm that can have a higher growth rate than that. 


## Data Structures

1. You are programming a robot to navigate a maze. As the robot moves forward, it records each intersection it passes. When it hits a dead end, it needs to retreat to the most recently visited intersection to try a different path.

**Answer**: Stack

**Justification**:

2. A server receives a massive influx of data packets from a streaming video application. To prevent the video from skipping or playing out of order on the user's end, the server must process and forward these packets in the exact sequence they were received.

**Answer**: Queue

**Justification**:

3. An atmospheric monitoring system reads temperature data from 10,000 sequentially numbered sensors (IDs 0 through 9999). Throughout the day, the system needs to constantly update and read the current temperature of randomly selected sensors based on their ID number to build localized weather maps.

**Answer**: Array

**Justification**:

4. You are building a lightweight syntax checker for a code editor. Its sole job is to scan a document and ensure that every opened parenthesis `(`, bracket `[`, and brace `{` is matched with its corresponding closing character in the correct nested order.

**Answer**: Stack

**Justification**:

## Empirical Comparison of Algorithms

1. A student is benchmarking an algorithm that takes a list as its input. They run it on progressively larger randomly generated lists, doubling the number of elements ($n$) and record the following execution times:

- $n = 1000$: 0.12 seconds
- $n = 2000$: 0.94 seconds
- $n = 4000$: 7.61 seconds
- $n = 8000$: 60.85 seconds

 Based on this empirical data, what is the most likely asymptotic time complexity of the algorithm? **Hint**: Calculate the doubling ratio between each pair of consecutive runs.

 **Answer**: Cubic time complexity, $\mathcal{O}(n^3)$

**Justification**:Growth rate analysis: When doubling the input size (from n to 2n), the execution time consistently increases by a factor of approximately 8. For polynomial time complexity O(n^k), doubling the input increases execution time by 2^k. Because 2^3 = 8, an 8-fold increase corresponds to a cubic exponent (k = 3).

 2. Two students write separate algorithms to compute a metric over an array of 10 million integers. Both algorithms perform exactly one mathematical operation per element, meaning both have a theoretical time complexity of $O(N)$. However, during benchmarking, Algorithm A consistently runs 15x faster than Algorithm B. Why might theoretical Big-O analysis fail to predict this massive performance gap? 

**Answer**: This can be caused by the overlook of the hardware students were using. Algorithm A might have been faster because of a faster and stronger cpu or memory. Also Big-O is only an upperbound so that means that these two students can have the same Big-O but have different times exactly. Because both of the algorithms still fall below the Big-O of (N).

 3. Scenario: To measure the running time of algorithms for an empirical comparison, a developer writes the following benchmarking script:

```python
import time

large_array = [i for i in range(1000000)]
start = time.time()
myAlg(large_array)
end = time.time()

print("Time:", end - start)
```

They run this script exactly once for each algorithm on their laptop while streaming a movie in the background. Identify at least three distinct methodological flaws in this benchmarking setup that make the results unreliable.

**Answer**:
1. Only doing one single trial. It is healthier to do multiple trials can avarage out the results to get a more reliable and healthy data. 
2. Single Data Size. The developer is only testing it in the range of 1000000, the developer can try different inputs and see the results and then again, try to come with an avarage. 
3. Using the CPU on the background. Streaming a movie puts a load on the cpu and this can make it less stable for the running algorithm and can give us not certainly reliable answers on the timing of the trials. 
4. Low-Precision Timer (time.time()): time.time() measures system wall-clock time and is subject to clock drift and lower measurement. High-precision benchmarking in Python should use time.perf_counter() instead.

## Pseudocode

1. Analyze the exact number of times the `do_work()` function is called in the following pseudocode, assuming $N \ge 1$.

```
count = 0
for i = 1 to N do
    for j = i to N do
        do_work()
```

Write a closed-form expression for the number of times `do_work()` is called in terms of $N$.

2. Analyze the exact number of times the `do_work()` function is called in the following pseudocode, assuming $N \ge 1$.

```
i = N
while i > 0:
    for j = 1 to i:
        do_work()
    i = floor(i / 2)
```

If $N=16$, how many times is `do_work()` called?

**Answer**: 31

**Justification**:

## Greedy Algorithms

You are organizing a film festival but only have access to a single screen. You are given a list of $n$ films, each with a specific `start_time` and `end_time`. You want to screen the maximum number of films possible.

Consider the following three greedy strategies:

- **Shortest First**: Always pick the film with the shortest duration (that doesn't conflict with already chosen films).
- **Earliest Start**: Always pick the film that starts the earliest (that doesn't conflict).
- **Earliest Finish**: Always pick the film that finishes the earliest (that doesn't conflict).

Which of these three strategies guarantees an optimal solution (maximum number of films)? For the two strategies that fail, provide a counter-example (a small set of film times) where the greedy choice results in a sub-optimal schedule.

**Answer**: The earliest finish strategy guarantees an optimal solution.

**Justification**: