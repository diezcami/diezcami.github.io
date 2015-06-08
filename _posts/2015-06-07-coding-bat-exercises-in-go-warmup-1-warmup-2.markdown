---
layout: post
title: "CodingBat Exercises in Go: Warmup-1, Warmup-2"
date: 2015-06-07 14:38:16 +0800
--- 
I've learned a number of languages this summer, but Go/Golang stood out as its structure was different compared to the likes of Java/C++. Learning it felt very counter intuitive, as concepts as fundamental as method signatures and variable declarations felt backwards (literally) and foreign. I've been burnt out trying to absorb everything about Go and its features lately, so I thought it'd be a good idea to start from scratch using CodingBat exercises.

The problems below have been taken from [CodingBat's Python Exercises](http://codingbat.com/python), while all solutions were written by me. I've used `go fmt` and conducted tests for my codes, but please don't hold it against me if I've missed a few edge cases somewhere. All solutions are licensed under MIT.
<hr style="margin-bottom: -10px">
# Warmup-1 #
Warmup-1 was as basic as I expected it to be - I didn't find myself wanting to use syntax features exclusive to Go or needing to refer to package API's. I managed to familiarize myself with how string manipulation works in Go (it's similar to Python, with understandably less magic) and the limitations of the built-in `math` library. Above all, I managed to get used to the backwards syntax of variable declaration and method signatures.



### sleep_in ###
The parameter weekday is True if it is a weekday, and the parameter vacation is True if we are on vacation. We sleep in if it is not a weekday or we're on vacation. Return True if we sleep in.

```
func sleep_in(weekday, vacation bool) bool {
    if vacation {
        return true
    }
    return !weekday
}
```

### monkey_trouble ###
We have two monkeys, a and b, and the parameters a_smile and b_smile indicate if each is smiling. We are in trouble if they are both smiling or if neither of them is smiling. Return True if we are in trouble.

```
func monkey_trouble(a_smile, b_smile bool) bool {
    return a_smile && b_smile || !a_smile && !b_smile
}
```

### sum_double ###
Given two int values, return their sum. Unless the two values are the same, then return double their sum.

```
func sum_double(a, b int) int {
    if a == b {
        return 4 * a
    }
    return a + b
}
```

### diff21 ###
Given an int n, return the absolute difference between n and 21, except return double the absolute difference if n is over 21.

```
func diff21(n int) int {
    if n > 21 {
        return 2 * (n - 21)
    }
    return int(math.Abs(float64(n - 21)))
}
```

### parrot_trouble ###
We have a loud talking parrot. The "hour" parameter is the current hour time in the range 0..23. We are in trouble if the parrot is talking and the hour is before 7 or after 20. Return True if we are in trouble.

```
func parrot_trouble(talking bool, hour int) bool {
    return talking && (hour < 7 || hour > 20)
}
```

### makes10 ###
Given 2 ints, a and b, return True if one if them is 10 or if their sum is 10.

```
func makes10(a, b int) bool {
    return a == 10 || b == 10 || a+b == 10
}
```

### near_hundred ###
Given an int n, return True if it is within 10 of 100 or 200. Note: abs(num) computes the absolute value of a number.

```
func near_hundred(n int) bool {
    return math.Abs(float64(100-n)) <= 10 || math.Abs(float64(200-n)) <= 10
}
```

### pos_neg ###
Given 2 int values, return True if one is negative and one is positive. Except if the parameter "negative" is True, then return True only if both are negative.

```
func pos_neg(a, b int, negative bool) bool {
    if negative {
        return a < 0 && b < 0
    }
    return (a < 0) != (b < 0)
}
```

### not_string ###
Given a string, return a new string where "not " has been added to the front. However, if the string already begins with "not", return the string unchanged.

```
func not_string(str string) string {
    if strings.HasPrefix(str, "not") {
        return str
    }
    return "not " + str
}
```

### missing_char ###
Given a non-empty string and an int n, return a new string where the char at index n has been removed. The value of n will be a valid index of a char in the original string (i.e. n will be in the range 0..len(str)-1 inclusive).

```
func missing_char(str string, n int) string {
    return str[0:n] + str[n+1:]
}
```

### front3 ###
Given a string, we'll say that the front is the first 3 chars of the string. If the string length is less than 3, the front is whatever is there. Return a new string which is 3 copies of the front.

```
func front3(str string) string {
    if len(str) < 3 {
        return str + str + str
    }
    return str[0:3] + str[0:3] + str[0:3]
}
```

<hr style="margin-bottom: 5px; margin-top: 27px">
# Warmup-2 #
Warmup-2 covers arrays, slices and control flow. Similarly to Warmup-1, the problems didn't call for any syntax features exclusive to Go; however, I still managed to learn several practices involving loops with blank variables and the `:=` operator.



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