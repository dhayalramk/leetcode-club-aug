## Method 1: Brute Force Approach

Breath first search. Going +1 and -1 on from the current value, till the end to find the possibility

```python
class Solution:
    def findTargetSumWays(self, nums: List[int], target: int) -> int:
        def backtrack(i, current_sum):
            if i == len(nums):
                return 1 if current_sum == target else 0
            return (
                backtrack(i+1, current_sum + nums[i])
                + backtrack(i+1, current_sum - nums[i])
            )
        return backtrack(0, 0)
```
----

## Method 1: Enhancement with DP. Memorization
Reason: It's repated with same re-calculation

```python
from typing import List

class Solution:
    def findTargetSumWays(self, nums: List[int], target: int) -> int:
        dp = {}

        def backtrack(i: int, current_sum: int) -> int:
            if (i, current_sum) in dp:
                return dp[(i, current_sum)]
            if i == len(nums):
                return 1 if current_sum == target else 0

            dp[(i, current_sum)] = (
                backtrack(i + 1, current_sum + nums[i]) +
                backtrack(i + 1, current_sum - nums[i])
            )
            return dp[(i, current_sum)]

        return backtrack(0, 0)

```
