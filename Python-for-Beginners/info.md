1- Introduction

0 Hello World
Question:
Hello, World
The phrase Hello, world! is a special phrase in programming. In 1972 Brian Kernighan, a computer scientist, wrote a tutorial for the B programming language using this phrase. He later helped create the C programming language.

For most programmers, writing a program that prints Hello, world! is the first program they write when learning code.

Challenge
To follow this tradition, we will start with the "Hello, World!" program. On the right, you will see a code editor with the following code:

print("")
Inside of the double quotes, type out the following text:

Hello, world!
After you're done, click the Submit button.

Hint: Capitalization and punctuation matter! Make sure to type the phrase exactly as shown.


What is this course?
This course will teach you the core concepts of programming using Python. To view all the topics we will cover click the Python for Beginners button in the navbar above.

You can also navigate between lessons with the left and right arrow buttons in the navbar above.


What does print("") mean?
In Python, print() is a built-in function used to display output to the console. We will learn more about functions later on in the course. For now you can use it to print text, variables, or the result of expressions to the console.

Most programming languages have the equivalent of print() to display output. For example, in JavaScript, you would use console.log().

The console is a text-based interface that allows you to interact with a computer. It is a common tool used by developers to debug their code. In this course, we are actually executing your code on our own server and sending the console output back to you.

Starter code:
print("")

Solution:
print("Hello, world!")



1 What is Python
Question:
What is Python?
Python is an interpreted programming language. It was created by Guido van Rossum and first released in 1991. Python is known for its simplicity and readability, which makes it a great language for beginners.

Python is one of the most popular languages in the world. It is often the preferred language when automating tasks via scripts. It is also widely used in scientific computing, data science, machine learning, and backend web development.

This course will teach you the core concepts of Python. But if you're a beginner, the most important thing you will learn is how to think like a programmer.

Challenge
You can click the Submit button to execute the code on the right. Don't worry if you don't understand any of it.

You will notice that the output is incorrect. We want to calculate the first 20 digits of pi, but right now our program is only printing the first 19 digits. With the power of programming we can fix this by changing a single line of code.

To fix this, find the following line of code:

n = 19
and change the number to 20. Then click the Submit button again.

Hint: If you don't want to read through the code, click the editor and press Ctrl + F. You can then type "n = 19" to find the line of code you need to change.


What is an interpreted programming language?

An interpreted programming language is different from a compiled language. In a compiled language, the code is translated into machine code before it is run. In an interpreted language, the code is executed line by line by an interpreter, usually written in another language. This makes it easier to write and test code, but it can be slower than compiled languages.

It's okay if you don't understand all of this yet. If you're a beginner learning Python as your first language, the distinction between interpreted and compiled languages is not important for now.


What is a script?

A script is a file that contains a series of commands that are executed by a computer. Scripts are often used to automate repetitive tasks, such as renaming files, moving files, or processing data. Python is often used to write scripts because of its simplicity and readability.

Technically, any program that is written in a scripting language is a script. However, the term is often used to refer to small programs that automate tasks on a computer. The terms "scripting language" and "interpreted language" are often used interchangeably. They are technically different, but the distinction is rarely important.

Starter Code:
from decimal import Decimal, getcontext

def calculate_pi(n):
    getcontext().prec = n + 2  # Set precision higher than needed for accuracy
    
    C = 426880 * Decimal(10005).sqrt()
    K = 6
    M = 1
    X = 1
    L = 13591409
    S = L
    
    for i in range(1, n):
        M = (K ** 3 - 16 * K) * M // i ** 3
        L += 545140134
        X *= -262537412640768000
        S += Decimal(M * L) / X
        K += 12
    
    pi = C / S
    return str(pi)[:n + 2]  # Return first n digits plus the '3.'

n = 19
pi_digits = calculate_pi(n)
print(pi_digits)


Solution:
from decimal import Decimal, getcontext

def calculate_pi(n):
    getcontext().prec = n + 2  # Set precision higher than needed for accuracy
    
    C = 426880 * Decimal(10005).sqrt()
    K = 6
    M = 1
    X = 1
    L = 13591409
    S = L
    
    for i in range(1, n):
        M = (K ** 3 - 16 * K) * M // i ** 3
        L += 545140134
        X *= -262537412640768000
        S += Decimal(M * L) / X
        K += 12
    
    pi = C / S
    return str(pi)[:n + 2]  # Return first n digits plus the '3.'

