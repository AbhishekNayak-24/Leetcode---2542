# Leetcode---2542
Maximum Subsequence Score
//code in java
import java.util.*;

class Solution {
    public long maxScore(int[] nums1, int[] nums2, int k) {
        int n = nums1.length;
        int[][] pairs = new int[n][2];

        for (int i = 0; i < n; i++) {
            pairs[i][0] = nums2[i];
            pairs[i][1] = nums1[i];
        }

        Arrays.sort(pairs, (a, b) -> b[0] - a[0]);
        PriorityQueue<Integer> minHeap = new PriorityQueue<>();
        long sum = 0, result = 0;

        for (int i = 0; i < n; i++) {
            sum += pairs[i][1];
            minHeap.add(pairs[i][1]);

            if (minHeap.size() > k) {
                sum -= minHeap.poll();
            }

            if (minHeap.size() == k) {
                result = Math.max(result, sum * pairs[i][0]);
            }
        }

        return result;
    }

    public static void main(String[] args) {
        Solution solution = new Solution();
        int[] nums1 = {1, 3, 3, 2};
        int[] nums2 = {2, 1, 3, 4};
        int k = 3;
        long result = solution.maxScore(nums1, nums2, k);
        System.out.println("The maximum subsequence score is: " + result);
    }
}
