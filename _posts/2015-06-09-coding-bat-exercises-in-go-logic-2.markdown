---
layout: post
title: "CodingBat Exercises in Go: Logic-2"
date: 2015-06-09 12:40:40 +0800
--- 
Logic-2 covers slightly more advanced program solving techniques. I've reached a certain peak of comfortability with Go at this point, and will no longer continue the CodingBat series on my blog. Thanks for tuning in, and I hope these codes have helped you in some way.

The problems below have been taken from [CodingBat's Python Exercises](http://codingbat.com/python), while all solutions were written by me. I've used `go fmt` and conducted tests for my codes, but please don't hold it against me if I've missed a few edge cases somewhere. All solutions are licensed under MIT.

### make_bricks ###
We want to make a row of bricks that is goal inches long. We have a number of small bricks (1 inch each) and big bricks (5 inches each). Return True if it is possible to make the goal by choosing from the given bricks.

```
func make_bricks(small, big, goal int) bool {

    if goal > 5*big+small {
        return false
    } else if goal%5 > small {
        return false
    } else {
        return true
    }
}
```

### lone_sum ###
Given 3 int values, a b c, return their sum. However, if one of the values is the same as another of the values, it does not count towards the sum.

```
func lone_sum(a, b, c int) int {
    if a == b && b == c {
        return 0
    } else if a == b {
        return c
    } else if b == c {
        return a
    } else if c == a {
        return b
    } else {
        return a + b + c
    }
}
```

### lucky_sum ###
Given 3 int values, a b c, return their sum. However, if one of the values is 13 then it does not count towards the sum and values to its right do not count. So for example, if b is 13, then both b and c do not count.

```
func lucky_sum(a, b, c int) int {
    if a == 13 {
        return 0
    } else if b == 13 {
        return a
    } else if c == 13 {
        return a + b
    } else {
        return a + b + c
    }
}
```

<h3> no_teen_sum </h3>
Given 3 int values, a b c, return their sum. However, if any of the values is a teen -- in the range 13..19 inclusive -- then that value counts as 0, except 15 and 16 do not count as a teens.

```
func no_teen_sum(a, b, c int) int {
    fix_teen := func(num int) int {
        if num == 15 || num == 16 {
            return num
        } else if num >= 13 && num <= 19 {
            return 0
        } else {
            return num
        }
    }

    return fix_teen(a) + fix_teen(b) + fix_teen(c)
}
```

### round_sum ###
For this problem, we'll round an int value up to the next multiple of 10 if its rightmost digit is 5 or more, so 15 rounds up to 20. Alternately, round down to the previous multiple of 10 if its rightmost digit is less than 5, so 12 rounds down to 10. Given 3 ints, a b c, return the sum of their rounded values.

```
func round_sum(a, b, c int) int {
    round10 := func(num int) int {
        if num%10 >= 5 {
            return num + (10 - num%10)
        }

        return num - (num % 10)
    }

    return round10(a) + round10(b) + round10(c)
}
```

### close_far ###
Given three ints, a b c, return True if one of b or c is "close" (differing from a by at most 1), while the other is "far", differing from both other values by 2 or more.

```
func close_far(a, b, c int) bool {
    iabs := func(num int) int {
        return int(math.Abs(float64(num)))
    }
    is_close := func(foo, bar int) bool {
        return iabs(foo-bar) <= 1
    }

    return (is_close(a, b) && !is_close(a, c) || is_close(a, c) && !is_close(a, b)) && !is_close(b, c)
}
```

### make_chocolate ###
We want make a package of goal kilos of chocolate. We have small bars (1 kilo each) and big bars (5 kilos each). Return the number of small bars to use, assuming we always use big bars before small bars. Return -1 if it can't be done.

```
func make_chocolate(small, big, goal int) int {
    if small >= goal%5 {
        if (big * 5) > (goal - goal%5) {
            return goal % 5
        }
        goal -= big * 5
        if small >= goal {
            return goal
        }
    }

    return -1
}
```

