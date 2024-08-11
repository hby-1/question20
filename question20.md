# 和有限的最长子序列

给你一个长度为 `n` 的整数数组 `nums` ，和一个长度为 m 的整数数组 `queries` 。

返回一个长度为 `m` 的数组 `answer` ，其中 `answer[i]` 是` nums` 中 元素之和小于等于 `queries[i]` 的 **子序列** 的 **最大** 长度  。

**子序列** 是由一个数组删除某些元素（也可以不删除）但不改变剩余元素顺序得到的一个数组。

## 示例 1：
>### 输入：
>nums = [4,5,2,1], queries = [3,10,21]
>### 输出：
>[2,3,4]
>### 解释：
>queries 对应的 answer 如下：
- 子序列 [2,1] 的和小于或等于 3 。可以证明满足题目要求的子序列的最大长度是 2 ，所以 answer[0] = 2 。
- 子序列 [4,5,1] 的和小于或等于 10 。可以证明满足题目要求的子序列的最大长度是 3 ，所以 answer[1] = 3 。
- 子序列 [4,5,2,1] 的和小于或等于 21 。可以证明满足题目要求的子序列的最大长度是 4 ，所以 answer[2] = 4 。

## 示例 2：
>### 输入：
>nums = [2,3,4,5], queries = [1]
>### 输出：
>[0]
>### 解释：
>空子序列是唯一一个满足元素和小于或等于 1 的子序列，所以 answer[0] = 0 。

## 代码：

1.

    public class Solution {
        public int[] AnswerQueries(int[] nums, int[] queries) {
            Array.Sort(nums);
            int n = nums.Length, m = queries.Length;
            int[] prefixSums = new int[n + 1];
            for (int i = 0; i < n; i++) {
                prefixSums[i + 1] = prefixSums[i] + nums[i];
            }
            int[] answer = new int[m];
            for (int i = 0; i < m; i++) {
                answer[i] = BinarySearch(prefixSums, queries[i]);
            }
            return answer;
        }

        public int BinarySearch(int[] prefixSums, int target) {
            int low = -1, high = prefixSums.Length - 1;
            while (low < high) {
                int mid = low + (high - low + 1) / 2;
                if (prefixSums[mid] <= target) {
                    low = mid;
                } else {
                    high = mid - 1;
                }
            }
            return low;
        }
    }
2.

    public class Solution {
        public int[] AnswerQueries(int[] nums, int[] queries) {
            Array.Sort(nums);
            int n = nums.Length, m = queries.Length;
            int[] answer = new int[m];
            for (int i = 0; i < m; i++) {
                int query = queries[i];
                int size = 0;
                int sum = 0;
                for (int j = 0; j < n; j++) {
                    if (sum + nums[j] > query) {
                        break;
                    }
                    sum += nums[j];
                    size++;
                }
                answer[i] = size;
            }
            return answer;
        }
    }
3.

    public class Solution {
        public int[] AnswerQueries(int[] nums, int[] queries) {
            Array.Sort(nums);
            int[] answer=new int[queries.Length];
            for(int i=0;i<queries.Length;i++){
                int m=0;
                for(int n=0;n<nums.Length;n++){
                    m+=nums[n];
                    if(m<=queries[i]){
                        answer[i]=n+1;
                    }
                    else{
                        break;
                    }
                }
            }
            return answer;
        }
    }
