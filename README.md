# Challenge 1

Given an array of integers, write a function that returns the maximum sum of any contiguous subarray.

Example:
Input: [1, -2, 3, 4, -1, 2, -3, 5 ]
Output: 11 (corresponding to the subarray [3, 4, -1, 2, -3, 5])

//Code

public class MaximumSubarraySum {

    public static int maxSubarraySum(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }

        int maxSum = nums[0];
        int currentSum = nums[0];

        for (int i = 1; i < nums.length; i++) {
            currentSum = Math.max(nums[i], currentSum + nums[i]);
            maxSum = Math.max(maxSum, currentSum);
        }

        return maxSum;
    }

    public static void main(String[] args) {
    Scanner scanner = new Scanner(System.in);

        System.out.print("Enter the size of the array: ");
        int size = scanner.nextInt();

        int[] userArray = new int[size];

        System.out.println("Enter the elements of the array:");

        for (int i = 0; i < size; i++) {
            System.out.print("Element " + (i + 1) + ": ");
            userArray[i] = scanner.nextInt();
        }
        int result = maxSubarraySum(userArray);
        System.out.println("Maximum Contiguous Subarray Sum: " + result);
    }
}
