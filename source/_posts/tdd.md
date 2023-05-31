---
title: Test Driven DSA(Data Structrure & Algorithm)
tags: [dsa, tdd, unit testing, go]
date: 2023-05-31
---

Just like **Test Driven Development**, I use **Test Driven DSA** to solve LeetCode questions locally. In **Go**.

* You won't need a `func main()`
* Saves time by copying all the test cases at once and testing them all at the same time.
* Brings the `Run Testcases` button to your IDE
* You learn how to write tests in various situations.
* Makes debugging a specific test case easier!
**Here is an example:**
Folder structure:

```bash
ƛ tree                           
.
├── 1431.go
├── 1431_test.go
└── go.mod

0 directories, 3 files
```

**Main File:** `1431.go`

```go
package kidsWithCandies

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

**Test File:** `1431_test.go`

```go
package kidsWithCandies

import "testing"

type addTest struct {
// The name data structure can help you identify which testcase is failing if you are unable
// to match the testcase expected with the output. I don't use it since it consumes more time
// to write tests, and ultimately I need to pass all the tests.

//  name       string
 candy      []int
 extraCandy int
 expected   []bool
}

var addtests = []addTest{
 {[]int{2, 3, 5, 1, 3}, 3, []bool{true, true, true, false, true}},
 {[]int{4, 2, 1, 1, 2}, 1, []bool{true, false, false, false, false}},
 {[]int{12, 1, 12}, 10, []bool{true, false, true}},
}

func TestKidsWithCandies(t *testing.T) {
 for _, test := range addtests {
  output := kidsWithCandies(test.candy, test.extraCandy)
  for i, v := range test.expected {
   if v != output[i] {
    t.Errorf("Output: %t \t Expected: %t", output, test.expected)
    break
   }
  }
 }
}
```

```go
module kidsWithCandies

go 1.19
```

In the CLI, I just need to run `go test` and it will run all the given test cases  for that function.

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

I find this process to be easy convinced and learning. We can basically understand this as *brining/building* Leetcode (premium)features like debugging and aggregated testing to your IDE.
