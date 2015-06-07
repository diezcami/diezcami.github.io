---
layout: post
title: "C++ Pointers and References: An Overview"
date: 2015-05-08 11:33:15 +0800
---
References and pointers are usually, in one way or another, implemented in every programming language; higher level languages, however, most likely do not provide explicit access to them. As a result, they often come up implicitly in the form of garbage collection and simpler OOP conventions. On the other hand, languages that have more freedom at lower levels such as C/C++ allow users to explicitly use pointers and references to manually control several aspects of a program including, but not limited to memory management/allocation, OOP and ease of access. 

This guide is split into two parts - here, I'll be going through a basic overview on pointers and references understandable to anyone with knowledge on basic programming in any language and minor C++ syntax (mainly std, cout and endl).

## Pointers
Every declared variable in a program, whether primitive or not, is stored in memory and has its own memory address in the form of a hexadecimal number (0x). These variables are normally accessed by identifiers they've been declared with, paying no attention to its location in memory. To access the memory address of a variable in C++, we use the referencing operator `&`.

```
std::string foo = "foo";
std::cout << &foo << std::endl; // output: memory address of foo
```

A **Pointer** is a variable that holds a memory address. Its behavior is relatable to how entries in a table of contents contain page numbers or addresses that lead to actual content. It can be declared with or without being defined using `data_type *identifier`. To get the variable stored in a pointer, we use the dereferencing operator `*`. Note that the `*` being used as an operator and as part of a pointer's declaration are independent of each other.

```
int num = 10;
int *foo;
int bar*; 
std::cout << foo << std::endl; // output: 0x0 (null memory address)

foo = &num; 
std::cout << foo << std::endl; // output: memory address of num
std::cout << *foo << std::endl; //output: 10
```

Pointers are not limited to being assigned by memory addresses derived from the `&` operator - they can also be assigned with the memory addresses stored in other pointers. If a pointer is assigned to another pointer, any changes to the variable stored in the common memory address will reflect on the `*` operation of either pointer. This behavior is reminiscent of how objects are handled handled in Java; 

```
std::string qux = "Tempura";
std::string *foo, *bar;

foo = &qux;
bar = foo;
std::cout << *foo << std::endl; // output: Tempura
std::cout << *bar << std:: endl; // output: Tempura

qux = "Tonkatsu";
std::cout << *foo << std::endl; // output: Tonkatsu
std::cout << *bar << std:: endl; // output: Tonkatsu
```

The deferencing operator `*` can also be used at the left hand side of operations to replace the values stored in a pointer or memory address. The referencing operator `&`, however, cannot as it would not make sense to reallocate where a variable would be stored in memory. The following is a continuation of the code snippet above:

```
// Recall that foo = &qux
*foo = "Gyudon";
std::cout << qux << std::endl; // output: Gyudon
```

## Pointer Practices
When using pointers regardless of how simple its applications are, it's paramount to take caution in remembering where a pointer comes from and goes towards during assignments. Carelessness here will lead to dangling pointers and memory leaks, which can be detrimental to your program's performance at best, and your whole computer's at worst. As good practice, the two main points to remember when using pointers are the following:

* **Deallocating memory** used by an object a pointer points to using `delete pointer_to_obj` or `delete[] pointer_to_obj` after its usage to avoid memory leaks
* **Setting a pointer to `null`** after its usage to avoid dangling pointers

It's important to note that either `delete` function is actually interpreted as **delete the object stored in pointer (arg)**, which is entirely different from deleting the pointer itself. It's also important to note that either `delete` function only works on objects allocated with `new`. We use `delete` for variables that take up one block of space (eg. int, double, subclasses) and `delete[]` for array-based variables (eg. string, int[]). The following code snippet shows an example of inaccessible memory:

```
std::string *bar = new std::string;
*bar = "..";
std::cout << *bar << std::endl; 
bar = null;
```

In the example above, the string `..` was initialized at the memory address stored in the pointer `bar`. After pointing `bar` to null (as stated in the second point in the guideline), there's nothing left that points to the memory storing the string containing `..`, making it impossible to deallocate and forced to remain in the RAM throughout the whole duration of the program. These situations are called **Memory Leaks**, and can be remedied by following the first guideline as stated earlier as seen below:

```
std::string *bar = new std::string;
*bar = "..";
std::cout << *bar << std::endl; 
delete bar; // deletes the object pointed to by bar, not bar itself
bar = null
```

Another type of problem presented by mishandling pointers is the **Dangling Pointer**, which happens when an pointer points to a memory address that, at the time of accessing, has not been allocated. It's important to note that not being allocated is not equivalent to pointing to null. The following code snippet shows an example of a dangling pointer:

```
int *bar = new int(5);
delete bar;
```

Since the memory address stored in `bar` has been freed with `delete bar`, `bar` now points to a deallocated memory address. Dereferencing or assigning the address at this point may be unsafe and result in **undefined behavior**, so it's better to set `bar` to `null` to stay on the safer side of memory management.

```
int *bar = new int(5);
delete bar;
bar = 0;
std::cout << bar << std::endl; // Output: 0x0 (null)
```

Beyond the band-aid fix of setting a pointer to null, however, it would be better to modify the code in a way that there would be no need to set the pointer to null to begin with. 
Most examples here are trivial and meant to showcase pointer syntax above anything else. In reality, pointers can be used in OOP and to allocate memory in more resource-hungry programs to maximise their performance.
## References
A **Reference** holds another variable of the same declared type, and serves as its alias. Its behavior is relatable to how a person can (but may not) be referred to by multiple nicknames or aliases while maintaining one full name. It can be declared and must be defined using `data_type &identifier`. Similarly with `*`, note that the `&` used when declaring a reference is not the same as the referencing operator `&` used in the earlier examples. Unlike pointers, a reference cannot be null or re-assigned after being defined. 

