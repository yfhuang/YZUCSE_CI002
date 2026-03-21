# Supplement 01: UVa Input Patterns

This supplement reviews the UVa problems referenced in [Problems.md](../Problems.md), [CPE One-Star Problem List](../CPE/CPEoneStar.md), and [CPE Exam History](../CPE/CPEHistory.md). The goal is not to memorize every problem statement. The goal is to recognize the input format quickly and choose the correct C++ reading strategy.

## Core Idea

When you read a UVa problem, identify these four things first:

1. What is the stopping condition: EOF, a test count `T`, or a sentinel such as `0`, `0 0`, `#`, or `0000`?
2. What is the reading unit: token, full line, block, or grid?
3. Are spaces important?
4. Should the value be stored as `int`, `long long`, `double`, or `string`?

Across the UVa problems used in this course, most inputs can be grouped into the patterns below.

## Quick Summary

| Input Type | Typical Signal | Representative UVa Problems | Preferred C++ Solution |
|---|---|---|---|
| Fixed-size tokens until EOF | No `T`, no sentinel, same token count repeats | UVa 100, 10055, 10071, 10221, 10242 | `while (cin >> ...)` |
| `T` test cases | First value is the number of cases | UVa 10783, 10050, 12503, 10908, 11349 | `cin >> T; while (T--)` |
| Sentinel-terminated input | Stop at `0`, `0 0`, `#`, `0000`, or similar | UVa 12149, 11461, 11332, 10189, 1203 | `while (cin >> ... && condition)` |
| Pure line-based text | Spaces and punctuation must be preserved | UVa 272, 483, 10082, 10222, 494 | `while (getline(cin, line))` |
| Token header plus full lines | Read a number first, then switch to `getline` | UVa 10008, 10226, 10142, 10188, 482 | `cin.ignore(...); getline(...)` |
| Grid or matrix input | Dimensions followed by rows or cells | UVa 10189, 10908, 541, 815, 11349 | Nested loops with `vector<string>` or `vector<vector<int>>` |
| Command stream or simulation input | Commands follow a setup section | UVa 12503, 118, 10409, 380, 1203 | Parse commands, store history/state |
| Numeric text read as strings | Numbers are too large or format-sensitive | UVa 10929, 10093, 10106, 11344, 10101 | Read into `string` |

## 1. Fixed-Size Tokens Until EOF

### Pattern

Each case contains the same number of values, and the input ends only at EOF.

### Typical examples

- UVa 100 - The 3n + 1 Problem
- UVa 10055 - Hashmat the Brave Warrior
- UVa 10071 - Back to High School Physics
- UVa 10221 - Satellites
- UVa 10242 - Fourth Point!!

### Reading strategy

Use `while (cin >> ...)` and process one case immediately.

```cpp
int a, b;
while (cin >> a >> b) {
	// solve one case
}
```

### Why this works

- EOF is the only stopping condition.
- No extra blank lines need special handling.
- This is the most common UVa token-based pattern.

## 2. `T` Test Cases

### Pattern

The first value tells you how many cases follow.

### Typical examples

- UVa 10783 - Odd Sum
- UVa 10050 - Hartals
- UVa 12503 - Robot Instructions
- UVa 10908 - Largest Square
- UVa 11349 - Symmetric Matrix

### Reading strategy

Read `T` first, then loop exactly `T` times.

```cpp
int T;
cin >> T;
for (int caseIndex = 1; caseIndex <= T; ++caseIndex) {
	// read one test case
	// solve and print
}
```

### Why this works

- The judge guarantees the number of cases.
- You do not need EOF or sentinel logic inside the main loop.
- Many UVa problems also require `Case X:` style output with this format.

## 3. Sentinel-Terminated Input

### Pattern

Input continues until a special value appears.

### Typical examples

- UVa 12149 - Feynman (`0` ends input)
- UVa 11461 - Square Numbers (`0 0` ends input)
- UVa 11332 - Summing Digits (`0` ends input)
- UVa 10189 - Minesweeper (`0 0` ends input)
- UVa 1203 - Argus (`#` ends registration section)

### Reading strategy

Put the stopping rule directly in the loop condition.

```cpp
int n;
while (cin >> n && n != 0) {
	// solve one case
}
```

```cpp
int a, b;
while (cin >> a >> b && (a != 0 || b != 0)) {
	// solve one case
}
```

### Why this works

- The sentinel belongs to the input format, not the algorithm.
- The sentinel case is not processed.
- This style keeps the code short and safe.

## 4. Pure Line-Based Text Until EOF

### Pattern

Spaces, punctuation, or line structure matter, so token-based reading is not enough.

### Typical examples

- UVa 272 - TeX Quotes
- UVa 483 - Word Scramble
- UVa 10082 - WERTYU
- UVa 10222 - Decode the Mad man
- UVa 494 - Kindergarten Counting Game

### Reading strategy

Use `getline` for every line.

```cpp
string line;
while (getline(cin, line)) {
	// process the full line
}
```

### Why this works

- Spaces must be preserved.
- Some lines may even be empty.
- `cin >>` would lose important formatting information.

## 5. Token Header Plus Full Lines

### Pattern

The input begins with one or more numbers, then the real content is stored line by line.

### Typical examples

