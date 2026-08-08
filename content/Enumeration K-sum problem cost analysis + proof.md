Prelude
---
During our discussions in the class Discord server, Professor Halim decided to ask us to think whether it is possible to have $$o(n^2)$$ solutions to the [3-Sum problem](https://leetcode.com/problems/3sum/solutions/), and I proved it impossible while taking a bus ride to the campus.
A day later, someone proposed the 'meet-in-middle' idea, claiming to have solved the 4-Sum problem in $$O(n^2logn)$$, and I was like "That's bullsh__, I proved the problem was $$\Omega(n^3)$$ didn't I?"
...Then they pulled out a bunch of research papers detailing the solutions.

What does this mean?
---
So, for context, K-Sum problems have two variants, the 'decision' version and the 'enumeration' problem.
The 'decision variant' simply requires the program to tell whether or not **there exists** a subset of k elements where they sum up to the target. For example, if K=2, target=100 & array =[1,2,3,...,100], you simply need to find a pair that summed to 100 and be over with. TwoSum in LeetCode is functionally the 'decision variant'.
The 'enumeration variant' requires that the program return **all configurations** that satisfy the requirements. Using the same example as above, the program would have to return all 49 pairs that fulfill the requirements. 3Sum, 4Sum in LeetCode are enumeration K-sum problems.

Now looking back, I really dodged a bullet with the $$o(n^2)$$ question X)
As in, there's literally something named "3Sum conjecture" where mathematicians are still looking for algorithms that solve 3Sum in $$O(n^{2-O(1)})$$ time. Best we can do is like, $$O(n^2/(logn)^c)$$ or whatever. (I mean, that's still $$o(n^2)$$, but that's kinda not all that good X))
Like, chill prof, we're not even into the semester and you're already throwing unsolved problems at us XD

Anyhow, I only managed to solve the problem because LeetCode happened to use the 'enumeration variant'. But, I was still 100% correct in my proof (That enumeration K-Sum problems are $$Omega(n^{K-1})$$.

So, let's see that proof now!

The Proof
---
...Wait! I'm not ready yet!

Um, it's just, quite difficult to pinpoint a worst case scenario for this kind of problem, So, uh, why don't we start from something, um... simpler?

Not The Proof %%THE LEMMA%%
---
Let's consider a different variant of the problem. Target is a positive integer, and all elements in the array are positive integers too. We still need to return a list of all unique combinations that would make the desired sum. What can we say about the new problem?

[Author left for dinner. To be continued...]