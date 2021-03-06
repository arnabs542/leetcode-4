# 137-single-number-ii

## Question {#question}

[https://leetcode.com/problems/single-number-ii/description/](https://leetcode.com/problems/single-number-ii/description/)

Given an array of integers, every element appears three times except for one, which appears exactly once. Find that single one.

**Example:**

```text

```

**Note:**

Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

## Thought Process {#thought-process}

1. Check Every Bit
   1. We sum all the bit for current bit position, if the sum is divisible by 3, we know current bit is 0, otherwise is 1
   2. Time complexity O\(n\)
   3. Space complexity O\(1\)
2. asd

## Solution

```java
class Solution {
    public int singleNumber(int[] nums) {
        int res = 0;
        for (int i = 0; i < 32; i++) {
            int mask = 1 << i;
            int sum = 0;
            for (int num : nums) {
                sum += (mask & num) == 0 ? 0 : 1;
            }
            res |= (sum % 3) << i;
        }
        return res;
    }
}
```

```java
class Solution {
    public int singleNumber(int[] nums) {
        int one = 0, two = 0;
        for (int num : nums){
            // xor num save the num, if one is set right now, 1, two is 0
            // the second time we see the number, one will become 0, because
            // two is set, where & ~two will unset it, then two will become set.
            one = (one ^ num) & ~two;
            two = (two ^ num) & ~one;
        }
        return one;
    }
}
```

## Additional {#additional}

