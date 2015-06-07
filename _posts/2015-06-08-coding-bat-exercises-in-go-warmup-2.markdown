---
layout: post
title: "CodingBat Exercises in Go: Warmup-2"
date: 2015-06-08 02:02:32 +0800
--- 
Warmup-2 covers arrays, slices and control flow. Similarly to Warmup-1, the problems didn't call for any syntax features exclusive to Go; however, I still managed to learn several practices involving loops with blank variables and the `:=` operator.

The problems below have been taken from [CodingBat's Python Exercises](http://codingbat.com/python), while all solutions were written by me. I've used `go fmt` and conducted tests for my codes, but please don't hold it against me if I've missed a few edge cases somewhere. All solutions are licensed under MIT.

### string_times ###
Given a string and a non-negative int n, return a larger string that is n copies of the original string. 

```
func string_times(str string, n int) string {
    var temp string = ""
    for i := 0; i < n; i++ {
        temp += str
    }

    return temp
}
```

### front_times ###
Given a string and a non-negative int n, we'll say that the front of the string is the first 3 chars, or whatever is there if the string is less than length 3. Return n copies of the front;

```
func front_times(str string, n int) string {
    var temp string = ""
    for i := 0; i < n; i++ {
        if len(str) < 3 {
            temp += str
        } else {
            temp += str[0:3]
        }
    }

    return temp
}
```

### string_bits ###
Given a string, return a new string made of every other char starting with the first, so "Hello" yields "Hlo".

```
func string_bits(str string) string {
    var temp string = ""
    for i := 0; i < len(str); i++ {
        if i%2 == 0 {
            temp += str[i : i+1]
        }
    }

    return temp
}
```

### string_splosion ###
Given a non-empty string like "Code" return a string like "CCoCodCode".

```
func string_splosion(str string) string {
    var temp string = ""
    for i := 0; i < len(str); i++ {
        temp += str[0 : i+1]
    }

    return temp
}
```

### last2 ###
Given a string, return the count of the number of times that a substring length 2 appears in the string and also as the last 2 chars of the string, so "hixxxhi" yields 1 (we won't count the end substring).

```
func last2(str string) int {
    var count int = 0
    suffix := str[len(str)-2:]
    for i := 0; i < len(str)-2; i++ {
        if str[i:i+2] == suffix {
            count++
        }
    }

    return count
}
```

### array_count9 ###
Given an array of ints, return the number of 9's in the array.

```
func array_count9(nums []int) int {
    var count int = 0
    for _, val := range nums {
        if val == 9 {
            count++
        }
    }

    return count
}
```

### array_front9 ###
Given an array of ints, return True if one of the first 4 elements in the array is a 9. The array length may be less than 4.

```
func array_front9(nums []int) bool {
    var size int = int(math.Min(float64(len(nums)), 4))
    for i := 0; i < size; i++ {
        if nums[i] == 9 {
            return true
        }
    }

    return false
}
```

### array123 ###
Given an array of ints, return True if .. 1, 2, 3, .. appears in the array somewhere.

```
func array123(nums []int) bool {
    if len(nums) < 3 {
        return false
    }

    for i := 0; i < len(nums)-2; i++ {
        if nums[i] == 1 && nums[i+1] == 2 && nums[i+2] == 3 {
            return true
        }
    }

    return false
}
```

### string_match ###
Given 2 strings, a and b, return the number of the positions where they contain the same length 2 substring. So "xxcaazz" and "xxbaaz" yields 3, since the "xx", "aa", and "az" substrings appear in the same place in both strings.

```
func string_match(a, b string) int {
    var count int = 0
    for i := 0; i < int(math.Min(float64(len(a)), float64(len(b))))-1; i++ {
        if a[i] == b[i] && a[i+1] == b[i+1] {
            count++
        }
    }

    return count
}
```