n = 20
pi_digits = calculate_pi(n)
print(pi_digits)


2 Execution Order
In programming, code is generally executed line-by-line, from top to bottom, and this holds true for Python code as well. This means that the order in which you write your code is important.

For example, the following code:

print("First")
print("Second")
print("Third")
will output:

First
Second
Third
Challenge
In the code editor, there are three print statements. Rearrange them so that the output is:

Fourth
Fifth
Sixth
If you think you have the correct answer, click the Submit button.

Starter code:
print("Fifth")
print("Fourth")
print("Sixth")


Solution:
print("Fourth")
print("Fifth")
print("Sixth")


3 Printing Text
Earlier we printed Hello, world! to the console.

print("Hello, world!")
You may have noticed that we used double quotes "" around the text. This is known as a string in programming. Most languages use double quotes to define a string.

Some languages like Python (and JavaScript) also allow you to use single quotes '' to define a string.

A string is just a sequence of characters between the opening and closing quotes.

But what if we wanted to print a string that also contains quote characters? For example, how would the Python interpreter know where the following string ends?

print("They said, "Hello, world!"")
This code will cause an error. Python thinks we have a string "They said, ", followed by Hello, world!, which is outside of the quotes (not apart of the string).

One possible solution to this is to use a backslash \, aka the escape character, before each quote character inside the string.

print("They said, \"Hello, world!\"")
This tells Python we want to interpret the quote " as a character inside the string, not as a quote that ends the string.

Challenge
Your task is to correct the code in the code editor to print the following text to the console:

My favorite quote is "To be or not to be."
If you think you have the correct answer, click the Submit button.


Is there another solution?

Yes! Another way to define a string is to use single quotes instead of double quotes. So alternatively, if we want to use double quotes inside of a string, we can define the string using single quotes.

print('They said, "Hello, world!"')

This way we don't need to use the escape character.

The choice between single and double quotes is up to you. The first solution we discussed is useful because it works in more programming languages, since not all languages allow you to use single quotes to define a string.

By the way, we can also use single quotes inside of double quotes without any issues.

print("They said, 'Hello, world!'")

Starter code:
print("My favorite quote is "To be or not to be."")


Solution:
print("My favorite quote is \"To be or not to be.\"")


4 Code Errors
Earlier, if you attempted to run the following code before correcting it:

print("My favorite quote is "To be or not to be."")
You may have seen something like this in the console:

ERROR!
Traceback (most recent call last):
  File "<main.py>", line 1
    print("My favorite quote is "To be or not to be."")
          ^^^^^^^^^^^^^^^^^^^^^^^^^
SyntaxError: invalid syntax. Perhaps you forgot a comma?
This is the result of an error in our code. Specifically, it's a syntax error. Syntax errors occur when the code is not written correctly according to the rules of the programming language. It's not so different from a spelling or grammar error in a human language, except that computers are much less forgiving.

Sometimes you may get helpful error messages which help you identify the problem. Other times, the error message may not be as clear.

There are many types of programming errors such as syntax errors, runtime errors, and logical errors. Syntax errors are easier to fix, because they usually point out which line the error is on.

Challenge
In the code editor, there is a syntax error. Correct the code so that it prints the following text to the console:

Can someone pls add a closing parenthesis?
If you think you have the correct answer, click the Submit button.


What is a runtime error?

A runtime error is an error that occurs while the program is running. That means the syntax of the program itself is fine. It is usually caused by something that the programmer did not anticipate. Runtime errors can be difficult to debug because they may not always occur consistently. For example, if we programmed a calculator and the user tries to divide by zero, we will get a runtime error.


What is a logical error?

A logical error is an error that occurs when the program runs without crashing or producing an error, but the output is not what the programmer intended. This is commonly known as a bug. Logical errors can be difficult to find because as programmers we have to identify which lines of code are causing the incorrect output. There are various techniques to debug logical errors, but in large programs, it can still be very challenging.