```
std::string foo = "..";
std::string& bar = foo;

bool foobar = (foo==bar);
std::cout << foobar << std::endl; // output: 1
```

In a way, references work similarly to pointers with more limitations and are `const` in nature. The existence of references, however, is not fully redundant - operations involving references are generally safer than those involving pointers, and are usually used unless the situation demands functions exclusive to pointers (recall how pointers can be reassigned, while references cannot). References are also generally easier to use, as there's no need to keep track of dangling pointers or inaccessible memory. While I won't be going through the in-depth uses of references, I've written one instance that showcases their functionality and definition well.

```
void swap_val (int foo, int bar) {
    int qux = foo;
    foo = bar;
    bar = qux;
}
```

When the above function `swap_val (a, b)` is called in an external function, the parameters `foo` and `bar` are merely copies of the values stored in `a` and `b`. As a result, calling this function will not result in swapping the actual values of `a` and `b` outside the function. When this behaviour happens in a function, it's said that its parameters **pass by value**. In the alternative function below,

```
void swap_ref (int &foo, int &bar) {
    int qux = foo;
    foo = bar;
    bar = qux;
}
```

Notice that references are passed instead of actual `int` parameters. When `swap_ref (a, b)` is called, what's passed to the function are *references to a and b*, and not just copies of their values. When this behavior occurs, a function's parameters are said to **pass by value**. Now, when the function calls operations on references of `a` and `b`, they are actually called on the variables `a` and `b` passed as parameters as well. As a result,

```
int foo = 10;
int bar = 20;
swap_val (foo, bar);
std::cout << foo << std::endl; // Output: 10
std::cout << bar << std::endl; // Output: 20

swap_ref (foo, bar);
swap_val (foo, bar);
std::cout << foo << std::endl; // Output: 20
std::cout << bar << std::endl; // Output: 10  
```

References are normally inaccessible in languages that maintain high level functionalities (including Java), making the language **pass by value** as a whole by default. What's good about the availability of access to references in C++ is the option to pass parameters either by value or by reference to functions, resulting in more versatile ways to code.

##  Summary
Here's a list of the terminologies used throughout the article:

<table>
	<tr>
		<td width=24%><strong>TERM</strong></td>
		<td width=24%><strong>SAMPLE USAGE</strong></td>
		<td width=52%><strong>DEFINITION</strong></td>
	</tr>

	<tr>
		<td>Pointer</td>
		<td><code>int *foo</code></td>
		<td>A data type that stores a memory address</td>
	</tr>

	<tr>
		<td>Reference (noun)</td>
		<td><code>int &foo</code></td>
		<td>A data type that serves as an alias to another variable</td>

	</tr>

	<tr>
		<td>Reference (verb)</td>
		<td><code>&bar</code></td>
		<td>To get the address of a variable using the <code>&</code> operator</td>
	</tr>

	<tr>
		<td>Dereference</td>
		<td><code>*bar</code></td>
		<td>To get the object stored in a memory address or pointer with the <code>*</code> operator</td>
	</tr>

	<tr>
		<td>Allocate (verb)</td>
		<td><code>n/a</code></td>
		<td>To reserve memory for an object</td>
	</tr>

	<tr>
		<td>Deallocate (verb)</td>
		<td><code>*bar</code></td>
		<td>To make previously allocated memory available again</td>
	</tr>

	<tr>
		<td>Memory Leak</td>
		<td><code>n/a</code></td>
		<td>Result of memory addresses that can no longer be accessed and deallocated</td>
	</tr>

	<tr>
		<td>Dangling Pointers</td>
		<td><code>n/a</code></td>
		<td>Result of deallocating a memory address a pointer is pointing to</td>
	</tr>

	<tr>
		<td>Undefined Behavior</td>
		<td><code>n/a</code></td>
		<td>Result of illogical operations (eg. dereferencing a dangling pointer)</td>
	</tr>

	<tr>
		<td>Pass</td>
		<td><code>foo (a, b)</code></td>
		<td>Action taken on parameters used when calling a function</td>
	</tr>

	<tr>
		<td>Pass by Value</td>
		<td><code>void (int foo)</code></td>
		<td>Behavior in which functions operate on copies or clones of passed parameters</td>
	</tr>

	<tr>
		<td>Pass by Reference </td>
		<td><code>void (int &foo)</code></td>
		<td>Behavior in which functions operate on aliases leading to the passed parameters</td>
	</tr>

</table>

## Further Reading
There're a number of common applications for references and pointers that I did not cover in this entry - here's a small list of those:

* **Memory Management: Stacks and Heaps**: In short, normal declared variables are allocated to the stack while variables called with `new` and pointers are allocated in the heap. Reading up on this will allow you to have a better understanding of what happens on a lower level beyond the the code and how memory is managed through code.
* **Nesting (de)referencing operators**: It's possible to call data types such as `type **identifier` to create a pointer to a pointer, or to use combinations of `&` and `*` to create variable types that may eventually come in handy. Understanding how nested operators work will also provide a stronger foundation in C++ OOP than what's covered in this article.
* **Pointers and Arrays**: These two are closely related and reading up on them can explain the similarities in data types such as `char *` and `int *` when declaring an array or a pointer.
* **Parameters and Return Values**: Pointers and References, like any other variable, can be used as parameters and return values when implementing functions. You will likely encounter terms such as *pass by value* and *pass by reference*, which were introduced briefly earlier in this guide.
* **Smart Pointers**: More modern pointers that can be configured to or automatically delete pointers after a specified event. These, for the most part, get rid of the dangerous side of memory management that come with using regular pointers.