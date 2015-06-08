---
layout: post
title: "CodingBat Exercises in Go: Logic-1"
date: 2015-06-08 18:43:49 +0800
--- 
Logic-1 covers control flow. I implemented some of Go's syntax features in my solutions whenever possible, namely functions within functions and if statements with `;` operators.

The problems below have been taken from [CodingBat's Python Exercises](http://codingbat.com/python), while all solutions were written by me. I've used `go fmt` and conducted tests for my codes, but please don't hold it against me if I've missed a few edge cases somewhere. All solutions are licensed under MIT.

### cigar_party ###
When squirrels get together for a party, they like to have cigars. A squirrel party is successful when the number of cigars is between 40 and 60, inclusive. Unless it is the weekend, in which case there is no upper bound on the number of cigars. Return True if the party with the given values is successful, or False otherwise.

```
func cigar_party(cigars int, is_weekend bool) bool {
    if is_weekend {
        return cigars >= 40
    }

    return cigars >= 40 && cigars <= 60
}
```

### date_fashion ###
You and your date are trying to get a table at a restaurant. The parameter "you" is the stylishness of your clothes, in the range 0..10, and "date" is the stylishness of your date's clothes. The result getting the table is encoded as an int value with 0=no, 1=maybe, 2=yes. If either of you is very stylish, 8 or more, then the result is 2 (yes). With the exception that if either of you has style of 2 or less, then the result is 0 (no). Otherwise the result is 1 (maybe).

```
func date_fashion(you int, date int) int {
    if you <= 2 || date <= 2 {
        return 0
    } else if you >= 8 || date >= 8 {
        return 2
    }

    return 1
}
```

### squirrel_play ###
The squirrels in Palo Alto spend most of the day playing. In particular, they play if the temperature is between 60 and 90 (inclusive). Unless it is summer, then the upper limit is 100 instead of 90. Given an int temperature and a boolean is_summer, return True if the squirrels play and False otherwise.

```
func squirrel_play(temp int, is_summer bool) bool {
    if is_summer {
        return temp >= 60 && temp <= 100
    }

    return temp >= 60 && temp <= 90
}
```

### caught_speeding ###
You are driving a little too fast, and a police officer stops you. Write code to compute the result, encoded as an int value: 0=no ticket, 1=small ticket, 2=big ticket. If speed is 60 or less, the result is 0. If speed is between 61 and 80 inclusive, the result is 1. If speed is 81 or more, the result is 2. Unless it is your birthday -- on that day, your speed can be 5 higher in all cases.

```
func caught_speeding(speed int, is_birthday bool) int {
    birthday_calculate := func(speed int) int {
        if speed >= 66 && speed <= 85 {
            return 1
        } else if speed >= 85 {
            return 2
        }

        return 0
    }

    normal_calculate := func(speed int) int {
        if speed >= 61 && speed <= 80 {
            return 1
        } else if speed >= 80 {
            return 2
        }
        return 0
    }

    if is_birthday {
        return birthday_calculate(speed)
    }

    return normal_calculate(speed)
}
```

### sorta_sum ###
Given 2 ints, a and b, return their sum. However, sums in the range 10..19 inclusive, are forbidden, so in that case just return 20.

```
func sorta_sum(a, b int) int {
    if sum := a + b; sum >= 10 && sum <= 19 {
        return 20
    }

    return a + b
}
```

### alarm_clock ###
Given a day of the week encoded as 0=Sun, 1=Mon, 2=Tue, ...6=Sat, and a boolean indicating if we are on vacation, return a string of the form "7:00" indicating when the alarm clock should ring. Weekdays, the alarm should be "7:00" and on the weekend it should be "10:00". Unless we are on vacation -- then on weekdays it should be "10:00" and weekends it should be "off".

```
func alarm_clock(day int, vacation bool) string {
    vacation_alarm := func(day int) string {
        if day == 0 || day == 6 {
            return "off"
        }
        return "10:00"
    }

    regular_alarm := func(day int) string {
        if day == 0 || day == 6 {
            return "10:00"
        }
        return "7:00"
    }

    if vacation {
        return vacation_alarm(day)
    }

    return regular_alarm(day)
}
```

### love6 ###
The number 6 is a truly great number. Given two int values, a and b, return True if either one is 6. Or if their sum or difference is 6.

```
func love6(a, b int) bool {
    diff := func(a, b int) bool {
        return int(math.Abs(float64(a-b))) == 6
    }
    return a == 6 || b == 6 || a+b == 6 || diff(a, b)
}
```

### in1to10 ###
Given a number n, return True if n is in the range 1..10, inclusive. Unless "outside_mode" is True, in which case return True if the number is less or equal to 1, or greater or equal to 10.

```
func in1to10(n int, outside_mode bool) bool {
    in_range := func(n int) bool {
        return n >= 1 && n <= 10
    }

    if outside_mode {
        return !in_range(n)
    }

    return in_range(n)
}
```

### near_ten ###
Given a non-negative number "num", return True if num is within 2 of a multiple of 10. Note: (a % b) is the remainder of dividing a by b, so (7 % 5) is 2.

```
func near_ten(num int) bool {
    return num%10 <= 2 || num%10 >= 8
}
```