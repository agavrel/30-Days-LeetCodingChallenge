# 30-Days-LeetCodingChallenge

C++ Lowest-Latency Solutions for https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/

*NB: Add the following at the top to optimize latency*

```c++
static int lambda_0 = []() { std::ios::sync_with_stdio(false); cin.tie(NULL); return 0; }();
```

---
## [Day 1 - Single Number](https://leetcode.com/problems/single-number/)

*Given a non-empty array of integers, every element appears twice except for one. Find that single one.*

##### Note:

Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

##### Example 1:
```
Input: [2,2,1]
Output: 1
```

##### Example 2:
```
Input: [4,1,2,1,2]
Output: 4
```

### Solution

```c++
static int lambda_0 = []() { std::ios::sync_with_stdio(false); cin.tie(NULL); return 0; }();

class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int res = 0;

        for (const int a:nums) {
            res ^=a;
        }
        return res;

    }
};
```

*Runtime: 4 ms  
Memory Usage: 7.5 MB*

---
## [Day 2 - Happy Number](https://leetcode.com/problems/happy-number/)


*Write an algorithm to determine if a number is "happy".*

*A happy number is a number defined by the following process: Starting with any positive integer, replace the number by the sum of the squares of its digits, and repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1. Those numbers for which this process ends in 1 are happy numbers.*

##### Example:
```
Input: 19
Output: true
Explanation:
12 + 92 = 82
82 + 22 = 68
62 + 82 = 100
12 + 02 + 02 = 1
```

### Solution

```c++
class Solution {
public:
    bool isHappy(int n) {
        while (n > 9)
        {
            short sumOfSquared = 0;
            do {
                short squaredDigit = n % 10;
                sumOfSquared += squaredDigit * squaredDigit;
            } while (n /= 10);
            n = sumOfSquared;
        }
        return n == 1 || n == 7;
    }
};
```
*Runtime: 0 ms  
Memory Usage: 5.9 MB*

or

```c++
class Solution {
public:
    bool isHappy(int n) {
        bool happyMap[10] = {false, [1] = true, [7] = true};         

        while (n > 9)
        {
            short sumOfSquared = 0;
            do {
                short squaredDigit = n % 10;
                sumOfSquared += squaredDigit * squaredDigit;
            } while (n /= 10);
            n = sumOfSquared;
        }
        return happyMap[n];
    }
};
```
*Runtime: 0 ms  
Memory Usage: 5.8 MB*

### [Explanation with this excellent blog article](https://www.stem.org.uk/news-and-views/opinions/how-find-happy-number)  

Unhappy numbers migrate towards a cyclical loop that includes 4, 16, 37, 58, 89, 145, 42, and 20.  

![Unhappy Numbers](https://raw.githubusercontent.com/agavrel/30-Days-LeetCodingChallenge/master/asset/unhappy_numbers.png)  

We can also observe that happy numbers converging to 1 and below 10 are either 1 and 7. Hence the above solutions  

![Happy Numbers](https://raw.githubusercontent.com/agavrel/30-Days-LeetCodingChallenge/master/asset/happy_numbers.png)  


 There are twenty happy numbers between 1 and 100. Hence we could even speed-up the algorithm by building an array with these 20 happy numbers and slightly change the condition:

 ```c++
 class Solution {
 public:
     bool isHappy(int n) {
         bool happyMap[101] = {false, [1] = true, [7] = true, [10] = true, [13] = true, [19] = true, [23] = true, [28] = true, [31] = true, [32] = true, [44] = true, [49] = true, [68] = true, [70] = true, [79] = true, [82] = true, [86] = true, [91] = true, [94] = true, [97] = true, [100] = true};         

         while (n > 100)
         {
             short sumOfSquared = 0;
             do {
                 short squaredDigit = n % 10;
                 sumOfSquared += squaredDigit * squaredDigit;
             } while (n /= 10);
             n = sumOfSquared;
         }
         return happyMap[n];
     }
 };
 ```


---
## [Day 3 - Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)

*Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.*

##### Example:
```
Input: [-2,1,-3,4,-1,2,1,-5,4],
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
```

##### Follow up:

If you have figured out the O(n) solution, try coding another solution using the divide and conquer approach, which is more subtle.

### Solution:

```c++
class Solution {
public:
    int max(int a, int b) { return (a > b)? a : b; }

    int maxSubArray(vector<int>& nums) {
        int currentStreak = 0;
        int largestSum = INT_MIN;
        for(const int n: nums) {
            currentStreak += n;
            if (currentStreak < n) // reset currentStreak if pointless to keep
                currentStreak = n;
            largestSum = max(largestSum, currentStreak);
        }
        return largestSum;   
    }
};
```

*Runtime: 4 ms  
Memory Usage: 7 MB*


---
## [Day 4 - Move Zeroes](https://leetcode.com/problems/move-zeroes/)

*Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.*

##### Example:
```
Input: [0,1,0,3,12]
Output: [1,3,12,0,0]
```

###### Note:

You must do this in-place without making a copy of the array.  
Minimize the total number of operations.

### Solution:

```c++
class Solution {
public:
    void moveZeroes(vector<int>& nums) {  
        fill(remove(nums.begin(), nums.end(), 0), nums.end(), 0);  
    }
};
```

*Another way:*

```c++
class Solution {
public:
    void moveZeroes(vector<int>& nums) {  
        unsigned int len = 0;
        vector<int>::iterator it = nums.begin();
        while (it != nums.end())
        {
            if (*it == 0) {
                it = nums.erase(it);
                len++;
            }
            else
                it++;
        }
        fill_n(std::back_inserter(nums), len, 0);
    }
};
```
