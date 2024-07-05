# Advanced_algorithms_IITM
Notes from Advanced Algorithms Classes at IITM

# Week 1
## L 1.1 : Storing Files on Tape I

### Problem 1: We want to store files on a linear magnetic tape. We are given the lengths of files on tape.

Cost of reading a kth file is = Cost of reading the files before it + Fk

So cost of accessing all files = F1 + F1 + F2 + F1 + F2 + F3 ..... F(n-1) + F(n)

### So how to do we optimize that?
We can sort the files in this case by ascending order and access the files.

But we also need to establish with a proof that this is indeed correct.
### Proof

Lemma. Expected cost is minimized when Lpi(i+1) >= Lpi(i). Here pi denotes the index of the file.
Suppose there is a optimal solution where Lpi(i+1) < Lpi(i).
Here Estimated cost = Lpi(i+1) + Lpi(i+1) + Lpi(i) > Lpi(i) + Lpi(i) + Lpi(i+1). As Lpi(i+1) > Lpi(i).

Hence what we supposed turns out to be false and there is another optimal ordering. Hence we can accept the Lemma and reject the contradictory assumption.

## L 1.2 : Storing Files on Tape II
### Problem 2: Suppose now the frequency of access is also given
Lecture discusses sort by frequency of access and then shows an example where that will fail.

Also, here the sort by size will also fail.

Another approach discussed is using a function g(f,l) = l - f
So for a file with length 5 and frequency 2 the g(f,l) = 3, which is the rank.

But this method also has its problems in terms of being optimal solution.

Optimal approach is sort ascending by length/frequency ratio. 

1. So longer files will be higher in rank and shorter will be in front.
2. and lower frequency will lead to higher rank and higher will lead to lower rank.

Lemma: Total cost pi(i) is minimized when lpi(i)/fpi(i) <= lpi(i+1)/fpi(i+1)

## L 1.3 : Scheduling Class I

### Problem: Schedule classes such that max classes can be attended

Three approaches - 
1. shortest Class first - As the shortest class may be in between two non-overlapping long classes and we then can only attend one  _-_
2. Class with the fewest overlaps should be chosen - In this case, we will also pick the sub-optimal classes.
3. Class which starts first - Wrong approach that one class may overlap all.

## L 1.4 : Scheduling Class II
### Problem : Same as above

1. Pick the class that finishes the earliest and if it does not have any conflict with previous class - Optimal Solution
   Algo -
   Sort classes by finish time and pick the first class.
   Pick the second class if its start time is after or same as the finish time of previous class.

Lemma: At least one optimal conflict-free collection of classes includes the one that finishes first.

## L 1.5 : Stable Mathchings I
### Problem : Two groups of agents want to get matched. Each agent has a rank of the match options that are available.
Unstable pair or blocking pair: When a pair of agents from side A and side B both prefer each other over the currently assigned partners.

Goal: Find a matching that minimized the number of blocking pairs. It is also called Stable Matching.

Some approaches - 
1. Match A1-B1  and A2-B2 and A3-B3. Then just keep resolving blocking pairs. Problem is that this can become never ending.

## L 1.6 : Stable Mathchings II
### Problem : Same as above

1. Another greedy approach (that works)
   Men propose in rank order and women engage with the best offer.

   If M1 proposed W1 and W1 accepts it then M1 and W1 get engaged.
   But in this case some women will not engaged in the first round of proposals. and some men will not get their first preference.

   Then we consider in the next round the second options.

   Women who get a second offer and the current offer ranks lower they will switch to this new offer. That will make the men who they were matched with before vacant.
   In case women do not choose the new proposal then there will be a blocking pair at the end.

   Example:
   q : C > B > A
   r : A > C > B
   s : A > B > C

   A : q > s > r
   B : q > r > s
   C : s > r > q

   R1 start = q - C; r - A; s - A
   R1 end = q - C; r - X; s - A

   R2 start = q - C; r - C; s - A
   R2 end = q - X; r - C; s - A

   R3 start = q - B; r - C; s - A
   R3 end = q - B; r - C; s - A

## L 1.7 : Stable Mathchings III
### Proof: Correctness of Algorithm

