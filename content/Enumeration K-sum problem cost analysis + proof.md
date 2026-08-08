# Prelude
---
During our discussions in the class Discord server, Professor Halim decided to ask us to think whether it is possible to have $$o(n^2)$$ solutions to the [3-Sum problem](https://leetcode.com/problems/3sum/solutions/), and I proved it impossible while taking a bus ride to the campus.
A day later, someone proposed the 'meet-in-middle' idea, claiming to have solved the 4-Sum problem in $$O(n^2logn)$$, and I was like "That's bullsh__, I proved the problem was $$\Omega(n^3)$$ didn't I?"
...Then they pulled out a bunch of research papers detailing the solutions.


# What does this mean?
---
So, for context, K-Sum problems have two variants, the 'decision' version and the 'enumeration' problem.
The 'decision variant' simply requires the program to tell whether or not **there exists** a subset of k elements where they sum up to the target. For example, if K=2, target=100 & array =[1,2,3,...,100], you simply need to find a pair that summed to 100 and be over with. TwoSum in LeetCode is functionally the 'decision variant'.
The 'enumeration variant' requires that the program return **all configurations** that satisfy the requirements. Using the same example as above, the program would have to return all 49 pairs that fulfill the requirements. 3Sum, 4Sum in LeetCode are enumeration K-sum problems.

Now looking back, I really dodged a bullet with the $$o(n^2)$$ question X)
As in, there's literally something named "3Sum conjecture" where mathematicians are still looking for algorithms that solve 3Sum in $$O(n^{2-O(1)})$$ time. Best we can do is like, $$O(n^2/(logn)^c)$$ or whatever. (I mean, that's still $$o(n^2)$$, but that's kinda not all that good X))
Like, chill prof, we're not even into the semester and you're already throwing unsolved problems at us XD

Anyhow, I only managed to solve the problem because LeetCode happened to use the 'enumeration variant'. But, I was still 100% correct in my proof (That enumeration K-Sum problems are $$Omega(n^{K-1})$$.

So, let's see that proof now!


# The Proof
---
...Wait! I'm not ready yet!

Um, it's just, quite difficult to pinpoint a worst case scenario for this kind of problem, So, uh, why don't we start from something, um... simpler?

# ...Not The Proof? 
## (The lemma)
---
Let's consider a different variant of the problem. Target is a positive integer, and all elements in the array are positive integers too. We still need to return a list of all unique combinations that would make the desired K-sum (Let's say target is *t*. What can we say about the new problem?

Well, let's consider an array containing K duplicates of each integer from 1 to *t*. By definition, we need to return any combination of K positive numbers that sum up to *t*. How many would that be?

Well, [simple combinatorial theorems](https://en.wikipedia.org/wiki/Stars_and_bars_\(combinatorics\) tell us that there are $$\binom{t-1}{K-1}$$ ways to split *t* into ordered K-tuples with all-positive integer elements. Since we don't care about order within each tuple, we need to account for duplicate counting. Each tuple is counted at least once and at most K! times. Ultimately, we have $$\frac{\binom{t-1}{K-1}}{K!}\le L\le \binom{t-1}{K-1}$$, with $$L$$ denoting the length of the output list.

Notice that $$L\sim \Theta (t^{K-1})$$ and the algorithm has to find and print all L combinations. There's no avoiding this. For this specific type of cases, a length of $$K\cdot t$$ can incur a cost on the scale of $$\Theta (t^{K-1})$$, where $$t \in \mathbb{Z} \land t \ge K$$.

*(\*  You absorbed the section's proof.)*
*(\*  ...Feels useful.)*


# The proof (cont.)
---
Well, we've stalled this out for as long as we can, time to finally tackle this head on.

Notice that if every element in the array increases/decreases by *m*, and the target increases/decreases by *mK*, the answer list length should remain the same, as any pick of K elements would have K elements changing by *m* after the change.

So, for every *t* where $$K | t$$, let $$t = K\cdot p$$, the aforementioned example array from 1 to *t* can have each element decreased by *p*, and we still have a way to methodically generate input arrays of length $$K\cdot t$$ and incur a cost of $$L\sim \Theta (t^{K-1})$$.

Therefore, the enumeration K-Sum problem defintionally costs $$\Omega (n^{K-1})$$ where $$n$$ denotes the length of the input array.



# $$\mathfrak{Quod\;erat\;demonstrandum}$$
# Subscribe

![[Pasted image 20260808220532.png]]

[IDK follow me on LinkedIn I guess](https://www.linkedin.com/in/enzomeng)