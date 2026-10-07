![[Pasted image 20260908101619.png]]
<span class="caption">Top 10 anime quotes before disaster</span>
# Prelude
---
Right, so remember how in [[Enumeration K-sum problem cost analysis + proof#What does this mean?|Enumeration K-sum problem cost analysis + proof]], I mentioned that there are two variants of the K-sum problem?

After we derived the asymptotically absolute optimal solution, generalized to all K, we kinda decided to move on to the decision variant of the problem.

By the way, if anyone wants to know,

> i believe there is a way to modify this such that it can suit the needs of 4sum
<small>
(This is false. We eventually managed to prove that adopting the meet-in-the-middle solution for enumeration still leads to the same worst case efficiency.)
</small>

Eventually, we did manage to draft a rough idea for how we can use the meet-in-the middle idea for the 4-Sum problem.

...It, uh... looks like this:

# Solution
---
![[Pasted image 20260908104756.png]]![[Pasted image 20260908104938.png]]
<span class = "caption">Don't worry, we'll skim over this</span>
# Analysis
#### Believe me, I hate this as much as you do
---
Okay, that was a whole lot to take in, what are we doing here?

##### Step 1: Initialization

Sort original array, then build all pairs of indices (i, j), sort by (arr[i] + arr[j]), then i, then j

##### Step 2: Run 2-pointer on the sums

##### Step 3: Given sums s1 & s2, determine in $O(1)$ time there exists two pairs of non-clashing indices

This is mostly done by inspecting the first pair under the smaller sum and last pair under the larger sum, and deriving properties about the rest of the pairs. 
For example, the s1 = s2 case (Step 3a) has been proofread and is correct. For Step 3b, I can vouch that the i1 = i2 & j1 = i2 cases are correct, I believe that j1 = j2 is also correct...? That one's too much of a headache to prove, even for me.

Interested readers can walk through the steps and see how they derive the correct answer.


...We're not doing that, though.
Let's see something much cleaner and intuitive.

# Another idea
---
It started when I tried to find a counterexample for the Step 3b, i2 = j1 case. 
![[Pasted image 20260908114423.png]]

a+b+c+d=11 is a really restrictive condition for unique positive integers. As any Killer Sudoku player would know, if a pair summed to 4 while another summed to 7 and they ended up in the same 3x3 block, the answer would have to be (1, 3), (2, 5).

However, arr = [1, 2, 3, 4, 5, 6], sum1 = 4, sum2 = 7 is a configuration that the proposed solution really struggles with, precisely because the (2, 5) lands smack-dab in the middle of the sum = 7 pairs, yet it's necessary for the final answer.
Keen-eyed readers may notice that the solution constructed **a whole extra frequency map during precomputations**, specifically to handle this type of case. It works, but just barely.

Granted, in a vacuum, finding something like this would be complex, and I can't think of a cleaner approach to find the answer, but that got me thinking... *Why do we have to find this contrived pair of sums, anyway?*

*...In fact, wouldn't we have found (1, 2, 3, 5) in the 3+8 case and be done with it?*

# (The cooler) Solution
---
Introducing... the **"Anything Short Of Perfect Is Useless" Lemma**
(Wow haha such a normal name and ideology to live by haha I'm not projecting what are you talking about)

Notice that if $a \leq b \leq c \leq d$, then $a+b$ is (among) the smallest pairwise sums, and $c+d$ is (among) the largest pairwise sums. Therefore, ==if $a+b+c+d=target$, and we ran two pointer on the list of sums, we will have found the solution $(a, b, c, d)$ via the sums of $(a, b)$ & $(c, d)$==. Since we also sorted the index pairs via lexicographical order to break ties, we know that this idea holds, even with multiple indices pointing to the same value.

So, the solution now becomes...(Drumroll please)

##### Step 1: Sort the original array
##### Step 2: Generate the $\frac{n \cdot (n - 1)}{2}$ index pairs (i, j), and sort by arr[i] + arr[j], break ties by i, then j.

##### Step 3: Run the

[Hm. It appears that there may be certain things I have not thought through. I will update this note once I do.]
...Well, not exactly. I think I can still make it work by using a frequency array to help me cheat under 4-Sum without exceeding the $O(n^2logn)$ bound, but that's shameless and boring and not generalizeable so I won't take it.
[The name of the author of the original solution has been redacted by their request.]