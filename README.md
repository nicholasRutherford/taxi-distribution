# Large Scale Taxi Distribution With Simulated Annealing.

## Problem Description
The problem we focused on is to deliver a set of packages in a city. We have the following parameters:

* **N** The number of packages to be delivered
* **K** The number of vehicles used to deliver the packages
* **M** The number of nodes in our graph of the city

Each package has a source node, and destination node. Each truck can only move one package at a time, so you can think of them like taxis moving people rather than a delivery truck delivering 100s of packages at one time. Each of the trucks starts and ends at the garage node. The city is constructed as a graph with possible locations being nodes and roads between those locations being weighted edges. The goal is to delivery all of these packages in an efficient manner.

## Solution Description
The main problem can be broken down into smaller problems.

1. Finding the best path from one location to another in the city.
2. Finding the best order to deliver a set of packages that a truck is responsible for delivering.
3. Finding the best set of packages for each truck.

To find the best path from location A to location B is a problem that can easily be solved with shortest path finding algorithms. We chose to use A* for this problem as it finds the optimal path in reasonable time. Addressing problems 2 and 3 is a bit more tricky. We could through everything into one large A* search, however at each step in our search we would need to generate b^k new search nodes where b is the maximum degree of node (if you imagine a basic grid most nodes would have b=4). This would result in a ludicrous amount of nodes being generated at each step, but it would give you the optimal if it ever managed to halt.

Instead we decided to use simulated annealing. This is where you generate an end state, then find a similar but slightly different end state. Then you test whether the new state is cheaper, if it is you move to this new state and repeat the process. If the new state is more expensive you have a chance at moving to it, but the chance of you moving to a higher cost state decreases as the program runs. Simulated annealing does not run into the state explosion that A* experiences, however it is not optimal which means it will return a good result, but not necessarily the best result. Another benefit of simulated annealing is that you can get better results by allowing the program to run longer.
