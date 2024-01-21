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

# Challenge 3

Calculate Average and Deviation of JSON Objects with Subjects

**Input:**

- The input is an array of JSON objects, where each object has a "name" field (string) and a "grades" field (list of objects with "subject" and "grade" fields).

**Output:**

- The output is a dictionary with the following keys:
    - "average_grades": a list of floats representing the average grade for each student.
    - "average_subjects": a list of floats representing the average grade for each subject across all students.
    - "overall_average": a float representing the overall average grade across all students.
    - "std_deviation": a float representing the standard deviation of grades across all students.

import math
import statistics

students_data = [
    {
        "name": "John Doe",
        "grades": [
            {"subject": "Math", "grade": 90},
            {"subject": "English", "grade": 85},
            {"subject": "Science", "grade": 92},
            {"subject": "History", "grade": 88},
            {"subject": "Art", "grade": 95}
        ]
    },
    {
        "name": "Jane Smith",
        "grades": [
            {"subject": "Math", "grade": 88},
            {"subject": "English", "grade": 92},
            {"subject": "Science", "grade": 87},
            {"subject": "History", "grade": 90},
            {"subject": "Art", "grade": 93}
        ]
    },
    {
        "name": "Bob Johnson",
        "grades": [
            {"subject": "Math", "grade": 78},
            {"subject": "English", "grade": 85},
            {"subject": "Science", "grade": 80},
            {"subject": "History", "grade": 88},
            {"subject": "Art", "grade": 82}
        ]
    }
]

# Gather all grades for each subject across all students
grades_by_subject = {}
for student in students_data:
    for subject_info in student['grades']:
        subject = subject_info['subject']
        grade = subject_info['grade']
        if subject in grades_by_subject:
            grades_by_subject[subject].append(grade)
        else:
            grades_by_subject[subject] = [grade]

# Calculate average grades for each student
average_grades = [statistics.mean(student['grades'], key=lambda x: x['grade']) for student in students_data]

# Calculate average grades for each subject
average_subjects = [statistics.mean(grades) for grades in grades_by_subject.values()]

# Calculate overall average
overall_average = statistics.mean(average_grades)

# Calculate standard deviation
all_grades = [grade for grades in grades_by_subject.values() for grade in grades]
std_deviation = statistics.stdev(all_grades)

# Prepare the expected output
expected_output = {
    "average_grades": average_grades,
    "average_subjects": average_subjects,
    "overall_average": overall_average,
    "std_deviation": std_deviation
}

print(expected_output)

import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;
import java.util.stream.Collectors;

public class StudentGrades {

    public static void main(String[] args) {
        List<Map<String, Object>> studentsData = List.of(
            Map.of("name", "John Doe", "grades", List.of(
                Map.of("subject", "Math", "grade", 90),
                Map.of("subject", "English", "grade", 85),
                Map.of("subject", "Science", "grade", 92),
                Map.of("subject", "History", "grade", 88),
                Map.of("subject", "Art", "grade", 95)
            )),
            Map.of("name", "Jane Smith", "grades", List.of(
                Map.of("subject", "Math", "grade", 88),
                Map.of("subject", "English", "grade", 92),
                Map.of("subject", "Science", "grade", 87),
                Map.of("subject", "History", "grade", 90),
                Map.of("subject", "Art", "grade", 93)
            )),
            Map.of("name", "Bob Johnson", "grades", List.of(
                Map.of("subject", "Math", "grade", 78),
                Map.of("subject", "English", "grade", 85),
                Map.of("subject", "Science", "grade", 80),
                Map.of("subject", "History", "grade", 88),
                Map.of("subject", "Art", "grade", 82)
            ))
        );

        // Gather all grades for each subject across all students
        Map<String, List<Integer>> gradesBySubject = new HashMap<>();
        studentsData.forEach(student -> {
            List<Map<String, Object>> grades = (List<Map<String, Object>>) student.get("grades");
            grades.forEach(gradeInfo -> {
                String subject = (String) gradeInfo.get("subject");
                int grade = (int) gradeInfo.get("grade");
                gradesBySubject.computeIfAbsent(subject, k -> new ArrayList<>()).add(grade);
            });
        });

        // Calculate average grades for each student
        List<Double> averageGrades = studentsData.stream()
            .map(student -> ((List<Map<String, Object>>) student.get("grades")).stream()
                .collect(Collectors.averagingInt(gradeInfo -> (int) gradeInfo.get("grade"))))
            .collect(Collectors.toList());

        // Calculate average grades for each subject
        List<Double> averageSubjects = gradesBySubject.values().stream()
            .map(grades -> grades.stream().collect(Collectors.averagingInt(Integer::intValue)))
            .collect(Collectors.toList());

        // Calculate overall average
        double overallAverage = averageGrades.stream().mapToDouble(Double::doubleValue).average().orElse(0);

        // Calculate standard deviation
        List<Integer> allGrades = gradesBySubject.values().stream()
            .flatMap(List::stream)
            .collect(Collectors.toList());

        double stdDeviation = calculateStandardDeviation(allGrades);

        // Prepare the expected output
        Map<String, Object> expectedOutput = Map.of(
            "average_grades", averageGrades,
            "average_subjects", averageSubjects,
            "overall_average", overallAverage,
            "std_deviation", stdDeviation
        );

        System.out.println(expectedOutput);
    }

    private static double calculateStandardDeviation(List<Integer> data) {
        double mean = data.stream().mapToInt(Integer::intValue).average().orElse(0);
        double variance = data.stream().mapToDouble(x -> Math.pow(x - mean, 2)).average().orElse(0);
        return Math.sqrt(variance);
    }
}
