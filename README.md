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


# Challenge 2

A palindrome is a sequence of characters that reads the same forward as backward. Your task is to write a function that finds and returns the longest palindromic substring in a given string. If there are multiple palindromes with the same length, return the one that appears first.

**Input:**

- The input string `s` consists of lowercase and/or uppercase letters and may contain spaces and other non-alphabetic characters.

**Output:**

- Return a string, which is the longest palindromic substring found in the input string.

**Example:**	

input_str = "babad"

**Expected Output:**
The function should return either "bab" or "aba" as both are valid palindromes of length 3 in the given input string.

public class LongestPalindromicSubstring {

    public static String longestPalindrome(String s) {
        if (s == null || s.length() < 1) {
            return "";
        }

        int start = 0, end = 0;

        for (int i = 0; i < s.length(); i++) {
            int len1 = expandAroundCenter(s, i, i);
            int len2 = expandAroundCenter(s, i, i + 1);
            int maxLength = Math.max(len1, len2);

            if (maxLength > end - start) {
                start = i - (maxLength - 1) / 2;
                end = i + maxLength / 2;
            }
        }

        return s.substring(start, end + 1);
    }

    private static int expandAroundCenter(String s, int left, int right) {
        while (left >= 0 && right < s.length() && s.charAt(left) == s.charAt(right)) {
            left--;
            right++;
        }
        return right - left - 1;
    }

    public static void main(String[] args) {
        String input_str = "babad";
        String result = longestPalindrome(input_str);
        System.out.println("Longest palindromic substring: " + result);
    }
}


