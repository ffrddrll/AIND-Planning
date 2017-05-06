# Implement a Planning Search

In this project, I ran 5 uninformed searches and 2 heuristic searches for 3 Air Cargo problems.<br>
I suggest using **A\* search** with admissible heuristics to solve simliar problems.

## Optimal Plan

- Problem 1
  ```
  Load(C1, P1, SFO)
  Load(C2, P2, JFK)
  Fly(P2, JFK, SFO)
  Unload(C2, P2, SFO)
  Fly(P1, SFO, JFK)
  Unload(C1, P1, JFK)
  ```
- Problem 2
  ```
  Load(C1, P1, SFO)
  Load(C2, P2, JFK)
  Load(C3, P3, ATL)
  Fly(P1, SFO, JFK)
  Fly(P2, JFK, SFO)
  Fly(P3, ATL, SFO)
  Unload(C3, P3, SFO)
  Unload(C2, P2, SFO)
  Unload(C1, P1, JFK)
  ```
- Problem 3
  ```
  Load(C1, P1, SFO)
  Load(C2, P2, JFK)
  Fly(P1, SFO, ATL)
  Load(C3, P1, ATL)
  Fly(P2, JFK, ORD)
  Load(C4, P2, ORD)
  Fly(P2, ORD, SFO)
  Fly(P1, ATL, JFK)
  Unload(C4, P2, SFO)
  Unload(C3, P1, JFK)
  Unload(C2, P2, SFO)
  Unload(C1, P1, JFK)
  ```

## Metrics

#### Non-heuristic planning searches
| Problem | Search | Node Expansions | Goal Tests | New Nodes | Time (ms) | Plan Cost |
| ------- | ------ | --------------: | ---------: | --------: | --------: | :-------: |
| 1 | breadth-first graph | 43 | 56 | 180 | 54 | *6* |
| 1 | breadth-first tree | 1458 | 1459 | 5960 | 1762 | *6* |
| 1 | depth-first graph | 21 | 22 | 84 | 28 | 20 |
| 1 | depth limited | 101 | 271 | 414 | 154 | 50 |
| 1 | uniform cost | 55 | 57 | 224 | 70 | *6* |
| 2 | breadth-first graph | 3343 | 4609 | 30509 | 20168 | *9* |
| 2 | breadth-first tree | - | - | - | > 1800000 | - |
| 2 | depth-first graph | 624 | 625 | 5602 | 4622 | 619 |
| 2 | dpeth limited | 222719 | 2053741 | 2054119 | 1430317 | 50 |
| 2 | uniform cost | 4852 | 4854 | 44030 | 55043 | *9* |
| 3 | breadth-first graph | 14663 | 18098 | 129631 | 141319 | *12* |
| 3 | breadth-first tree | - | - | - | > 1800000 | - |
| 3 | depth-first graph | 408 | 409 | 3364 | 2743 | 392 |
| 3 | depth limited | - | - | - | > 1800000 | - |
| 3 | uniform cost | 18235 | 18237 | 159716 | 462659 | *12* |

#### A\* search with heuristics
| Problem | Heuristic | Node Expansions | Goal Tests | New Nodes | Time (ms) | Plan Cost |
| ------- | --------- | --------------: | ---------: | --------: | --------: | :-------: |
| 1 | ignore precondition | 41 | 43 | 170 | 55 | *6* |
| 1 | level-sum | 11 | 13 | 50 | 2140 | *6* |
| 2 | ignore precondition | 1506 | 1508 | 13820 | 16330 | *9* |
| 2 | level-sum | 86 | 88 | 841 | 220106 | *9* |
| 3 | ignore precondition | 5118 | 5120 | 45650 | 101154 | *12* |
| 3 | level-sum | 403 | 405 | 3798 | 1411304 | *12* |

## Comparison

To measure the performance of planning searches, following four aspects should be taken into consideration:

- **Completeness**

  From AIMA book, I learned both **breadth-first search** and **uniformed cost search** are complete.
  The completeness of **depth-first search** or **depth limited search** can't be guaranteed.
  The **A\* search** is also comoplete.

  For the Air Cargo problems, if the planning search takes longer than 30 minutes, I would classify it as *timed out* i.e. can't be terminated.
  This kind of search is incomplete.

- **Optimality**

  A plan is called optimal if it has lowest cost among all plans.

  The textbook showed the **breadth-first search** and **uniformed cost search** is optimal.
  And the **A\* graph search** is optimal if the heuristic is admissible or consistent.

  In real world, fly likely cost much more than load or unload.
  But in Air Cargo problem, the cost of each kind of action was not specified.
  I assume every action has equal cost.
  Therefore, the cost of plan is the number of actions in it.

  The optimal cost of Air Cargo problems can be estimated by summed up the minimal number of action required seperately.
  The cargos must be loaded onto and unloaded from planes, thus the optimal cost are at least two times the number of cargos.
  The optimal number of fly actions depends on where each cargo is from and to.
  The problem 1 asked to swap two cargos at two airport, so the minimal fly cost is 2.
  Similarly, the minimal fly cost for problem 2 is 3.
  For problem 3, it is 4.
  Hence the lowest number of action needed for each problem are 6, 9, 12.

