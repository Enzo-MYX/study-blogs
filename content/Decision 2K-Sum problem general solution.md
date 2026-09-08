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

Granted, in a vacuum, finding something like this would be complex, 