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

A Greedy Approach: Consider we have a blackbox i.e. our algo which will tell us whether an S is a part of F or not.

Algo:
Sort the elements in decreasing order of weights. 
Initialize solution set = empty
While there are elements:
  If (X U curr belongs to F): # This is our black box check
    Add X to curr
  Move to next element

Example U = {W,X,Y,Z}

wt(W) = 50, wt(X) = 30, wt(Y) = 42, wt(Z) = 10

Let F = { {W}, {X,Y}, {Y,Z}, {Z} }
Weights will be 50, **72**, 52, 10 for the F members

For W Y X Z out algo should return 72. But it does not.

We check whether W is in F, yes so we add it to X.
WY is not in F so we move forward.
WX is not in F so we move forward.
WZ is not in F so we move forward.

This missed out on the other sets. Hence greedy did not work here.

Kruskal's algorithm will work here.

Let's forcefully prove that our greedy algo works.

Let Output of greedy = f1, f2, .... fk
Let weights then be = w1 >= w2 >= w3 ...

Optimal solution is g1, g2, g3 ...
Optimal weights are wg1 >= wg2 >= ...

Let f1 ... fp and g1 ... gp upto fp greedy and optimal did the same.
Let fp+1 < gp+1 i.e. it did not work similar to optimal. Why did this happen? It is because greedy ran out of elements as it was stuck with W.

We can see that the definition of Matroid will help us get out of this situation.

We will define what is a matroid and then show that if the family is a matroid then our greedy algo with work.

## L2. 2: Definition and Examples

(U,F) where U consists of elements and F is a set of subset of U
Properties of Matroid: (read carefully)

1. Non-emptiness - Empty set is always part of the Family.
2. Heridity - If X belongs to F and Y belongs to X then Y belongs to F.
3. Exchange Property - X, Y belong to F and size of X > size of Y then x = X-Y is not empty. and Y union x is also part of F.

Let F = { {W}, {X,Y}, {Y,Z}, {Z} }
Our example above violates all the three properties:
1. Violates Non-emptiness - It does not have empty set
2. Violates Heridity - X,Y belong to F and Y belong to X,Y but Y does not belong F and X does not belong to F.
3. Violates Exchange Property - {X,Y}-{Y,Z} = {X} {Y,Z} union {X} is not in F.

### Uniform matroid (k)
n = 10
U = {1,2,3...n}
F = {X | X subset U, |X|<=k}, k = 2
F = {phi, {1}, {2}, ... {12}, {13}, ... {9 10}}

1. Non-emptiness is followed
2. Heridity is followed
3. Exchange property also works

### Linear Matroid
Suppose A-> n X m matrix
U = {1,2....n}
F = {X subset U | the columns corresponding to X are linearly independent in A}

1. Non-emptiness - An empty set is always part of the Family. As it also linearly independent.
2. Heridity - If X belongs to F and Y belongs to X then Y belongs to F. As in this case, each vector is also linearly independent.
3. Exchange Property - X, Y belongs to F, and size of X > size of Y then x = X-Y is not empty. and Y union x is also part of F.

### Graphic Matroid
Suppose G = (V,E)
U = E
F = { X subset E | G[X] is acyclic }

1. Non-emptiness - An empty set is always part of the Family. As it is also acyclic.
2. Heridity - If X belongs to F and Y belongs to X then Y belongs to F. As every single edge will also be acyclic.
3. Exchange Property - X, Y belongs to F, and size of X > size of Y then x = X-Y is not empty. and Y union x is also part of F. Here if we remove some edges of Y from X and then take one of those remaining edges in X and add it to Y then also YUx will be acyclic. Detailed proof in video.

### Another example of Non-matroid
G = (V,E)
U = E
F = {X | X subset E such that X is a matching }

Self exercise

## L2. 3: Greedy Works!

Members of Family F are called independent Sets.
A maximal elements of F is called basis. That means no other set can contain that set.

All basis have the same size.
Claim If X, Y belong to F. If X & Y are basis elements i.e. they are maximal in F. Then size X == Size Y.

For sake of contradiction lets say X != Y.

Then by exchange property X-Y = x and YUx should belong to F. This is a contradiction as Y was supposed to be maximal but we found YUx which is greater than Y.
Hence X and Y must be same size.

All basis elements have same size and this size is called Rank of the Matroid.

Basis of a Maximal independent set is nothing but a Maximal Spanning Tree.

If a set is in the family then it is called independent set and if you are out then it is called dependent set.

Summary Rank and Independent are import takeaways here/

### Back to problem from L2.1

Problem: U is a universe of elements e1 ... en
Each element has a weight wt: U -> Q>=0. Weight function from Universe to weights >= 0.
Family of set of universes F = {S1, S2, ..... Sm}; Si c= U. Where Si is a subset of U

weight of each set is the Sum of the weights of each element in the set

Goal: Find max weight set in F.
Input: (U,F), wt: U-> Q>=0, oracle access to F. 
Output: max wt set in F.

Sort the elements of U in decreasing order of wt.

X -> phi

for i in 1->n:
  if (XUei belong to F):
    X <- X U {ei}
return X

We saw that our algo will not work on non-matroid structure. Like last time. But this time we will apply it on matroid family.

Assume:
Output of Greedy: f1, f2, f3 ... fk
Optimal Output : g1, g2 .... gk

Let k be size of greedy output <= rank of matroid. It cannot be more than the rank.

Size of Optimal output will be k as if it was less than that set would be subset of some other maximal set and optimal solution can always be improved.
Hence Optimal Output = k.

let's say greedy output some solution which had less than k elements. Now we can see that at some point there was an element which is part of a maximal set and must have been picked by greedy and when Oracle access was initiated it must have returned true and hence greedy will not ignore that element and in the end will end up with a maximal set of size k. This is by heredity.

Proof is by contradiction: see the video for clarity.

## L2. 4: Greedy Fails on non-Matroid Structures

Let Subset system is a finite collection of sets that satisfy heredity.

X belongs to F, Y subset X then Y belongs to F

Claim: for any subset system (U,F) that is not a matroid, then there is a wt. function such that the greedy algorithm does not return an optimal solution

Assume F is not a matroid and fails on exchange property.

For all X, Y belongs to F. If size X > size Y, then there exists x belongs to X\Y such that Y union x belongs to F.

**Negation of this:**
X,Y belongs to F such that size X > size Y but for all x belonging to X\Y, YUx does not belong to F.

## Why greedy failed in Non-overlapping classes case?
Let's say the algo was to pick the non-overlapping classes.
Take this example _-_
Consider the single class as Y and two classes as X. Here if we see size X > size Y but X-Y = x will have the two classes of X. and if we were to add any of the two classes to Y it will not be part of F. As F is a family of non-overlapping classes.

But we will say that some other greedy algo worked where we sorted the classes in decreasing order by end times. It was a special case.

If we were to add weights to the classes and if we say I want to pick non-overlapping classes and maximize weight then greedy algo may end up failing.
So in non-matroids, greedy algos could work but in special cases and special algos.

## L2. 5: Scheduling with Deadlines












