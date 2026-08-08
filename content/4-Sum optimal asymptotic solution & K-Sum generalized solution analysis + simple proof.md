This is the same as the one I presented in LeetCode for the enumeration version of the [4-Sum problem](https://leetcode.com/problems/4sum/description/). Enjoy.
# Intuition

Has anyone looked at this question and thought, 'Wow I could save so much time if I just copy-pasted my work from 3Sum, slapped a loop onto it, and called it a day'?  
Well that's what we're doing now.

# Basic Idea

Consider an ideal case: If we had a solver method for 3-Sum problems— let's call it solve3(int[] arr, int start, int end, int target)— where solve3 returns all 3-Sum solutions with elements from arr.subarray(start, end) (start inclusive, end exclusive) hitting a sum of target. We also have the array sorted already. How do we solve this problem?

Well, we could "take away one of the smallest element" and solve for a sum of target-nums[0].  
I.e., call solve3(nums, 1, nums.length, target-nums[0]).  
If we add that nums[0] back in every combination, this would give us all solutions where the smallest element is nums[0].  
Then, we could "take away all copies of the smallest element, and one of the second smallest", and solve again.  
Say the index of the second smallest is _i_, we'd be solving for solve3(nums, _i_+1, nums.length, target-nums[_i_]). Adding nums[_i_] back to every combination we got, this would be all solutions where the smallest element is nums[_i_].

Notice the pattern. If we iterate through all different elements, we obtain all combinations, thereby solving the 4-Sum problem.

# My Approach

Examining the basic idea, we see that it doesn't matter if you iterate the smallest or largest element. Using the largest requires fewer changes in my code, so I opted for that.

I also didn't have the pointer version of 3Sum solver, so I had to White-Box reuse that code. Having the pointer version means you get to perform blackbox reusage without incurring copyOfRange costs (which, doesn't change asymptotic time, I just don't like it)

Of course, there's still a lot to be improved in actual runtime, as smarter users probably have better ways to handle integer overflow, or skip loops when elements are clearly too big/small. I'll leave all that to the pros.

# Complexity

- Time complexity:  
    O(n3)
    
- Space complexity:  
    O(logn) for Arrays.sort (O(1) for in-place sorts like Selection Sort)  
    O(K) for generalized K-sum problem
    

# Generalization

As demonstrated above, from running a K-Sum solver at most n times on a sorted array we obtain a solver for (K+1)-Sum problems. With a base case of K=2 being classic Two-Pointer solution, we get the generalized algorithm idea.  
For K≥3, optimal time complexity is O(n^{K−1}), and optimal space complexity is O(1).

# Code

```java
class Solution {
    public List<List<Integer>> fourSum(int[] nums, int target) {
        Arrays.sort(nums);
        List<List<Integer>> ans = new ArrayList<>();
        for (int n = nums.length - 1; n > 2; n--) {
            if (n < nums.length - 1 && nums[n] == nums[n + 1]) continue;
            for (int i = 0; i < n - 2; i++) {
                if (i > 0 && nums[i] == nums[i - 1]) continue;
                int j = i + 1;
                int k = n - 1;
                while (j < k) {
                    long sum = (long) nums[i] + nums[j] + nums[k] + nums[n];
                    if (sum < target) {
                        j++;
                        continue;
                    } else if (sum > target) {
                        k--;
                        continue;
                    } else {
                        ans.add(Arrays.asList(nums[i], nums[j], nums[k], nums[n]));
                        while (j < k && nums[j] == nums[j + 1]) {
                            j++;
                        }
                        j++;
                        while (j < k && nums[k] == nums[k - 1]) {
                            k--;
                        }
                        k--;
                    }
                }
            }
        }
        return ans;
    }
}
```