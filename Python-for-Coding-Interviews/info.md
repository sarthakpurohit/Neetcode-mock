1 - Sorting

0 Sort Ascending
Question:
Sort Ascending
In Python, you can sort a list of elements by calling .sort() on the list.

elements = [5, 3, 6, 2, 1]

elements.sort()

print(elements) # [1, 2, 3, 5, 6]
By default, the .sort() method sorts the elements in ascending order in-place. The return value of the .sort() method is None.

This method also works for a list of strings.

elements = ["grape", "apple", "banana", "orange"]

elements.sort()

print(elements) # ['apple', 'banana', 'grape', 'orange']
By default, strings are sorted in lexicographical order.

Challenge
Implement the following functions:

sort_words(words: List[str]) -> List[str] - This function accepts a list of words and returns the list of words sorted in ascending order.
sort_numbers(numbers: List[int]) -> List[int] - This function accepts a list of numbers and returns the list of numbers sorted in ascending order.
sort_decimals(numbers: List[float]) -> List[float] - This function accepts a list of decimal numbers and returns the list of decimal numbers sorted in ascending order.
Time and Space Complexity
The time complexity of the .sort() method is 
O
(
n
l
o
g
n
)
O(nlogn), where n is the number of elements in the list.
The space complexity is 
O
(
n
)
O(n), where n is the number of elements in the list.
Note: Python uses the Timsort algorithm for sorting lists. Timsort is a hybrid sorting algorithm derived from merge sort and insertion sort. To learn more about sorting, check out the Data Structures and Algorithms for Beginners course.

Starter code:
from typing import List


def sort_words(words: List[str]) -> List[str]:
    pass

def sort_numbers(numbers: List[int]) -> List[int]:
    pass

def sort_decimals(numbers: List[float]) -> List[float]:
    pass



# do not modify below this line
print(sort_words(["cherry", "apple", "blueberry", "banana", "watermelon", "zucchini", "kiwi", "pear"]))

print(sort_numbers([1, 5, 3, 2, 4, 11, 19, 9, 2, 5, 6, 7, 4, 2, 6]))

print(sort_decimals([3.14, 2.82, 6.433, 7.9, 21.555, 21.554]))

Solution:
from typing import List


def sort_words(words: List[str]) -> List[str]:
    words.sort()
    return words

def sort_numbers(numbers: List[int]) -> List[int]:
    numbers.sort()
    return numbers

def sort_decimals(numbers: List[float]) -> List[float]:
    numbers.sort()
    return numbers


# do not modify below this line
print(sort_words(["cherry", "apple", "blueberry", "banana", "watermelon", "zucchini", "kiwi", "pear"]))

print(sort_numbers([1, 5, 3, 2, 4, 11, 19, 9, 2, 5, 6, 7, 4, 2, 6]))

print(sort_decimals([3.14, 2.82, 6.433, 7.9, 21.555, 21.554]))


1 Sort Descending
Quesiton:
Sort Descending
The .sort() method also accepts some optional parameters. This is the .sort() function signature:

def sort(key=None, reverse=False) -> None:
The key parameter allows us to customize the sorting order. We will learn more about this soon.
The reverse parameter is a boolean value that determines whether the list should be sorted in descending order. By default, it is set to False.
If we want to sort a list in descending order, we can set the reverse parameter to True.

elements = [5, 3, 6, 2, 1]

elements.sort(key=None, reverse=True)

print(elements) # [6, 5, 3, 2, 1]
We can actually omit the key parameter and only pass the reverse parameter, by using a feature of Python called keyword arguments.

elements.sort(reverse=True)
It's also possible for us to sort the list in ascending order and then manually reverse the result.

elements = [5, 3, 6, 2, 1]

elements.sort()

elements.reverse()
Challenge
Implement the following functions:

sort_words(words: List[str]) -> List[str] - This function accepts a list of words and returns the list of words sorted in descending order.
sort_numbers(numbers: List[int]) -> List[int] - This function accepts a list of numbers and returns the list of numbers sorted in descending order.
sort_decimals(numbers: List[float]) -> List[float] - This function accepts a list of decimal numbers and returns the list of decimal numbers sorted in descending order.

