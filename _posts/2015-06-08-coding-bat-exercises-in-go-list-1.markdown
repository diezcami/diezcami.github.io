---
layout: post
title: "CodingBat Exercises in Go: List-1"
date: 2015-06-08 16:06:25 +0800
--- 
List-2 covers array and slice manipulation. The solutions are mostly language agnostic, so there's nothing much to see if you're not entirely new to programming.

The problems below have been taken from [CodingBat's Python Exercises](http://codingbat.com/python), while all solutions were written by me. I've used `go fmt` and conducted tests for my codes, but please don't hold it against me if I've missed a few edge cases somewhere. All solutions are licensed under MIT.

### first_last6 ###
Given an array of ints, return True if 6 appears as either the first or last element in the array. The array will be length 1 or more.

```
func first_last6(nums []int) bool {
    return nums[0] == 6 || nums[len(nums)-1] == 6
}
```

<h3> same_first_last </h3>
Given an array of ints, return True if the array is length 1 or more, and the first element and the last element are equal.

```
func same_first_last(nums []int) bool {
    if len(nums) > 1 {
        return nums[0] == nums[len(nums)-1]
    }

    return false
}
```


### make_pi ###
Return an int array length 3 containing the first 3 digits of pi, {3, 1, 4}.

```
func make_pi() []int {
    return []int{3, 1, 4}
}
```


### common_end ###
Given 2 arrays of ints, a and b, return True if they have the same first element or they have the same last element. Both arrays will be length 1 or more.

```
func common_end(a, b []int) bool {
    return a[0] == b[0] || a[len(a)-1] == b[len(b)-1]
}
```


### sum3 ###
Given an array of ints length 3, return the sum of all the elements.

```
func sum3(nums []int) int {
    return nums[0] + nums[1] + nums[2]
}
```


### rotate_left3 ###
Given an array of ints length 3, return an array with the elements "rotated left" so {1, 2, 3} yields {2, 3, 1}.

```
func rotate_left3(nums []int) []int {
    return append(nums[2:3], nums[:2]...)
}
```


### reverse3 ###
Given an array of ints length 3, return a new array with the elements in reverse order, so {1, 2, 3} becomes {3, 2, 1}.

```
func reverse3(nums []int) []int {
    return []int{nums[2], nums[1], nums[0]}
}
```


### max_end3 ###
Given an array of ints length 3, figure out which is larger between the first and last elements in the array, and set all the other elements to be that value. Return the changed array.

```
func max_end3(nums []int) []int {
    max := int(math.Max(float64(nums[0]), float64(nums[2])))
    return []int{max, max, max}
}
```


### sum2 ###
Given an array of ints, return the sum of the first 2 elements in the array. If the array length is less than 2, just sum up the elements that exist, returning 0 if the array is length 0.

```
func sum2(nums []int) int {
    var count int = 0
    if len(nums) < 2 {
        for _, val := range nums {
            count += val
        }
        return count
    }

    return nums[0] + nums[2]
}
```


### middle_way ###
Given 2 int arrays, a and b, each length 3, return a new array length 2 containing their middle elements.

```
func middle_way(a, b []int) []int {
    return []int{a[1], b[1]}
}
```


### make_ends ###
Given an array of ints, return a new array length 2 containing the first and last elements from the original array. The original array will be length 1 or more.

```
func make_ends(nums []int) []int {
    return []int{nums[0], nums[len(nums)-1]}
}
```


### has23 ###
Given an int array length 2, return True if it contains a 2 or a 3.

```
func has23(nums []int) bool {
    for _, val := range nums {
        if val == 2 || val == 3 {
            return true
        }
    }
    return false
}
```



