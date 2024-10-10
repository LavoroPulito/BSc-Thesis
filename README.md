# :mortar_board: Bachelor's Thesis in Computer Science

[My Bachelor's Degree Thesis](src\Thesis.pdf) in Computer Science at Sapienza Università di Roma, entitled:
"Achieving Max Flow in Strongly Polynomial Time for Sparse Networks: Beyond the Edmonds-Karp Algorithm".

## Abstract
The following report is aimed at analyzing the evolution of solutions to the max-flow problem in networks. It will clearly and thoroughly demonstrate how improvements can be made upon the Edmonds-Karp algorithm.

Finding the maximum flow that can be routed through a network posed a significant challenge for decades, since the first solution was introduced by L. R. Ford Jr. and D. R. Fulkerson in 1956. Their algorithm runs in $O(mf)$ time were $f$ represents the maximum flow in the network.

Given the rapid growth and dynamic nature of connections (especially virtual ones), determining the maximum flow of a network is a crucial problem. If solved efficiently, it allows for traffic optimization within the network, minimizing both waste and slowdowns.

For example, if we consider the internet, it consists of numerous connected devices that continuously receive and forward packets to other devices. Naturally, each device has different performance capabilities and can handle varying amounts of data flow.

By identifying the maximum flow capacity, we can determine how fast information can travel from one point to another within the network. This allows us to maximize resource utilization without exceeding limits, which could otherwise cause bottlenecks.

Furthermore, since network topologies are highly dynamic, with many nodes and branches, quickly identifying the maximum routable data flow becomes crucial to ensuring the validity and efficiency of information transfer.

This thesis will focus on the $O(nm)$ solution for sparse graphs. Computational cost becomes particularly challenging when there are few edges, as the costs of other phases of the solution tend to increase.

An algorithm with $O(nm)$ complexity has existed since 1992 the King-Goldberg-Tarjan algorithm by V. King, S. Rao, and R. Tarjan (which is not covered in this thesis). However, this solution only achieves the declared complexity on relatively dense graphs. By contrast, Orlin’s 2013 solution achieves $O(nm)$ complexity specifically for sparse graphs.

In conclusion, we will show that it is possible to find the maximum flow for any type of graph. By reconstructing all intermediate algorithms, from Edmonds-Karp to the most recent ones, even a less experienced reader will be able to understand the final solution while learning all the necessary concepts.

The algorithms are presented in chronological order, starting with Dinic's algorithm, continuing with Goldberg-Rao, and culminating with Orlin’s most recent and effective solution. However, before delving into these algorithms, a chapter is dedicated to explaining some preliminary graph theory concepts that are essential for understanding how the solutions work.
