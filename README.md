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

---
## [Minimum Subsequence in Non-Increasing Order]](https://leetcode.com/problems/minimum-subsequence-in-non-increasing-order/)

*Given the array nums, obtain a subsequence of the array whose sum of elements is strictly greater than the sum of the non included elements in such subsequence.*

*If there are multiple solutions, return the subsequence with minimum size and if there still exist multiple solutions, return the subsequence with the maximum total sum of all its elements. A subsequence of an array can be obtained by erasing some (possibly zero) elements from the array.*

NB: the solution with the given constraints is guaranteed to be unique. Also return the answer sorted in non-increasing order.



##### Example 1:
```
Input: nums = [4,3,10,9,8]
Output: [10,9]
Explanation: The subsequences [10,9] and [10,8] are minimal such that the sum of their elements is strictly greater than the sum of elements not included, however, the subsequence [10,9] has the maximum total sum of its elements.
```

##### Example 2:
```
Input: nums = [4,4,7,6,7]
Output: [7,7,6]
Explanation: The subsequence [7,7] has the sum of its elements equal to 14 which is not strictly greater than the sum of elements not included (14 = 4 + 4 + 6). Therefore, the subsequence [7,6,7] is the minimal satisfying the conditions. Note the subsequence has to returned in non-decreasing order.  
```

##### Example 3:
```
Input: nums = [6]
Output: [6]
```

### Few Lines Solution
```c++
class Solution {
public:
    vector<int> minSubsequence(vector<int>& nums) {
        vector<int> res;
        auto sub_sum = 0, rem_sum = accumulate(begin(nums), end(nums), 0);
        priority_queue<int> pq(begin(nums), end(nums));
        while (sub_sum <= rem_sum / 2) {
            res.push_back(pq.top());
            sub_sum += res.back();
            pq.pop();
        }
        return res;
    }
};
```

*Runtime: 40 ms  
Memory Usage: 10.8 MB*

### Efficient Solution

Above solution has many flaws like for example the fact that the priority_queue and the total (rem_sum) will force to loop twice over nums.

```c++
class Solution {
public:
    vector<int> minSubsequence(vector<int>& nums) {
        int arr[101] = {0};
        short total = 0;
        short current = 0;

        for (auto n : nums) {
            total += n;  
            arr[n]++;
        }
        nums.clear(); // we can reuse the same vector to save memory
        short i = 100;
        while (current <= total) {
            if (arr[i]--) {
                nums.push_back(i);
                current += i;
                total -= i;
            }
            else
                i--;
        }
        return nums;
    }
};
```

*Runtime: 12 ms  
Memory Usage: 10.5 MB*


---
## [Number of Steps to Reduce a Number in Binary Representation to One](https://leetcode.com/problems/number-of-steps-to-reduce-a-number-in-binary-representation-to-one/)

*Given a number s in their binary representation. Return the number of steps to reduce it to 1 under the following rules:*  

*If the current number is even, you have to divide it by 2.*  

*If the current number is odd, you have to add 1 to it.*  

*It's guaranteed that you can always reach to one for all testcases.*  


##### Example 1:
```
Input: s = "1101"
Output: 6
Explanation: "1101" corressponds to number 13 in their decimal representation.
Step 1) 13 is odd, add 1 and obtain 14.
Step 2) 14 is even, divide by 2 and obtain 7.
Step 3) 7 is odd, add 1 and obtain 8.
Step 4) 8 is even, divide by 2 and obtain 4.  
Step 5) 4 is even, divide by 2 and obtain 2.
Step 6) 2 is even, divide by 2 and obtain 1.  
```

##### Example 2:
```
Input: s = "10"
Output: 1
Explanation: "10" corressponds to number 2 in their decimal representation.
Step 1) 2 is even, divide by 2 and obtain 1.  
```

##### Example 3:
```
Input: s = "1"
Output: 0
```

##### Constraints:
```
1 <= s.length <= 500
s consists of characters '0' or '1'
s[0] == '1'
```

### Overflow Solution

```c++
class Solution {
public:
    int numSteps(string s) {
        int i = 0;
        int n = stoi(s, 0, 2);
        while (n > 1)
        {
            if (n & 1)
                ++n;
            else
                n >>= 1;
            ++i;
        }
        return i;
    }
};
```

This solution will not work as s.length is between 1 and 500 (2^500 will give an overflow)

### Optimal Solution

```c++
class Solution {
public:
    int numSteps(string s) {
        int i = s.length() - 1;
        int step = 0;

        while (i > 0)
        {
            if (s[i] == '1')
            {
                do {
                    step++;
                    i--;
                } while (s[i] == '1' && i > 0);
                step += (i == 0) ;
                s[i] = '1';
            }
            else
                --i;
            step++;

        }

        return step;
    }
};
```
*Runtime: 4 ms  
Memory Usage: 6.3 MB*


### Even faster Solution

```c++
class Solution {
public:
    int numSteps(string s) {
        short res = 0, rem = 0;
        for (auto i = s.size(); --i > 0; res++) {
            if (s[i] - '0' + rem == 1) {
                rem = 1;
                res++;
            }
        }
        return res + rem;
    }
};
```
*Runtime: 0 ms  
Memory Usage: 6.5 MB*