Starter code:
print("Can someone pls add a closing parenthesis?"

Solution:
print("Can someone pls add a closing parenthesis?")


5 Comments
In programming we can annotate our code without affecting the output. This is done using comments.

Comments are ignored by the interpreter. They are used to explain what the code is doing or add any sort of message, usually for humans. They are useful for other programmers who may read your code, or for yourself in the future if you forget what a certain piece of code does.

In Python, comments are created using the # character. Any text after the # character on a line is considered a comment.

# This is a comment
If we want to ignore a piece of code, we can also comment it out temporarily. This is useful for debugging or testing.

# print("This line of code is commented out")
The above code will not print anything to the console because the line is commented out.

Challenge
Your task is to fix the code on the right without deleting any of the lines. It should print the following text to the console:

I belong here.
I also belong here.
Me too!
If you think you have the correct answer, click the Submit button.


Click me for a useful tip.

A short cut to comment out lines of code in most code editors is to select the lines you want to comment out and press Ctrl + / (Windows / Linux) or Cmd + / (Mac). This will automatically add the # character to the beginning of each line.

Starter code:
print("I belong here.")
print("Why am I here?")
print("Get me out of here!")
print("I also belong here.")
print("Me too!")


Solution:
print("I belong here.")
# print("Why am I here?")
# print("Get me out of here!")
print("I also belong here.")
print("Me too!")




2 - Variables

6 Variable Declaration
Earlier we printed the "Hello, world!" string to the console. After it was printed we couldn't reuse that string, unless we retyped it all out from scratch, as shown below:

print("Hello, world!")
print("Hello, world!")
But what if we wanted to use that string multiple times in our code? This is where variables come in. With the following code, we can store the string in a variable and print it multiple times:

message = "Hello, world!"
print(message)
print(message)
Output:

Hello, world!
Hello, world!
In the code above, we stored the string "Hello, world!" in a variable called message. Then, instead of passing a raw string to the print() function, we passed the variable message. This way, we can print the same string multiple times without having to retype it.

Variables are like containers that hold values.

Challenge
Update the code on the right so that it prints this string is stored in a variable to the console twice. You should be able to accomplish this by only adding one line of code.

If you think you have the correct answer, click the Submit button.


Variable vs Raw String

Notice that we don't have double quotes around message. If we did, Python would think we're trying to print the string "message" instead of the value stored in the variable message.

Starter code:

# don't modify the code below this line
print(message)
print(message)


Solution:
message = "this string is stored in a variable"
# don't modify the code below this line
print(message)
print(message)


7 Variable Naming
8 Naming Conventions
9 Reassigning Variables
10 Multiple Assignments
11 Variable Types
12 Dynamic Typing
13 Type Casting
14 Type Errors
15 Empty Variable


3 - Math

16 Arithmetic Operators
17 More Operators
18 Shorthand Operators
19 Boolean OR
20 Boolean AND
21 Boolean Negation

4 - Funcitons

22 Introduction to Functions
23 Function Declaration
24 Parameters
25 Multiple Parameters
26 Return Statement
27 Type Hints
28 Scope
29 Global vs Local Scope
30 Default Arguments

5 - Conditional Statements

31 Comparison Operators
32 If Statements
33 If Statement Scope
34 If-Else Statements
35 Else-If Statements
36 Logic Condition
37 Truthy and Falsy

6 - Loops

38 While Loops
39 While Loops Counting
40 While Loops Multiples
41 For Loops
42 For Loops Start
43 For Loops Step
44 For Loops Reverse
45 Nested Loops
46 Control Flow

7 - Strings

47 Length Function
48 String Indexing
49 String Looping
50 String Looping Shorthand
51 String Concatenation
52 String Slicing Part 1
53 String Slicing Part 2
54 Reversing a String
55 Strings are Immutable
56 Strings Formatting

8 - Lists

57 Intro to Lists
58 List Operations
59 List Looping
60 List Functions
61 List Append
62 List Pop
63 List Find
64 List Slicing
65 Tuples

9 - Sets

66 Intro to sets
67 Set operations
68 Set practice

10 - Dictionaries

69 Intro to Dictionaries
70 Dict Operations
71 Dict Looping
72 Dict Practice
73 Dict Remove
74 Dict Values

11 - Reading Stdin

75 Reading Input
76 Type Conversion with Input
77 Parse Input
78 Read Input Practice

12 - Exception Handling

79 Try Except
80 Error Catching
81 Multiple Except Blocks