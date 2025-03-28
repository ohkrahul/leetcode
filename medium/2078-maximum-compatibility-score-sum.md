# Maximum Compatibility Score Sum

## Problem Link
[LeetCode - Maximum Compatibility Score Sum](https://leetcode.com/problems/maximum-compatibility-score-sum/)

## Difficulty
Medium

## Problem Description
<p>There is a survey that consists of <code>n</code> questions where each question&#39;s answer is either <code>0</code> (no) or <code>1</code> (yes).</p>

<p>The survey was given to <code>m</code> students numbered from <code>0</code> to <code>m - 1</code> and <code>m</code> mentors numbered from <code>0</code> to <code>m - 1</code>. The answers of the students are represented by a 2D integer array <code>students</code> where <code>students[i]</code> is an integer array that contains the answers of the <code>i<sup>th</sup></code> student (<strong>0-indexed</strong>). The answers of the mentors are represented by a 2D integer array <code>mentors</code> where <code>mentors[j]</code> is an integer array that contains the answers of the <code>j<sup>th</sup></code> mentor (<strong>0-indexed</strong>).</p>

<p>Each student will be assigned to <strong>one</strong> mentor, and each mentor will have <strong>one</strong> student assigned to them. The <strong>compatibility score</strong> of a student-mentor pair is the number of answers that are the same for both the student and the mentor.</p>

<ul>
	<li>For example, if the student&#39;s answers were <code>[1, <u>0</u>, <u>1</u>]</code> and the mentor&#39;s answers were <code>[0, <u>0</u>, <u>1</u>]</code>, then their compatibility score is 2 because only the second and the third answers are the same.</li>
</ul>

<p>You are tasked with finding the optimal student-mentor pairings to <strong>maximize</strong> the<strong> sum of the compatibility scores</strong>.</p>

<p>Given <code>students</code> and <code>mentors</code>, return <em>the <strong>maximum compatibility score sum</strong> that can be achieved.</em></p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> students = [[1,1,0],[1,0,1],[0,0,1]], mentors = [[1,0,0],[0,0,1],[1,1,0]]
<strong>Output:</strong> 8
<strong>Explanation:</strong>&nbsp;We assign students to mentors in the following way:
- student 0 to mentor 2 with a compatibility score of 3.
- student 1 to mentor 0 with a compatibility score of 2.
- student 2 to mentor 1 with a compatibility score of 3.
The compatibility score sum is 3 + 2 + 3 = 8.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> students = [[0,0],[0,0],[0,0]], mentors = [[1,1],[1,1],[1,1]]
<strong>Output:</strong> 0
<strong>Explanation:</strong> The compatibility score of any student-mentor pair is 0.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>m == students.length == mentors.length</code></li>
	<li><code>n == students[i].length == mentors[j].length</code></li>
	<li><code>1 &lt;= m, n &lt;= 8</code></li>
	<li><code>students[i][k]</code> is either <code>0</code> or <code>1</code>.</li>
	<li><code>mentors[j][k]</code> is either <code>0</code> or <code>1</code>.</li>
</ul>


## Test Cases
```
[[1,1,0],[1,0,1],[0,0,1]]
[[1,0,0],[0,0,1],[1,1,0]]
[[0,0],[0,0],[0,0]]
[[1,1],[1,1],[1,1]]
```

## Initial Template
```python
# Code template not available
```

## Solution
1. Initial Thoughts:
   - Problem analysis: We're given two 2D arrays representing student and mentor answers to a survey. We need to find the optimal pairing of students to mentors that maximizes the total compatibility score (sum of matching answers across all pairs).
   - Key observations: Since `m` and `n` are small (<= 8), we can explore all possible permutations of mentor assignments to students. This suggests a backtracking approach.
   - Possible approaches: Backtracking to try all pairings and keep track of the maximum compatibility score.  We can pre-calculate the compatibility scores between each student and mentor to avoid redundant computations during backtracking.

2. Solution Implementation:
```python
def maxCompatibilitySum(students, mentors):
    m = len(students)
    n = len(students[0])

    # Pre-calculate compatibility scores
    compatibility = [[0] * m for _ in range(m)]
    for i in range(m):
        for j in range(m):
            score = 0
            for k in range(n):
                if students[i][k] == mentors[j][k]:
                    score += 1
            compatibility[i][j] = score

    max_score = 0
    used_mentors = [False] * m

    def backtrack(student_idx, current_score):
        nonlocal max_score  # Access the outer scope max_score
        if student_idx == m:
            max_score = max(max_score, current_score)
            return

        for mentor_idx in range(m):
            if not used_mentors[mentor_idx]:
                used_mentors[mentor_idx] = True
                backtrack(student_idx + 1, current_score + compatibility[student_idx][mentor_idx])
                used_mentors[mentor_idx] = False  # Backtrack: unassign mentor

    backtrack(0, 0)
    return max_score
```

3. Solution Explanation:
   - How the solution works: We use a recursive backtracking function `backtrack`.  It explores assigning each student to a mentor, one by one. `used_mentors` keeps track of which mentors have already been assigned. The `compatibility` matrix stores pre-calculated scores for every student-mentor pair. At each level of recursion, we try assigning a free mentor to the current student and recursively call `backtrack` for the next student. When all students are assigned (base case), we update `max_score` if the current assignment has a higher total compatibility score.  Crucially, we backtrack by unassigning the mentor after the recursive call, allowing us to explore other pairings.
   - Key steps and logic explained:  Pre-calculating the compatibility scores helps avoid redundant computations inside the recursive function. The `used_mentors` array ensures each mentor is assigned only once.  Backtracking allows exploring all possible pairings.
   - Why this approach is effective: While seemingly brute-force, the backtracking approach systematically checks all valid pairings and guarantees finding the optimal solution. The small problem constraints (m, n <= 8) make this approach feasible.

4. Complexity Analysis:
   - Time complexity: O(m! * n) - We explore m! permutations of mentor assignments. The compatibility calculation takes O(m^2 * n) which is dominated by the backtracking part if m is close to n.  If m is much smaller than n, then pre-calculation becomes the dominant factor.
   - Space complexity: O(m) - Due to the `used_mentors` array and the recursive call stack.  The `compatibility` matrix takes O(m^2), which can also be a significant factor.


## Topics
Array, Dynamic Programming, Backtracking, Bit Manipulation, Bitmask

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-03-28