---
## [Construct K Palindrome Strings](https://leetcode.com/problems/construct-k-palindrome-strings/)

*Given a string s and an integer k. You should construct k non-empty palindrome strings using all the characters in s.*  

*Return True if you can use all the characters in s to construct k palindrome strings or False otherwise.*  

##### Example 1:
```
Input: s = "annabelle", k = 2
Output: true
Explanation: You can construct two palindromes using all characters in s.
Some possible constructions "anna" + "elble", "anbna" + "elle", "anellena" + "b"
```

##### Example 2:
```
Input: s = "leetcode", k = 3
Output: false
Explanation: It is impossible to construct 3 palindromes using all the characters of s.
```

##### Example 3:
```
Input: s = "true", k = 4
Output: true
Explanation: The only possible solution is to put each character in a separate string.
```

##### Example 4:
```
Input: s = "yzyzyzyzyzyzyzy", k = 2
Output: true
Explanation: Simply you can put all z's in one string and all y's in the other string. Both strings will be palindrome.
```

##### Example 5:
```
Input: s = "cr", k = 7
Output: false
Explanation: We don't have enough characters in s to construct 7 palindromes.
```

##### Constraints:
```
1 <= s.length <= 10^5
All characters in s are lower-case English letters.
1 <= k <= 10^5
```

### Solution

```c++
static int lambda_0 = []() { std::ios::sync_with_stdio(false); cin.tie(NULL); return 0; }();class

class Solution {
public:    
    bool canConstruct(string s, int k) {
        __int128 ret = 0;
        __int128 a = 1;
        for (char c : s) ret ^= a << c;

        return __builtin_popcount(ret >> 96) <= k && (s.size() >= k);
    }
};
```
*Runtime: 12 ms  
Memory Usage: 12 MB*

---
## [Longest Happy String](https://leetcode.com/problems/longest-happy-string)

*A string is called happy if it does not have any of the strings 'aaa', 'bbb' or 'ccc' as a substring.*  

*Given three integers a, b and c, return any string s, which satisfies following conditions:*  
```
s is happy and longest possible.
s contains at most a occurrences of the letter 'a', at most b occurrences of the letter 'b' and at most c occurrences of the letter 'c'.
s will only contain 'a', 'b' and 'c' letters.
If there is no such string s return the empty string "".
```


##### Example 1:
```
Input: a = 1, b = 1, c = 7
Output: "ccaccbcc"
Explanation: "ccbccacc" would also be a correct answer.
```

##### Example 2:
```
Input: a = 2, b = 2, c = 1
Output: "aabbc"
```

##### Example 3:
```
Input: a = 7, b = 1, c = 0
Output: "aabaa"
Explanation: It's the only correct answer in this case.
```

##### Constraints:
```
0 <= a, b, c <= 100
a + b + c > 0
```

### [Solution](https://leetcode.com/problems/longest-happy-string/discuss/564277/C%2B%2BJava-a-greater-b-greater-c)
```c++
string longestDiverseString(int a, int b, int c, char aa = 'a', char bb = 'b', char cc = 'c') {
    if (a < b)
        return longestDiverseString(b, a, c, bb, aa, cc);
    if (b < c)
        return longestDiverseString(a, c, b, aa, cc, bb);
    if (b == 0)
        return string(min(2, a), aa);
    auto use_a = min(2, a), use_b = a - use_a >= b ? 1 : 0;
    return string(use_a, aa) +  string(use_b, bb) +
		longestDiverseString(a - use_a, b - use_b, c, aa, bb, cc);
}
```

---
## [Day 5 - Best Time to Buy and Sell Stock II](https://leetcode.com/problems/move-zeroes/)

*Say you have an array for which the ith element is the price of a given stock on day i.*  

*Design an algorithm to find the maximum profit. You may complete as many transactions as you like (i.e., buy one and sell one share of the stock multiple times).*  

*Note: You may not engage in multiple transactions at the same time (i.e., you must sell the stock before you buy again).*  

##### Example 1:
```
Input: [7,1,5,3,6,4]
Output: 7
Explanation: Buy on day 2 (price = 1) and sell on day 3 (price = 5), profit = 5-1 = 4.
             Then buy on day 4 (price = 3) and sell on day 5 (price = 6), profit = 6-3 = 3.
```

##### Example 2:
```
Input: [1,2,3,4,5]
Output: 4
Explanation: Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4.
             Note that you cannot buy on day 1, buy on day 2 and sell them later, as you are
             engaging multiple transactions at the same time. You must sell before buying again.
```

##### Example 3:
```
Input: [7,6,4,3,1]
Output: 0
Explanation: In this case, no transaction is done, i.e. max profit = 0.
```

### Solution

```
static int lambda_0 = []() { std::ios::sync_with_stdio(false); cin.tie(NULL); return 0; }();


class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int ret = 0;
        for (int i = 1; i < prices.size(); i++) {
            if (prices[i] - prices[i-1] > 0) {
                ret += (prices[i] - prices[i-1]) ;

            }
        }
        return ret;
    }
};
```

