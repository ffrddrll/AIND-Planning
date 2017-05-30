# Historical Developments in AI Planning and Search

AI planning arose from investigations into state-space search, theorem proving, and control theory and from the practical needs of robotics, scheduling, and other domains. <sup>[1]</sup>
Here is my selection of important historical developments in this field.

## Shakey

During the late 1960s and early 1970s, a group of AI researchers at the SRI AI lab developed a mobile robot known as "Shakey the Robot".
Shakey could receive and analyze the command of completing a large task, then execute a combination of basic actions in limited world. <sup>[2]</sup>
For example, Shakey was able to recognize command that push a box to a location, then find and move the box to the destination as well as bypass some obstacles on the routes.
These tasks required planning, route-finding, and the rearranging of simple objects. <sup>[3]</sup>
The project combined research in robotics, computer vision, and natural language processing.
Some most notable research results include the STRIPS planning system, A\* search algorithm, the Hough transform, and the visibility graph method. <sup>[2]</sup>
The software architecture and algorithms greatly influenced the modern robotics and AI development. <sup>[4]</sup>

STRIPS, the automatic plan generator used on Shakey, is the first major planning system.
It only can solve simple classical planning problem.
But the STRIPS language or its variants was used by almost all of following planning systems.
The Action Description Language, or ADL, relaxed some of the restrictions in the STRIPS language and made it possible to encode more realistic problems.
The Problem Domain Description Language or PDDL was introduced as a computer-parsable, standardized syntax for representing STRIPS, ADL, and other languages.
PDDL has been used as the standard language for International Planning Competition events.
<sup>[1]</sup>

## Planning Graph

Irrelevant actions and inaccurate heuristics are primary concerns when solving planning problem using standard search algorithm.
Blum and Furst introduced the GRAPHPLAN planner in STRIPS-like domains.
The algorithm begins by explicitly constructing a compact structure called Planning Graph.
By encodes constraints of the planning problem in the data structure, the branching factor can be reduced effectively.
Also, more accurate heuristics can be generated using Planning Graph.

Taking the advantages of Planning Graph, the GRAPHPLAN speed up the search greatly.
It outperformed other planners of the time, such as Prodigy or UCPOP.
The GRAPHPLAN inspired the following planner like IPP, STAN, SGP, etc.
And the Planning Graph was used in combination with other techniques (e.g. SAT, local search) since then.
<sup>[5]</sup>

## Markov Decision Processes

The environments of classical planning are fully observable, deterministic, finite, static, and discrete. <sup>[6]</sup>
Unfortunately, above assumptions do not hold in most of real world problems.
To solve planning problem under uncertainty, researchers had put lots of effort into creating variants of classical planner in the past.
But the development of decision-theoretic planning might be more influential.

Sven Koenig is the first one to make the connection between MDPs and AI planning problems.
He showed how to use Markov decision processes, or MDPs, to construct optimal plans for a simple probabilistic and decision-theoretic problem in his master's thesis.
The partial observable Markov decision processes (POMDPs) also became a tool for planning problem in the following years.
Kaelbling, et al. gave an improved POMDPs algorithm for planning and acting in partially observable stochastic domain.
Bonet and Geffner developed a conformant planner based on the idea of POMDPs.

POMDPs is closely related to reinforcement learning. <sup>[7]</sup>
Recent researches on deep reinforcement learning achieved breakthrough result. <sup>[8]</sup>
I am really exciting to see how deep learning help decision-theoretic planning move forward in the future.

## Reference

[1] Artificial Intelligence: A Modern Approach (AIMA) Second Edition, Chapter 11. p.409<br>
[2] [Shakey the robot - Wikipedia](https://en.wikipedia.org/wiki/Shakey_the_robot)<br>
[3] [Shakey the robot | SRI International](https://www.sri.com/work/timeline-innovation/timeline.php?timeline=computing-digital#!&innovation=shakey-the-robot)<br>
[4] [Shakey the Robot: The First Robot to Embody Artificial Intelligence - YouTube](https://www.youtube.com/watch?v=7bsEN8mwUB8)<br>
[5] AIMA 2/E Chapter 11. p.411<br>
[6] AIMA 2/E Chapter 11. p.375<br>
[7] [Reinforcement learning - Wikipedia](https://en.wikipedia.org/wiki/Reinforcement_learning)<br>
[8] [Deep Reinforcement Learning | DeepMind](https://deepmind.com/blog/deep-reinforcement-learning/)

Avrim Blum and Merrick Furst. [Fast Planning Through Planning Graph Analysis](https://www.cs.cmu.edu/~avrim/Papers/graphplan.pdf)<br>
Sven Koenig. [Optimal Probabilistic and Decision-Theoretic Planning using Markovian Decision Theory](http://idm-lab.org/bib/abstracts/papers/masters.pdf)<br>
Leslie Kaelbling, Michael Littman, and Anthony Cassandra. [Planning and acting in partially observable stochastic domains](http://people.csail.mit.edu/lpk/papers/aij98-pomdp.pdf)<br>
Blai Bonet and Hector Geffner. [Planning with Incomplete Information as Heuristic Search in Belief Space](https://vvvvw.aaai.org/Papers/AIPS/2000/AIPS00-006.pdf)<br>