Starter Code:
from typing import List


def sort_words(words: List[str]) -> List[str]:
    pass

def sort_numbers(numbers: List[int]) -> List[int]:
    pass

def sort_decimals(numbers: List[float]) -> List[float]:
    pass



# do not modify below this line
print(sort_words(["cherry", "apple", "blueberry", "banana", "watermelon", "zucchini", "kiwi", "pear"]))

print(sort_numbers([1, 5, 3, 2, 4, 11, 19, 9, 2, 5, 6, 7, 4, 2, 6]))

print(sort_decimals([3.14, 2.82, 6.433, 7.9, 21.555, 21.554]))


Solution:
from typing import List


def sort_words(words: List[str]) -> List[str]:
    words.sort(reverse=True)
    return words

def sort_numbers(numbers: List[int]) -> List[int]:
    numbers.sort(reverse=True)
    return numbers

def sort_decimals(numbers: List[float]) -> List[float]:
    numbers.sort(reverse=True)
    return numbers


# do not modify below this line
print(sort_words(["cherry", "apple", "blueberry", "banana", "watermelon", "zucchini", "kiwi", "pear"]))

print(sort_numbers([1, 5, 3, 2, 4, 11, 19, 9, 2, 5, 6, 7, 4, 2, 6]))

print(sort_decimals([3.14, 2.82, 6.433, 7.9, 21.555, 21.554]))


2 Sort Custom
Question:
Sort Custom
We can also specify a custom sorting order by using the key parameter in the .sort() method. The key parameter doesn't accept a value, instead, it accepts a function that returns a value to be used for sorting.

def get_word_length(word: str) -> int:
    return len(word)

words = ["apple", "banana", "kiwi", "pear", "watermelon", "blueberry", "cherry"]

words.sort(key=get_word_length)

print(words) # ['kiwi', 'pear', 'apple', 'banana', 'cherry', 'blueberry', 'watermelon']
In the example above, we defined a function get_word_length that returns the length of a word. We then passed this function as the key parameter to the .sort() method. This means the words will be sorted based on their length, in ascending order, and not based on their lexicographical order.

Challenge
Implement the following functions:

sort_words(words: List[str]) -> List[str] - This function accepts a list of words and returns a new list of words sorted based on their length, in descending order.
sort_numbers(numbers: List[int]) -> List[int] - This function accepts a list of numbers and returns a new list of numbers sorted based on their absolute value, in ascending order. Hint: You may use the abs() function to get the absolute value of a number.
Hint: You may define additional functions. Functions defined in the global scope are accessible within other functions.

Starter code:
from typing import List


def sort_words(words: List[str]) -> List[str]:
    pass


def sort_numbers(numbers: List[int]) -> List[int]:
    pass


# do not modify below this line
print(sort_words(["cherry", "apple", "blueberry", "banana", "watermelon", "zucchini", "kiwi", "pear"]))

print(sort_numbers([1, -5, -3, 2, 4, 11, -19, 9, -2, 5, -6, 7, -4, 2, 6]))

Solution:
from typing import List


def word_length(word: str) -> int:
    return len(word)

def number_abs(number: int) -> int:
    return abs(number)


def sort_words(words: List[str]) -> List[str]:
    words.sort(key=word_length, reverse=True)
    return words

def sort_numbers(numbers: List[int]) -> List[int]:
    numbers.sort(key=number_abs)
    return numbers    


# do not modify below this line
print(sort_words(["cherry", "apple", "blueberry", "banana", "watermelon", "zucchini", "kiwi", "pear"]))

print(sort_numbers([1, -5, -3, 2, 4, 11, -19, 9, -2, 5, -6, 7, -4, 2, 6]))


3 Sort Lambda
Question:
Sort Lambda
Defining a separate function just to pass it into the key parameter of the .sort() method can be cumbersome. We can use a lambda function to define a function in a single line and pass it directly to the .sort() method.

To sort a list of words by their length, we can use a lambda function like this:

words = ["apple", "banana", "kiwi", "pear", "watermelon", "blueberry", "cherry"]

words.sort(key=lambda word: len(word))

