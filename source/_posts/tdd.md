---
title: Test Driven Leetcode (TDL)
tags: [data structures & algorithms, leetcode, unit testing]
date: 2023-12-23
---

![TDL](/images/TDL.png)

In this article, I want combine unit testing and Leetcode, to create a new way of solving Leetcode questions. I call it **Test Driven Leetcode** or **TDL** for short.

## Intro

You might have heard about [Test Driven Development(**TDD**)](https://en.wikipedia.org/wiki/Test-driven_development). It's a practice to write the test for the functionality first, before implementing it.  Some say it's stupid, while others say it's a good practice.

'*If you **100.00%** sure about what the output is going to be, then TDD is the way to go.*' is something I have concluded from all those opinions.

When solving a Leetcode question, you are in that **100.00% sure** spot. Leetcode, provides you the input and the output, you just need to figure out the path. Sounds familiar? Yes, it's the same as TDD.

## Pros

There are many obvious(*conscious*) & subtle(*unconscious*) benefits to this technique, but I will list the ones which I think are the most important:

1. You might not need a `func main()` to test your code locally.*^1*
2. Brings 5 out of 11 **Leetcode premium** feature to your IDE.
   1. [Debugging](https://leetcode.com/subscribe/#:~:text=your%20source%20code.-,Debugger,-Tired%20ofSystem)
   2. [Unlimited Playgrounds](https://leetcode.com/subscribe/#:~:text=Unlimited%20Playgrounds)
   3. [Cloud Storage](https://leetcode.com/subscribe/#:~:text=select%20items/content.-,Cloud%20Storage,-Code%20and%20layouts) *using GitHub/GitLab*
   4. [Autocomplete](https://leetcode.com/subscribe/#:~:text=from%20Google%20alone.-,Autocomplete,-Not%20interested%20in)
   5. [Lightning Judge](https://leetcode.com/subscribe/#:~:text=our%20code%20editor.-,Lightning%20Judge,-Tired%20of%20waiting)
3. As a *Junior Developer*, you could impress the interviewer by writing a unit test!*^2*

 *^1 In languages like C/C++, it's a little trivial to write a unit test, in those cases in my humble opinion is not worth it.*

 *^2 This actually happened to me in an interview. The questions were already written in a [GitHub Code Spaces](https://github.com/features/codespaces) like environment. But he was comfortable with me solving the question locally where I used this technique, and he explicitly said 'He has never seen someone solve algorithms question using a Unit Test'.*

> *Update 25/12/2023*
> Another benefit of using TDL, is you can see the code coverage of your solution. Using the coverage info, you can either add more test cases in your code or remove the parts of code that are not covered.
> In an interview, when the interviewer asks you, 'what happen if I remove this line of code?' the *code coverage will be there to save you*!

![Code Coverage](/images/codeCoverage.png)

NOTE: Full code coverage isn't achievable for all code segments, as some are essential to preserve language syntax and preventing compilation errors.

## How to do it?

So, here's how you do it. I will be using [Leetcode 509. Fibonacci Number](https://leetcode.com/problems/fibonacci-number/) as an example.

I have used the 3 most popular languages in Leetcode, Java, C++ and Python. I have also included Go, as it's the easiest to write a unit test in it, again in my humble opinion.

### Example in Go

**Code File:** `509.go`

```go
package fib

var recursionArray map[int]int

func fib(n int) int {
 if n <= 1 {
  return n
 }
 if recursionArray == nil {
  recursionArray = make(map[int]int)
 }
 if _, ok := recursionArray[n]; ok {
  return recursionArray[n]
 }
 recursionArray[n] = fib(n-1) + fib(n-2)
 return recursionArray[n]
}
```

**Test File:** `509_test.go`

```go
package fib

import "testing"

// Auto-Generated test using Go VSCode Extention.
func TestFib(t *testing.T) {
 type args struct {
  n int
 }
 tests := []struct {
  name string
  args args // for single inputs, replace the struct with the type
  want int
 }{// I usually write the first test, rest is given by GH copilot.
  {"Fib(0)", args{0}, 0},
  {"Fib(1)", args{1}, 1},
  {"Fib(4)", args{4}, 3},
  {"Fib(7)", args{7}, 13},
  
 }
 for _, tt := range tests {
  t.Run(tt.name, func(t *testing.T) {
   if got := fib(tt.args.n); got != tt.want {
    t.Errorf("Fib() = %v, want %v", got, tt.want)
   }
  })
 }
}
```

**Testing:**

```bash
# For a passing test
ƛ go test .
ok      gitlab.com/jammutkarsh/dsa-in-go/509    0.253s

# For a failing test
ƛ go test .
--- FAIL: TestFib (0.00s)
    --- FAIL: TestFib/Fib(0) (0.00s)
        509_test.go:23: Fib() = 0, want 1
FAIL
FAIL    gitlab.com/jammutkarsh/dsa-in-go/509    0.354s
FAIL
```

### Example in C++

This is the **^1** exception which I wanted to show.

**Code and Test file:** `509.cpp`

```cpp
#include <algorithm>
#include <functional>
#include <iostream>
#include <iterator>
#include <list>
#include <map>            // map and multimaps
#include <numeric>        // some numeric algorithm
#include <set>            // set and multisets
#include <unordered_map>  // unordered map and unordered multimap
#include <unordered_set>  // unordered set and unordered multisets
#include <vector>

using namespace std;

// Sometimes needed to convert a vector to a string for printing
string VectorToString(vector<int> input) {
    string str = "[";
    for (int i = 0; i < input.size(); i++) {
        str += to_string(input[i]);
        if (i != input.size() - 1) {
            str += ", ";
        }
    }
    str += "]";
    return str;
}

class Args {
   private:
    struct Parameters {
        int target;
    };

    struct Result {
        int result;
    };

   public:
    string TestCase;
    Parameters Input;
    Result Output;
    Args(string name, Parameters input, Result output) {
        TestCase = name;
        Input = input;
        Output = output;
    }
};

int Recursivefib(int n) {
    if (n <= 1) return n;
    return Recursivefib(n - 1) + Recursivefib(n - 2);
}

int main() {
    bool allPassing = false;

    vector<Args> args;
    args.push_back(Args("Test Case 1", {0}, {0}));
    args.push_back(Args("Test Case 2", {1}, {1}));
    args.push_back(Args("Test Case 3", {2}, {1}));
    args.push_back(Args("Test Case 4", {3}, {2}));
    args.push_back(Args("Test Case 5", {4}, {3}));
    args.push_back(Args("Test Case 5", {5}, {5}));
    args.push_back(Args("Test Case 5", {6}, {8}));

    for (int i = 0; i < args.size(); i++) {
        auto result = Recursivefib(args[i].Input.target);
        if (result != args[i].Output.result) {
            cout << "FAIL: " << args[i].TestCase << endl;
            cout << "EXPECTED: " << args[i].Output.result << endl;
            cout << "GOT: " << result << endl;
            allPassing = true;
        }
    }

    if (!allPassing) {
        cout << endl << "ok!" << endl;
        return 1;
    }

    return 0;
}
```

**Testing:**

```bash
# For a passing test
$ gpp 509.cpp

ok!

# For a failing test
$ gpp 509.cpp
FAIL: Test Case 4
EXPECTED: 2
GOT: 1
```

> `gpp` is a custom script that complies, runs, and deletes the code binary.

### Example in Python

**Code File:** `509.py`

```python
class Fibonacci:
    def fib(self, n: int) -> int:
        current_val = 0
        next_val = 1
        if n == 0:
            return current_val
        elif n == 1:
            return next_val
        else:
            for _ in range(2, n + 1):
                sum_val = current_val + next_val
                current_val = next_val
                next_val = sum_val
            return next_val

```

**Test File:** `test_503.py`

```python
import unittest
from fibonacci import Fibonacci

class TestFibonacci(unittest.TestCase):

    def setUp(self):
        self.fibonacci = Fibonacci()

    def test_fibonacci(self):
        test_cases = [
            (0, 0),
            (1, 1),
            (2, 1),
            (3, 2),
            (4, 3),
            (5, 5),
            (6, 8),
            # Add more test cases as needed
        ]

        for n, expected_output in test_cases:
            with self.subTest(n=n):
                result = self.fibonacci.fib(n)
                self.assertEqual(result, expected_output, f"fib({n}) should be {expected_output}, but got {result}")

if __name__ == '__main__':
    unittest.main()
```

**Testing:**

```bash
# For a passing test
$ python3 -m unittest test_503.py

# For a failing test
$ python3 -m unittest test_503.py
```

### Example in Java

Code File: `Fibonacci.java`

```java
public class Fibonacci {

    public int fib(int n) {
        int currentVal = 0;
        int nextVal = 1;

        if (n == 0) {
            return currentVal;
        } else if (n == 1) {
            return nextVal;
        } else {
            for (int i = 2; i <= n; i++) {
                int sum = currentVal + nextVal;
                currentVal = nextVal;
                nextVal = sum;
            }
            return nextVal;
        }
    }
}
```

**Test File:** `TestFibonacci.java`

```java
public class TestFibonacci {

    public static void main(String[] args) {
        testFibonacci();
    }

    public static void testFibonacci() {
        int[][] testCases = {
            {0, 0},
            {1, 1},
            {2, 1},
            {3, 2},
            {4, 3},
            {5, 5},
            {6, 8}
            // Add more test cases as needed
        };

        boolean allTestsPassed = true;

        for (int[] testCase : testCases) {
            int n = testCase[0];
            int expectedOutput = testCase[1];

            Fibonacci fibonacci = new Fibonacci();
            int result = fibonacci.fib(n);

            if (result != expectedOutput) {
                allTestsPassed = false;
                System.out.println("FAIL": n)
                System.out.println("EXPECTED: " + expectedOutput);
                System.out.println("GOT: " + result);
            }
        }
        if (allTestsPassed) {
            System.out.println("ok!");
        }
    }
}
```

**Testing:**

```bash
# Passing Test
$ javac Fibonacci.java TestFibonacci.java && java TestFibonacci
ok!

# Failing Test
javac Fibonacci.java TestFibonacci.java && java TestFibonacci
FAIL: 9
EXPECTED: 3
GOT: 34
```

## Cons

### Boilerplate Code

This might seem a little exhausting initially, writing up all the boilerplate code, then adding tests to it.

For this, I maintain a basic `0.cpp` file this includes the basic, based on question to question, I tweak it. Then I simply need to import the function signature, and let GitHub Copilot write test cases for me.

### Advanced Topics

In advanced topics, when there will be complex inputs and outputs, this might become very challenging. In those edge cases, you don't need to do this. Just use Leetcode directly.

If you still plan to use TDL, you might learn how a complex data structure is represented.

## Conclusion

Just like learning about Data Structures and Algorithm through Leetcode, makes you think once about the speed and space efficiency of a function in production code.
This technique could help your become a better developer. Because as Junior Developer myself, I think it's an effective way fundamentals of Software Development while solving Leetcode questions.

---
