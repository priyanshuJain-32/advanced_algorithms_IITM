# advanced_algorithms_IITM
Notes from Advanced Algorithms Classes at IITM

# Week 1
## L 1.1 : Storing Files on Tape I
**Problem 1:** We want to store files on a linear magnetic tape. We are given the lengths of files on tape.

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

Problem 2: 