*Runtime: 4 ms  
Memory Usage: 7.5 MB*



---
## [Day 6 - Group Anagrams](https://leetcode.com/problems/group-anagrams/)


*Given an array of strings, group anagrams together.*  

##### Example:
```
Input: ["eat", "tea", "tan", "ate", "nat", "bat"],
Output:
[
  ["ate","eat","tea"],
  ["nat","tan"],
  ["bat"]
]
```

##### Note:

All inputs will be in lowercase.  
The order of your output does not matter.  

### Solution
```c++
static int lambda_0 = []() { std::ios::sync_with_stdio(false); cin.tie(NULL); return 0; }();

class Solution {
public:
    uint32_t getHash(string &word) {
        static int primes[123] = {0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 7, 59, 29, 31, 2, 67, 41, 53, 5, 97, 73, 23, 47, 11, 19, 43, 101, 13, 3, 17, 37, 71, 79, 89, 61, 83}; // 123 because 'a' position is 97 and we add 26. Then we use the 26 first prime numbers and order them by occurence of letters (like 'e' (5th after the streak of 0s) is most frequent so we give it 2 and 101 for 'q' which is the rarest.

        uint32_t hash = 1;
        for (char &c : word) {
            int prime = primes[c];
            hash *= prime;
        }
        return hash;
    }
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        unordered_map<uint32_t, int> anagramHashTable;
        anagramHashTable.reserve(strs.size() >> 3);
        unordered_map<uint32_t,int>::iterator it;
        uint32_t a = 0;
        uint32_t myHash;
        vector<vector<string>> res;
        res.reserve(strs.size() >> 3);

        for (auto &s : strs) {
            if ((it = anagramHashTable.find(myHash = getHash(s))) == anagramHashTable.end()) { // myHash was not previously compounded
                anagramHashTable[myHash] = a++; // we create a new entry and set the value to the index of our returned vector.
                res.push_back(vector<string> {s});
            }
            else
                res[it->second].push_back(s);
        }

        return res;
    }
};
```

*Runtime: 40 ms  
Memory Usage: 14 MB*


---
## [Counting Elements]()

*Given an integer array arr, count element x such that x + 1 is also in arr.*  

*If there're duplicates in arr, count them seperately.*  

##### Example 1:
```
Input: arr = [1,2,3]
Output: 2
Explanation: 1 and 2 are counted cause 2 and 3 are in arr.
```

##### Example 2:
```
Input: arr = [1,1,3,3,5,5,7,7]
Output: 0
Explanation: No numbers are counted, cause there's no 2, 4, 6, or 8 in arr.
```

##### Example 3:
```
Input: arr = [1,3,2,3,5,0]
Output: 3
Explanation: 0, 1 and 2 are counted cause 1, 2 and 3 are in arr.
```

##### Example 4:
```
Input: arr = [1,1,2,2]
Output: 2
Explanation: Two 1s are counted cause 2 is in arr.
 ```

##### Constraints:

1 <= arr.length <= 1000  
0 <= arr[i] <= 1000

### Solution

```c++
class Solution {
public:
    int countElements(vector<int>& arr) {
        int count[1001] = {0};
        int ret = 0;

        for (auto &n : arr) count[n]++;
        for (int i = 0; i < 1000; i++) ret += (count[i] && count[i+1]) * count[i];

        return ret;
    }
};
```

*Runtime: 0 ms  
Memory Usage: 6.6 MB*

---
## [Counting Bits](https://leetcode.com/problems/counting-bits/)

*Given a non negative integer number num. For every numbers i in the range 0 ≤ i ≤ num calculate the number of 1's in their binary representation and return them as an array.*

##### Example 1:
```
Input: 2
Output: [0,1,1]
```

##### Example 2:
```
Input: 5
Output: [0,1,1,2,1,2]
```

##### Follow up:

It is very easy to come up with a solution with run time O(n*sizeof(integer)). But can you do it in linear time O(n) /possibly in a single pass?  
Space complexity should be O(n).  
Can you do it like a boss? Do it without using any builtin function like __builtin_popcount in c++ or in any other language.

### Solution

You will notice a specific pattern
```
/* pattern
       [0,
           1,                                      2^0
           1,                  2,                  2^1
           1,2,                2,3,                2^2
           1,2,2,3,            2,3,3,4,            2^3
           1,2,2,3,2,3,3,4,    2,3,3,4,3,4,4,5,    2^4
           1 ...]                                  2^5
         */
```

Which can be translated as the following algorithm:

```c++
class Solution {
public:
    vector<int> countBits(int num) {
        vector<int> v(num+1);
        v[0] = 0;

        for (int i = 1 ; i <= num ; i++)
            v[i] = (i & 1) + v[i >> 1];

        return v;
    }
};
```

*Runtime: 48 ms  
Memory Usage: 7.1 MB*

**NB: If Leetcode was compiling with c++20 we could potentially get values for the vector at compile time and then trunc it with ```v.erase(v.begin() + num + 1, v.end());```**  
