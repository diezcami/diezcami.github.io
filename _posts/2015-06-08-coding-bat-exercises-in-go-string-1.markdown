---
layout: post
title: "CodingBat Exercises in Go: String-1"
date: 2015-06-08 02:55:16 +0800
--- 
String-1 provided opportunities for me to define functions inside a separate function, as well as create functions that returned multiple values. Other than that, the problems were predominantly solvable with language agnostic solutions. 

The problems below have been taken from [CodingBat's Python Exercises](http://codingbat.com/python), while all solutions were written by me. I've used `go fmt` and conducted tests for my codes, but please don't hold it against me if I've missed a few edge cases somewhere. All solutions are licensed under MIT.

### hello_name ###
Given a string name, e.g. "Bob", return a greeting of the form "Hello Bob!".

```
func hello_name(str string) string {
    return "Hello " + str + "!"
}
```

### make_abba ###
Given two strings, a and b, return the result of putting them together in the order abba, e.g. "Hi" and "Bye" returns "HiByeByeHi".

```
func make_abba(a, b string) string {
    return a + b + b + a
}
```


### make_tags ###
The web is built with HTML strings like "<i>Yay</i>" which draws Yay as italic text. In this example, the "i" tag makes <i> and </i> which surround the word "Yay". Given tag and word strings, create the HTML string with tags around the word, e.g. "<i>Yay</i>".

```
func make_tags(tag, word string) string {
    start := func(tag string) string {
        return "<" + tag + ">"
    }
    end := func(tag string) string {
        return "</" + tag + ">"
    }
    return start(tag) + word + end(tag)
}
```


<h3> make_out_word </h3>
Given an "out" string length 4, such as "<<>>", and a word, return a new string where the word is in the middle of the out string, e.g. "<<word>>".

```
func make_out_word(out, word string) string {
    return out[0:2] + word + out[2:]
}
```

### extra_end ###
Given a string, return a new string made of 3 copies of the last 2 chars of the original string. The string length will be at least 2.

```
func extra_end(str string) string {
    return str[len(str)-2:] + str[len(str)-2:] + str[len(str)-2:]
}
```

### first_two ###
Given a string, return the string made of its first two chars, so the String "Hello" yields "He". If the string is shorter than length 2, return whatever there is, so "X" yields "X", and the empty string "" yields the empty string "".

```
func first_two(str string) string {
    if len(str) < 2 {
        return str
    }

    return str[0:2]
}
```

### first_half ###
Given a string of even length, return the first half. So the string "WooHoo" yields "Woo".

```
func first_half(str string) string {
    return str[:len(str)/2]
}
```

### without_end ###
Given a string, return a version without the first and last char, so "Hello" yields "ell". The string length will be at least 2.

```
func without_end(str string) string {
    return str[1 : len(str)-1]
}
```

### combo_string ###
Given 2 strings, a and b, return a string of the form short+long+short, with the shorter string on the outside and the longer string on the inside. The strings will not be the same length, but they may be empty (length 0).

```
func combo_string(a, b string) string {
    compare_strings := func(a, b string) (string, string) {
        if len(a) < len(b) {
            return a, b
        }
        return b, a
    }

    short, long := compare_strings(a, b)

    return short + long + short
}
```

### non_start ###
Given 2 strings, return their concatenation, except omit the first char of each. The strings will be at least length 1.

```
func non_start(a, b string) string {
    return a[1:] + b[1:]
}
```

### left2 ###
Given a string, return a "rotated left 2" version where the first 2 chars are moved to the end. The string length will be at least 2.

```
func left2(str string) string {
    return str[2:] + str[:2]
}
```