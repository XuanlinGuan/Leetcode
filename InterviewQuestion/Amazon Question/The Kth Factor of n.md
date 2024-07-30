
1492. The kth Factor of n
Solved
Medium
Topics
Companies
Hint
You are given two positive integers n and k. A factor of an integer n is defined as an integer i where n % i == 0.

Consider a list of all factors of n sorted in ascending order, return the kth factor in this list or return -1 if n has less than k factors.

 

Example 1:

Input: n = 12, k = 3
Output: 3
Explanation: Factors list is [1, 2, 3, 4, 6, 12], the 3rd factor is 3.
Example 2:

Input: n = 7, k = 2
Output: 7
Explanation: Factors list is [1, 7], the 2nd factor is 7.
Example 3:

Input: n = 4, k = 4
Output: -1
Explanation: Factors list is [1, 2, 4], there is only 3 factors. We should return -1.
 

Constraints:

1 <= k <= n <= 1000



    public class Solution {
    public int kthFactor(int n, int k) {
        // 存储小于等于sqrt(n)的因子
        int[] smallDivisors = new int[n];
        // 存储大于sqrt(n)的因子
        int[] largeDivisors = new int[n];
        int smallCount = 0;
        int largeCount = 0;

        for (int i = 1; i * i <= n; i++) {
            if (n % i == 0) {
                smallDivisors[smallCount++] = i; // 将因子存入数组
                if (i != n / i) {
                    largeDivisors[largeCount++] = n / i; // 只有当i不等于n/i时才添加
                }
            }
        }

        // 检查k是否在因子总数的范围内
        if (k <= smallCount + largeCount) {
            if (k <= smallCount) {
                return smallDivisors[k - 1]; // 直接从小因子数组中取值
            } else {
                return largeDivisors[largeCount - (k - smallCount)]; // 从大因子数组逆序取值
            }
        }

        return -1; // 如果k大于因子总数，返回-1
    }

    public static void main(String[] args) {
        Solution sol = new Solution();
        System.out.println(sol.kthFactor(12, 3)); // 输出: 3
        System.out.println(sol.kthFactor(7, 2));  // 输出: 7
        System.out.println(sol.kthFactor(4, 4));  // 输出: -1
    }
}

空间时间 复杂度:    
    1. 空间: $\sqrt{n}$    
    2. 时间: $\sqrt{n}$ 