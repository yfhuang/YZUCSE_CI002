# On-Site Examination Code Evaluation Prompt

This Markdown file provides reusable AI prompts for students to review and improve their UVa/CPE-style on-site examination code.

## Full Prompt for Evaluating My On-Site Examination Code

```markdown
I am practicing for an on-site programming examination using UVa/CPE-style problems. 

The overall problem set can be found here:  
https://github.com/yfhuang/YZUCSE_CI002/blob/main/Problems.md


Please help me review my code carefully and guide me to understand the weaknesses in my current solution.

## Problem Information

- Problem ID:
- Problem Title:
- Topic / Data Structure:
- Time limit:
- My expected difficulty:
  - [ ] Easy
  - [ ] Medium
  - [ ] Hard
- My current status:
  - [ ] Accepted
  - [ ] Wrong Answer
  - [ ] Runtime Error
  - [ ] Time Limit Exceeded
  - [ ] Compile Error
  - [ ] Not submitted yet

## Problem Summary

Briefly describe the problem in my own words:

```text
[Write your understanding of the problem here.]
```

## My Algorithm Idea

Describe my current solution idea:

```text
[Write your algorithm idea here.]
```

## My Code

```cpp
// Paste your full code here
```

## Please Evaluate My Code From These Perspectives

### 1. Problem Understanding

Check whether my interpretation of the problem is correct.

Please identify:

- Any misunderstanding of the problem statement
- Any misunderstanding of the input format
- Any misunderstanding of the output format
- Any missing special cases
- Whether my algorithm matches the problem requirements

### 2. Input / Output Handling

Check whether my code correctly handles:

- Single test case or multiple test cases
- Input until EOF
- Blank lines, spaces, or mixed-format input
- Required output format
- Case numbering, if required
- Extra spaces or missing newlines in the output

### 3. Algorithm Correctness

Check whether my logic is correct.

Please explain:

- What my code is trying to do
- Whether the main logic is valid
- Where the logic may fail
- Whether the solution handles all important cases
- Whether the algorithm is too simple, incomplete, or overcomplicated

### 4. Data Structure Usage

Check whether my selected data structure is appropriate.

Please comment on:

- Array, vector, stack, queue, set, map, or other STL usage
- Whether the container size is safe
- Whether the indexing is correct
- Whether there is any risk of out-of-bound access
- Whether another STL container could simplify the solution

### 5. Boundary Cases

Please test my code mentally using boundary cases, such as:

- Minimum input
- Maximum input
- Repeated values
- Empty, zero, or one-element cases
- Special cases mentioned in the problem statement
- Cases that may cause Wrong Answer
- Cases that may cause Runtime Error or Infinite Loop

### 6. Common C++ Programming Issues

Please check for:

- Uninitialized variables
- Array out-of-bound errors
- Infinite loops
- Incorrect loop conditions
- Incorrect use of `cin`, `getline`, or mixed input
- Integer overflow
- Missing `return` value in functions
- Incorrect variable reuse
- Confusing variable names
- Unnecessary or unreachable code

### 7. Time and Space Complexity

Please estimate:


- Time complexity
- Space complexity
- Whether the code is efficient enough for UVa/CPE constraints
- Whether there is a simpler or more efficient approach

### 8. Improvement Suggestions

Please provide suggestions in three levels:

#### Minimal Fix

Only fix the necessary bugs while keeping my original structure.

#### Cleaner Version

Rewrite the code in a clearer and more readable style.

#### Teaching Explanation

Explain the key concept in a way suitable for a beginner C++ student.

## Output Format

Please organize your review using the following structure:

1. Overall Judgment
2. Main Weaknesses
3. Possible Wrong Answer Cases
4. Minimal Corrected Code
5. Cleaner Reference Code
6. Key Learning Points
7. Suggestions for Future On-Site Examinations
```
