---
title: Test Driven DSA(Data Structrure & Algorithm)
tags: [data structures & algorithms, leetcode, unit testing, go]
date: 2023-05-31
---

## Introduction

Just like **test-driven development**, you can use **test-driven DSA** to solve Leetcode(or any other platform) questions locally.
Similar to writing the test for a feature you want to implement, in test-driven DSA, you write the test for the solution function.

Every problem on websites like Leetcode comes with a basic [function signature](https://developer.mozilla.org/en-US/docs/Glossary/Signature/Function). Like:

```go
func kidsWithCandies(candies []int, extraCandies int) []bool { // Function Signature
    // Function Body
}
```

Using this signature and the sample test cases provided by the platform, you can write or generate tests for the solution.

The benefits of this are:

* You won't need a `func main()`.
* Saves time by copying and testing all the test cases at once.
* Faster results.
* Brings the `Run` button to your IDE
* Learn unit-testing.

## Why solve in Go?

One of the benefits of programming in Go is that you don't need to write the **test** for the problem. The [Go VSCode extension](https://marketplace.visualstudio.com/items?itemName=golang.Go) can generate a test function by using its signature. The only thing you are left with is adding the test cases, which can be populated by [GitHub Copilot](https://github.com/features/copilot) *(After filling in one test case from the platform, it automatically suggests the rest of them)*.

![Generate Test](https://code.visualstudio.com/assets/docs/languages/go/testcommands.png)

> Checkout my [repository](https://gitlab.com/jammutkarsh/dsa-in-go) to get an idea of how you can document and organise your solutions in a structured manner.

## Example

As an example, we are solving the [1431. Kids With the Greatest Number of Candies](https://leetcode.com/problems/kids-with-the-greatest-number-of-candies/) in [Go](https://go.dev/).

Start by creating some files in your *DSA* workspace. I prefer to choose the package name same as the function name and the file name same as the problem number.

```bash
# Init Go Modules
go mod init kidsWithCandies

# Create program and test files
touch 1431.go 1431_test.go
```

Your **folder structure** should look something like this:

```bash
ƛ tree                           
.
├── 1431.go
├── 1431_test.go
└── go.mod

0 directories, 3 files
```

The **main file:** i.e. `1431.go` which consists of the solution. This will be the same function that you submit on the platform.

*I have already solved the problem and written the solution.*

```go
package kidsWithCandies // you will copy everything as the solution, except this line.

func max(nums []int) (max int) {
 for i := 0; i < len(nums); i++ {
  if nums[i] > max {
   max = nums[i]
  }
 }
 return
}

func kidsWithCandies(candies []int, extraCandies int) []bool {
 maxCandies := max(candies)
 maxOrNot := make([]bool, len(candies))
 for i := 0; i < len(candies); i++ {
  if candies[i]+extraCandies >= maxCandies {
   maxOrNot[i] = true
  }
 }
 return maxOrNot
}
```

The **test file:** i.e. `1431_test.go` consists of the test cases.

> As a best practise, it is recommended to first write the test and then the actual feature.
> So, I suggest you to follow the same practise. First, write the test, then the solution.

```go
package kidsWithCandies

import (
 "reflect"
 "testing"
)

func TestKidsWithCandies(t *testing.T) {
 type args struct {
  candies      []int
  extraCandies int
 }
 tests := []struct {
  name string
  args args
  want []bool
 }{
  {"Leetcode Case 1", args{[]int{2, 3, 5, 1, 3}, 3}, []bool{true, true, true, false, true}},
  {"Leetcode Case 2", args{[]int{4, 2, 1, 1, 2}, 1}, []bool{true, false, false, false, false}},
  {"Leetcode Case 3", args{[]int{12, 1, 12}, 10}, []bool{true, false, true}},
 }
 for _, tt := range tests {
  t.Run(tt.name, func(t *testing.T) {
   if got := kidsWithCandies(tt.args.candies, tt.args.extraCandies); !reflect.DeepEqual(got, tt.want) {
    t.Errorf("kidsWithCandies() = %v, want %v", got, tt.want)
   }
  })
 }
}
```

**Module file:** `go.mod`

```go
module kidsWithCandies

go 1.19
```

In the CLI, you just need to run `go test`, an equivalent to `Run` on Leetcode and it will test for the given test cases.

```bash
# For a passing test
ƛ go test         
PASS
ok      kidsWithCandies 0.505s

# For a failing test
ƛ go test
--- FAIL: TestKidsWithCandies (0.00s)
    1431_test.go:22: Output: [false true true false true]        Expected: [true true true false true]
 # we can find which test is failing by uncommenting `name string`. For more info refer _test.go file. 
FAIL
exit status 1
FAIL    kidsWithCandies 0.460s
```

You can think of this as *brining/building* some of the [Leetcode Premium](https://leetcode.com/subscribe/) features like *Unlimited Playgrounds*, *Debugger*, *Autocomplete*, and *Lightning Judge,* to your IDE.

I find this process to be easy and convincing for learning, and I hope you do too.

In a future post, we will explore how you can write a bash script to automate file creation.

---