print(words) # ['kiwi', 'pear', 'apple', 'banana', 'cherry', 'blueberry', 'watermelon']
The lambda function lambda word: len(word) is equivalent to the function get_word_length we defined in the previous example. It takes a word as input and returns the length of the word.

The syntax includes:

The keyword lambda.
The input variable word. We can use any variable name here.
The colon :, after which we define the function body.
The expression len(word), which is the return value of the function.
A lambda function must be a single expression, and it cannot contain multiple statements. It's a convenient way to define simple functions without the need to define a separate function.

Challenge
Implement the following functions:

sort_words(words: List[str]) -> List[str] - This function accepts a list of words and returns a new list of words sorted based on their length, in descending order. Use a lambda function to sort the words by their length.
sort_numbers(numbers: List[int]) -> List[int] - This function accepts a list of numbers and returns a new list of numbers sorted based on their absolute value, in ascending order. Use a lambda function to sort the numbers by their absolute value.

Starter code:
from typing import List


def sort_words(words: List[str]) -> List[str]:
    pass


def sort_numbers(numbers: List[int]) -> List[int]:
    pass


# do not modify below this line
print(sort_words(["cherry", "apple", "blueberry", "banana", "watermelon", "zucchini", "kiwi", "pear"]))

print(sort_numbers([1, -5, -3, 2, 4, 11, -19, 9, -2, 5, -6, 7, -4, 2, 6]))

Solution:
from typing import List


def sort_words(words: List[str]) -> List[str]:
    words.sort(key=lambda word: len(word), reverse=True)
    return words

def sort_numbers(numbers: List[int]) -> List[int]:
    numbers.sort(key=lambda number: abs(number))
    return numbers    


# do not modify below this line
print(sort_words(["cherry", "apple", "blueberry", "banana", "watermelon", "zucchini", "kiwi", "pear"]))

print(sort_numbers([1, -5, -3, 2, 4, 11, -19, 9, -2, 5, -6, 7, -4, 2, 6]))


4 Sorted copy
Question:
Sorted Copy
There is another way to sort a list in Python, using the sorted() function. The sorted() function returns a new list with the elements sorted in the specified order. The original list remains unchanged.

words = ["kiwi", "pear", "apple", "banana", "cherry", "blueberry"]

sorted_words = sorted(words)

print(sorted_words) # ['apple', 'banana', 'blueberry', 'cherry', 'kiwi', 'pear']
The sorted() function takes the list as the first argument and returns a new list with the elements sorted in ascending order by default.

You can also specify the order using the reverse parameter:

numbers = [5, -3, 2, -4, 6, -2, 4]

sorted_numbers = sorted(numbers, reverse=True)

print(sorted_numbers) # [6, 5, 4, 2, -2, -3, -4]
You can also pass a custom function to the key parameter to specify the sorting criteria.

numbers = [5, -3, 2, -4, 6, -2, 4]

sorted_numbers = sorted(numbers, key=abs)

print(sorted_numbers) # [2, -2, -3, 4, -4, 5, 6]
For the most part, it's similar to the sort() method, but it returns a new list instead of modifying the original list.

Challenge
Implement the following functions:

sort_words(words: List[str]) -> List[str] - This function accepts a list of words and returns a new list of words sorted in ascending order. Do not modify the original list.
sort_numbers(numbers: List[int]) -> List[int] - This function accepts a list of numbers and returns a new list of numbers sorted in descending order based on their absolute value. Do not modify the original list.

Starter code:
from typing import List


def sort_words(words: List[str]) -> List[str]:
    pass


def sort_numbers(numbers: List[int]) -> List[int]:
    pass


# do not modify below this line
original_words = ["cherry", "apple", "blueberry", "banana", "watermelon", "zucchini", "kiwi", "pear"]

print(original_words)
print(sort_words(original_words))

original_numbers = [1, -5, -3, 2, 4, 11, -19, 9, -2, 5, -6, 7, -4, 2, 6]

print(original_numbers)
print(sort_numbers(original_numbers))

Solution:
from typing import List


def sort_words(words: List[str]) -> List[str]:
    sorted_words = sorted(words)
    return sorted_words

def sort_numbers(numbers: List[int]) -> List[int]:
    sorted_numbers = sorted(numbers, key=lambda x: abs(x), reverse=True)
    return sorted_numbers


