# Week 2
## L2.1: A Generic Optimization Problem
### Matroids

We can establish that our problem has a Matroid structure and the problem's solution proof can be outsourced to Matroids.

Problem: U is a universe of elements e1 ... en
Each element has a weight wt: U -> Q>=0. Weight function from Universe to weights >= 0.
Family of set of universes F = {S1, S2, ..... Sm}; Si c= U. Where Si is a subset of U

weight of each set is Sum of weights of each element in the set

Goal: Find max weight set in F.

Example - 
Universe - is vertices of G
Family could be - 
1. paths in G. Every subset is a collection of vertices such that they all are connected. or
2. Independent sets in G. Every subset is a collection of vertices such that they are all disconnected.

Family is generally not given but just specified. Universe is given.
Or a subset will be given and we have to tell whether it belongs to a family or not.

It's called "Oracle Access" is given to a set and we tell whether that set belongs a particular family.