- **Time complexity**

  In theory, the worst case running time bound are:

  - **bread-first search** and **uniformed cost search** (when all action costs are equal): *O(b<sup>d+1</sup>)*
  - **depth-first search**: *O(b<sup>m</sup>)*
  - **depth limited search**: *O(b<sup>l</sup>)*

  where *b* is the branching factor;
  *d* is the depth of the shallowest solution;
  *m* is the maximum depth of the search space;
  *l* is the depth limit.

  The time complexity of **A\* search** depends on the heuristic.
  In worst case, it would be *O(b<sup>d</sup>)*.
  But a good heuristic can cut down the branching factor effectively.

- **Space complexity**

  The memory usage of all searches are:

  - **bread-first search**, **uniformed cost search** (when all action costs are equal), and **A\* search**: *O(b<sup>d+1</sup>)*
  - **depth-first search**: *O(bm)*
  - **depth limited search**: *O(bl)*

### Uninformed planning searches

- Complete: all but **breadth-first tree search** (failed at problem 2 and 3) and **depth limited search** (failed at problem 3)

- Optimal: only **breadth-first search** and **uniformed cost search**

- Time elapsed: **depth-first graph search** < **breadth-first graph search** < **uniformed cost search** < **depth limited search** < **breadth-first tree search**

- Space used: **depth-first graph search** < **breadth-first graph search** < **uniformed cost search** < **depth limited search** < **breadth-first tree search**

Among 5 uninformed searches, **depth-first graph search** used least time and space, but it failed to produce optimal plan.

The **breadth-first graph search** give me optimal plans, while it used much more time & space than **depth-first graph search**.<br>
For problem 1, **breadth-first graph search** cost double time & space.
And it need over quadruple time & 5 times space to complete problem 2.
For problem 3, time usage raised to 50 times over, and space usage increased above 35 times.<br>
It seems that the **depth first grapth search** goind down a long way but reach the goal state quickly.
That means it did not branch too many times.
The **breadth-first graph search** has a advantage of the shorter solution depth.
But it is not a real benefit because the time and space usage increased exponentially for each addtional level.
However, the **breadth-first graph serarch** still ranked in second place for both time performance and space performance.

When all actions have same cost, the **uniformed cost search** is identical to **breadth-first search**.<br>
The metrics showed the **uniformed cost search** is optimal.
But it used much more resources than **breadth-first graph search**.<br>
How could it be? I read the source code and found some differences between the implementation of two search algorithm.
The **breadth-first graph search** use a stack as the data container for frontier, while **uniformed cost search** use a priority queue.
The insertion of priority queue(implemented using `bisect.insort`) take *O(log n)* time.
It is a huge difference compare to the *O(1)* time in stack.
The priority queue also store more information than the stack in implementation.
And the **uniformed cost search** performed additional condition check when expand the child.

At the bottom of the rank are **depth limited search** & **breadth-first tree search**.<br>
I think **breadth-first tree search** may lost the direction in the state space of Air Cargo problems.
Because **tree search** can't avoid repeated action sequence.
The **depth limited search** was implemented to increase the dpeth limit recursively.
It reached the maximum depth limit (50) in both problem 1 & 2.
For the more complex problem 3, it seems not reach the depth limit yet.<br>
Another observation: although **breadth-first tree search** give an optimal plan for problem 1, its performance is at least 10 times worse than **depth limited search**.

### A\* search with heuristics

- Complete: both heuristics

- Optimal: all plans are optimal

- Time elapsed: **ignore precondition** < **level-sum**

- Space used: **level-sum** < **ignore precondition**

The difference between two heuristics is the trade-off between time and space.<br>
I found the **ignore precondition** is good on time efficiency.
Its performance is even better than the **breadth-first graph search**.
The **level-sum** heuristics, on the other hand, used much more time but only a small amount of memory.
This heuristic is slightly better than the **depth-first graph search** on space usage.
But you need to be patient for waiting the result.

Both heuristics derive the Air Cargo problem to relaxed problem.
The **ignore precondition** heuristic relaxed the problem (reference: AIMA book section 4.2) by remove some restrictions.
And the **level-sum** heuristic (reference: AIMA book section 11.4) use the planning graph, which can be treated as a relaxed problem, for computing accurate heuristic.

The difference between two heuristics is caused by how the heuristic was generated.
The **level-sum** heuristic creates a new planning graph and go through every state levels to estimate the cost.
However, the computation of **ignore precondition** heuristic just need to compare the goal and current state.

### Best planning search method

My pick is the **A\* search** with **ignore precondition** heuristic.
This search method is complete and optimal.
It also reaches a great balance between time and space.
And the performance tops all optimal non-heuristic searches.
I saw how an admissible heuristic can help reduce the branching factor of a problem in this project.

But if there is memory space restriction on the problem I want to solve, I will consider using the **level-sum** heuristic.
So the **A\* search** can take the advantage of the planning graph with more accurate estimation.