- UVa 10008 - What's Cryptanalysis?
- UVa 10226 - Hardwood Species
- UVa 10142 - Australian Voting
- UVa 10188 - Automated Judge Script
- UVa 482 - Permutation Arrays

### Reading strategy

After `cin >> ...`, consume the leftover newline before calling `getline`.

```cpp
#include <limits>

int T;
cin >> T;
cin.ignore(numeric_limits<streamsize>::max(), '\n');

string line;
for (int caseIndex = 0; caseIndex < T; ++caseIndex) {
	getline(cin, line);
	// process line-based content
}
```

### Why this works

- `cin >>` leaves a newline in the buffer.
- If you call `getline` immediately without `ignore`, the first line may be read as empty by mistake.

## 6. Grid or Matrix Input

### Pattern

The input gives dimensions first, then rows of characters or numbers.

### Typical examples

- UVa 10189 - Minesweeper
- UVa 10908 - Largest Square
- UVa 541 - Error Correction
- UVa 815 - Flooded!
- UVa 11349 - Symmetric Matrix

### Reading strategy

Read dimensions first, then read rows using nested loops.

```cpp
int rows, cols;
cin >> rows >> cols;

vector<string> grid(rows);
for (int i = 0; i < rows; ++i) {
	cin >> grid[i];
}
```

```cpp
int n;
cin >> n;
vector<vector<int>> matrix(n, vector<int>(n));
for (int i = 0; i < n; ++i) {
	for (int j = 0; j < n; ++j) {
		cin >> matrix[i][j];
	}
}
```

### Why this works

- The dimension header tells you exactly how much input to read.
- It prevents under-reading or over-reading.
- This pattern is common in simulation, matrix, and geometry problems.

## 7. Blank-Line Separated Blocks

### Pattern

One test case may contain many lines, and blank lines separate cases.

### Typical examples

- UVa 10226 - Hardwood Species
- UVa 10142 - Australian Voting
- UVa 482 - Permutation Arrays

### Reading strategy

Use `getline`, skip optional blank lines, and collect lines until the next blank line.

```cpp
int T;
cin >> T;
cin.ignore(numeric_limits<streamsize>::max(), '\n');

string line;
getline(cin, line); // consume the blank line after T if it exists

for (int caseIndex = 0; caseIndex < T; ++caseIndex) {
	vector<string> block;
	while (getline(cin, line) && !line.empty()) {
		block.push_back(line);
	}
	// solve one block
}
```

### Why this works

- The blank line is part of the input structure.
- You must separate cases without losing the final block.

## 8. Command Stream or Stateful Simulation

### Pattern

After the setup data, the input contains instructions, commands, or operations that must be executed in order.

### Typical examples

- UVa 12503 - Robot Instructions
- UVa 118 - Mutant Flatworld Explorers
- UVa 10409 - Die Game
- UVa 380 - Call Forwarding
- UVa 1203 - Argus

### Reading strategy

Read commands one by one, parse the command word, and keep enough state to replay or apply them.

```cpp
int n;
cin >> n;

vector<string> history(n + 1);
for (int i = 1; i <= n; ++i) {
	string command;
	cin >> command;

	if (command == "LEFT" || command == "RIGHT") {
		history[i] = command;
	} else {
		string sameAs;
		int index;
		cin >> sameAs >> index; // SAME AS k
		history[i] = history[index];
	}
}
```

### Why this works

- The input is not just data; it also encodes actions.
- You often need arrays, maps, or queues to remember previous commands.

## 9. Numeric Text That Should Be Read as Strings

### Pattern

The input looks numeric, but using integer types is risky or unnecessary.

### Typical examples

- UVa 10929 - You can say 11
- UVa 10093 - An Easy Problem!
- UVa 10106 - Product
- UVa 11344 - The Huge One
- UVa 10101 - Bangla Numbers

### Reading strategy

Read the value as a string and process digit by digit.

```cpp
string s;
while (cin >> s) {
	// process digits in s
}
```

### Why this works

- The number may be too large for built-in integer types.
- Sometimes the original digit sequence matters more than the numeric value.

## How to Choose the Correct Input Method Quickly

Use this checklist when you see a new UVa problem:

1. If the first token is the number of cases, use the `T`-based pattern.
2. If the input ends with `0`, `0 0`, `#`, or another special marker, use the sentinel pattern.
3. If spaces must be preserved, use `getline`.
4. If dimensions appear first, expect a grid or matrix.
5. If a number is followed by many text lines, mix `cin` and `getline` carefully.
6. If the value is too large or format-sensitive, read it as `string`.

## Common Input Mistakes in UVa

- Mixing `cin >>` and `getline` without calling `cin.ignore(...)`.
- Forgetting to reset arrays, counters, or vectors for each test case.
- Treating a sentinel value as real data.
- Assuming every text line has the same length. This is especially dangerous in UVa 490.
- Using `int` when the problem really needs `long long`, `double`, or `string`.
- Printing extra blank lines when the judge expects exact formatting.

## Final Reminder

For UVa, input handling is often half of the problem. Before writing the algorithm, classify the input first. Once you know whether the problem is based on EOF, `T`, sentinel values, full lines, grids, or command streams, the implementation becomes much more predictable.