# do not modify below this line
original_words = ["cherry", "apple", "blueberry", "banana", "watermelon", "zucchini", "kiwi", "pear"]

print(original_words)
print(sort_words(original_words))

original_numbers = [1, -5, -3, 2, 4, 11, -19, 9, -2, 5, -6, 7, -4, 2, 6]

print(original_numbers)
print(sort_numbers(original_numbers))



2 - Pythonic Code

5 Unpacking
Question:
Unpacking
The biggest advantage of using Python for coding interviews is its simplicity and readability. In this section we will learn some of the shortcuts Python provides to make our code easy to read and write.

One of these shortcuts is unpacking.

point1 = [0, 0]
point2 = [2, 4]

x1, y1 = point1 # x1 = 0, y1 = 0
x2, y2 = point2 # x2 = 2, y2 = 4

slope = (y2 - y1) / (x2 - x1)

print(slope) # Output: 2.0
Above, we have code that calulates the slope of a line given two points.
Each point is a list of two integers.
Notice how we have two variables on the left side of the assignment operator, with a list on the right side. This is called unpacking. We know point1 and point2 are lists of size 2, so we can unpack them into two variables each.
The below code accomplishes the same without unpacking but with slightly more code:

x1, y1 = point1[0], point1[1]
x2, y2 = point2[0], point2[1]
If we attempt unpacking with not enough variables on the left-side, we will get a ValueError.

x, y = [0, 0, 0] # ValueError: too many values to unpack (expected 2)
Unpacking also works with tuples and sets with the same syntax.

Challenge
Implement the following functions using unpacking:

sum_3_integers(triplet: List[int]) -> int that takes a list of 3 integers and returns the sum of the integers.
compute_volume(box_dimensions: Tuple[int, int, int]) -> int that takes a list of 3 integers representing [width, height, depth] of a box and returns the volume of it.
That's it?
You may think that these small shortcuts don't make a difference. But after you master the arts of Pythonic code, you will be able to save several lines of code as opposed to a more verbose language.

For example, a 30 line function in Java may only be 15 lines in Python.

Starter code:
from typing import List, Tuple


def sum_3_integers(triplet: List[int]) -> int:
    pass


def compute_volume(box_dimensions: Tuple[int, int, int]) -> int:
    pass
  

# do not modify below this line
print(sum_3_integers([1, 2, 3]))
print(sum_3_integers([4, 6, 2]))

print(compute_volume((1, 2, 3)))
print(compute_volume((3, 2, 1)))
print(compute_volume((3, 9, 7)))

Solution:
from typing import List, Tuple


def sum_3_integers(triplet: List[int]) -> int:
    a, b, c = triplet
    return a + b + c


def compute_volume(box_dimensions: Tuple[int, int, int]) -> int:
    width, height, depth = box_dimensions
    return width * height * depth
  

# do not modify below this line
print(sum_3_integers([1, 2, 3]))
print(sum_3_integers([4, 6, 2]))

print(compute_volume((1, 2, 3)))
print(compute_volume((3, 2, 1)))
print(compute_volume((3, 9, 7)))


6 Loop unpacking

7 Enumerate

8 Zip

9 Inequality

10 Min Max Shortcut


3 - Lists

11 Resizable List Part 1

12 Resizable List Part 2

13 List concat

14 List initialization

15 List clone

16 List comprehension


4 - Stacks and Queues

17 Stack Push and Pop

18 Queue Enqueue and Dequeue 

19 Double ended queue


5 - 2-D Lists

20 Multi-dimensional List

21 2D Grid

22 Nested List Comprehension


6 - Hashmaps and Hashsets

23 Hash Map Basics
24 Default Dict
25 Counter
26 Dict Comprehension
27 Dict Items
28 Hash Set Basics
29 Set Comprehension
30 Tuple Keys


7 - Heaps / Priority Queues

31 Heap Push
32 Heap Pop
33 Heapify
34 Max Heap
35 Custom Heap
36 Heap N Smallest
37 Heap N Largest


8 - Sorted Dicts and Sorted Sets

38 Sorted Dict Basics
39 Sorted Set Basics
