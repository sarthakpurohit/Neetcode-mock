1 - Memoization & Caching

0 Basic Memoization with a Dict
Question:
Basic Memoization with a Dict
When a recursive function recomputes the same subproblems, we can store results in a dictionary to avoid redundant work. This is called **memoization**.

The pattern is simple:
1. Create a dictionary (the cache)
2. Before computing, check if the result is already cached
3. If yes, return it directly
4. If no, compute, store it, then return

```python
memo = {}

def fib(n):
    if n in memo:
        return memo[n]
    if n <= 1:
        result = n
    else:
        result = fib(n - 1) + fib(n - 2)
    memo[n] = result
    return result
```

Without memoization, `fib(40)` takes billions of operations. With memoization, it takes ~40. That's the difference between O(2^n) and O(n).

Challenge
Implement `count_paths(m, n)` that returns the number of unique paths from top-left to bottom-right of an m×n grid, moving only right or down. Use a dictionary for memoization.

Expected output:
count_paths(3, 3) → 6
count_paths(3, 7) → 28

Starter code:
def count_paths(m, n, memo=None):
    if memo is None:
        memo = {}
    # TODO: implement with memoization
    pass


print(count_paths(3, 3))
print(count_paths(3, 7))

Solution:
def count_paths(m, n, memo=None):
    if memo is None:
        memo = {}
    if (m, n) in memo:
        return memo[(m, n)]
    if m == 1 or n == 1:
        return 1
    memo[(m, n)] = count_paths(m - 1, n, memo) + count_paths(m, n - 1, memo)
    return memo[(m, n)]


print(count_paths(3, 3))
print(count_paths(3, 7))


1 functools.cache Decorator
Question:
functools.cache Decorator
Python 3.9+ provides `@functools.cache` — an unlimited memoization decorator. Wrap any pure function and Python handles the caching automatically.

```python
from functools import cache

@cache
def fib(n):
    if n <= 1:
        return n
    return fib(n - 1) + fib(n - 2)
```

That's it. No manual dictionary, no key management. The decorator stores results keyed by the function arguments (which must be hashable).

For Python 3.8 and earlier, use `@lru_cache(maxsize=None)` for the same effect.

Challenge
Implement `climb_stairs(n)` that returns the number of distinct ways to climb n stairs taking 1 or 2 steps at a time. Use `@cache`.

Expected output:
climb_stairs(5) → 8
climb_stairs(10) → 89

Starter code:
from functools import cache


@cache
def climb_stairs(n):
    # TODO: implement
    pass


print(climb_stairs(5))
print(climb_stairs(10))

Solution:
from functools import cache


@cache
def climb_stairs(n):
    if n <= 2:
        return n
    return climb_stairs(n - 1) + climb_stairs(n - 2)


print(climb_stairs(5))
print(climb_stairs(10))


2 lru_cache with maxsize
Question:
lru_cache with maxsize
`@lru_cache(maxsize=N)` keeps only the N most recently used results. When memory matters (e.g., processing a stream), this avoids unbounded growth.

```python
from functools import lru_cache

@lru_cache(maxsize=128)
def expensive(x):
    return x ** x
```

You can inspect cache stats with `expensive.cache_info()` and clear it with `expensive.cache_clear()`.

When `maxsize=None`, it behaves identically to `@cache`.

Challenge
Implement `min_cost_climbing(costs)` where `costs` is a list and you can start at index 0 or 1, taking 1 or 2 steps, paying `costs[i]` when stepping on stair `i`. Return the minimum cost to reach past the last stair. Use `@lru_cache`.

Expected output:
min_cost_climbing([10, 15, 20]) → 15
min_cost_climbing([1, 100, 1, 1, 1, 100, 1, 1, 100, 1]) → 6

Starter code:
from functools import lru_cache


def min_cost_climbing(costs):
    n = len(costs)

    @lru_cache(maxsize=None)
    def dp(i):
        # TODO: implement
        pass

    return min(dp(0), dp(1))


print(min_cost_climbing([10, 15, 20]))
print(min_cost_climbing([1, 100, 1, 1, 1, 100, 1, 1, 100, 1]))

Solution:
from functools import lru_cache


def min_cost_climbing(costs):
    n = len(costs)

    @lru_cache(maxsize=None)
    def dp(i):
        if i >= n:
            return 0
        return costs[i] + min(dp(i + 1), dp(i + 2))

    return min(dp(0), dp(1))


print(min_cost_climbing([10, 15, 20]))
print(min_cost_climbing([1, 100, 1, 1, 1, 100, 1, 1, 100, 1]))


3 Memoization with Tuple Keys
Question:
Memoization with Tuple Keys
`@cache` requires hashable arguments. Lists aren't hashable, but tuples are. A common interview trick: convert a list slice or state to a tuple for the cache key.

```python
from functools import cache

@cache
def helper(nums_tuple, target):
    # nums_tuple is hashable, a list wouldn't work here
    ...
```

For 2D problems, you often cache on `(row, col)` or `(index, remaining)` tuples.

Challenge
Implement `can_partition(nums)` that returns True if `nums` can be split into two subsets with equal sum. Use memoization with tuple keys. Hint: reduce to "can we find a subset that sums to total//2?"

Expected output:
can_partition([1, 5, 11, 5]) → True
can_partition([1, 2, 3, 5]) → False

Starter code:
from functools import cache


def can_partition(nums):
    total = sum(nums)
    if total % 2 != 0:
        return False
    target = total // 2

    @cache
    def dp(i, remaining):
        # TODO: implement
        pass

    return dp(0, target)


print(can_partition([1, 5, 11, 5]))
print(can_partition([1, 2, 3, 5]))

Solution:
from functools import cache


def can_partition(nums):
    total = sum(nums)
    if total % 2 != 0:
        return False
    target = total // 2

    @cache
    def dp(i, remaining):
        if remaining == 0:
            return True
        if i >= len(nums) or remaining < 0:
            return False
        return dp(i + 1, remaining - nums[i]) or dp(i + 1, remaining)

    return dp(0, target)


print(can_partition([1, 5, 11, 5]))
print(can_partition([1, 2, 3, 5]))


4 Tabulation (Bottom-Up DP)
Question:
Tabulation (Bottom-Up DP)
Memoization is top-down: start from the final answer and recurse down. **Tabulation** is bottom-up: fill a table from base cases upward. It avoids recursion depth issues and is often faster due to no function-call overhead.

```python
def fib(n):
    if n <= 1:
        return n
    dp = [0] * (n + 1)
    dp[1] = 1
    for i in range(2, n + 1):
        dp[i] = dp[i-1] + dp[i-2]
    return dp[n]
```

Both approaches solve the same problems. Top-down is easier to write; bottom-up is more memory-predictable.

Challenge
Implement `count_paths_tab(m, n)` using tabulation (a 2D list) — same grid paths problem as Challenge 0, but iterative.

Expected output:
count_paths_tab(3, 3) → 6
count_paths_tab(3, 7) → 28

Starter code:
def count_paths_tab(m, n):
    # TODO: implement with a 2D dp table
    pass


print(count_paths_tab(3, 3))
print(count_paths_tab(3, 7))

Solution:
def count_paths_tab(m, n):
    dp = [[1] * n for _ in range(m)]
    for i in range(1, m):
        for j in range(1, n):
            dp[i][j] = dp[i-1][j] + dp[i][j-1]
    return dp[m-1][n-1]


print(count_paths_tab(3, 3))
print(count_paths_tab(3, 7))


5 Space-Optimized Tabulation
Question:
Space-Optimized Tabulation
Many DP tables only depend on the previous row/column. You can reduce O(m×n) space to O(n) by keeping only one row at a time.

```python
def fib(n):
    if n <= 1:
        return n
    prev, curr = 0, 1
    for _ in range(2, n + 1):
        prev, curr = curr, prev + curr
    return curr
```

This is a constant-space Fibonacci. The same idea applies to grid problems: keep one row and update in-place.

Challenge
Implement `count_paths_opt(m, n)` using O(n) space — one row that you update m-1 times.

Expected output:
count_paths_opt(3, 3) → 6
count_paths_opt(3, 7) → 28

Starter code:
def count_paths_opt(m, n):
    # TODO: implement with O(n) space
    pass


print(count_paths_opt(3, 3))
print(count_paths_opt(3, 7))

Solution:
def count_paths_opt(m, n):
    row = [1] * n
    for _ in range(1, m):
        for j in range(1, n):
            row[j] += row[j-1]
    return row[n-1]


print(count_paths_opt(3, 3))
print(count_paths_opt(3, 7))


2 - Binary Search Utilities

6 bisect_left and bisect_right
Question:
bisect_left and bisect_right
Python's `bisect` module provides binary search functions that find insertion points in sorted sequences.

```python
from bisect import bisect_left, bisect_right

nums = [1, 3, 3, 3, 5, 7]

bisect_left(nums, 3)   # 1 — leftmost position where 3 can be inserted
bisect_right(nums, 3)  # 4 — rightmost position where 3 can be inserted
```

- `bisect_left(a, x)`: index of first element >= x
- `bisect_right(a, x)`: index of first element > x

The count of occurrences of `x` is `bisect_right(a, x) - bisect_left(a, x)`.

These run in O(log n) time — no need to write binary search from scratch for sorted-array lookups.

Challenge
Implement `count_occurrences(nums, target)` that returns how many times `target` appears in the sorted list `nums` using bisect. O(log n) time.

Expected output:
count_occurrences([1, 2, 2, 2, 3, 4, 5], 2) → 3
count_occurrences([1, 1, 1, 1, 1], 1) → 5
count_occurrences([1, 3, 5, 7], 4) → 0

Starter code:
from bisect import bisect_left, bisect_right


def count_occurrences(nums, target):
    # TODO: implement using bisect
    pass


print(count_occurrences([1, 2, 2, 2, 3, 4, 5], 2))
print(count_occurrences([1, 1, 1, 1, 1], 1))
print(count_occurrences([1, 3, 5, 7], 4))

Solution:
from bisect import bisect_left, bisect_right


def count_occurrences(nums, target):
    return bisect_right(nums, target) - bisect_left(nums, target)


print(count_occurrences([1, 2, 2, 2, 3, 4, 5], 2))
print(count_occurrences([1, 1, 1, 1, 1], 1))
print(count_occurrences([1, 3, 5, 7], 4))


7 insort for Maintaining Sorted Order
Question:
insort for Maintaining Sorted Order
`bisect.insort(a, x)` inserts `x` into sorted list `a` while maintaining sort order. Insertion itself is O(n) due to list shifting, but finding the position is O(log n).

```python
from bisect import insort

nums = [1, 3, 5, 7]
insort(nums, 4)
print(nums)  # [1, 3, 4, 5, 7]
```

Use this when you need a sorted collection that supports insertion — simpler than a heap when you also need indexing.

Challenge
Implement `MedianFinder` class with:
- `add(num)`: adds a number using insort
- `median()`: returns the median of all added numbers

Expected output:
finder adds 3, 1, 5, 2 → median() returns 2.5

Starter code:
from bisect import insort


class MedianFinder:
    def __init__(self):
        self.nums = []

    def add(self, num):
        # TODO
        pass

    def median(self):
        # TODO
        pass


finder = MedianFinder()
for x in [3, 1, 5, 2]:
    finder.add(x)
print(finder.median())

Solution:
from bisect import insort


class MedianFinder:
    def __init__(self):
        self.nums = []

    def add(self, num):
        insort(self.nums, num)

    def median(self):
        n = len(self.nums)
        if n % 2 == 1:
            return self.nums[n // 2]
        return (self.nums[n // 2 - 1] + self.nums[n // 2]) / 2


finder = MedianFinder()
for x in [3, 1, 5, 2]:
    finder.add(x)
print(finder.median())


8 Custom Binary Search Template
Question:
Custom Binary Search Template
Sometimes `bisect` doesn't fit — you need a custom condition. The standard template:

```python
def binary_search(lo, hi, condition):
    while lo < hi:
        mid = (lo + hi) // 2
        if condition(mid):
            hi = mid
        else:
            lo = mid + 1
    return lo
```

This finds the **leftmost** position where `condition` is True. Variants:
- For rightmost False: return `lo - 1` after the loop
- For exact match: check `lo` after the loop

Challenge
Implement `first_bad_version(n, is_bad)` where versions 1..n exist and `is_bad(v)` returns True if version v is bad. All versions after the first bad one are also bad. Find the first bad version in O(log n).

Expected output:
first_bad_version(10, lambda v: v >= 4) → 4

Starter code:
def first_bad_version(n, is_bad):
    # TODO: binary search for leftmost bad version
    pass


print(first_bad_version(10, lambda v: v >= 4))
print(first_bad_version(100, lambda v: v >= 77))

Solution:
def first_bad_version(n, is_bad):
    lo, hi = 1, n
    while lo < hi:
        mid = (lo + hi) // 2
        if is_bad(mid):
            hi = mid
        else:
            lo = mid + 1
    return lo


print(first_bad_version(10, lambda v: v >= 4))
print(first_bad_version(100, lambda v: v >= 77))


9 Binary Search on Answer
Question:
Binary Search on Answer
A powerful pattern: binary search on the **answer** itself. If you can check "is answer X feasible?" in O(n), and feasibility is monotonic (all values >= some threshold work), binary search finds the optimal answer in O(n log range).

Example: "What's the minimum capacity to ship packages in D days?" — binary search on capacity, check feasibility by simulating.

Challenge
Implement `min_eating_speed(piles, h)` — Koko has `h` hours to eat all bananas. At speed `k`, she eats `ceil(pile/k)` hours per pile. Find minimum integer `k` so she finishes in time.

Expected output:
min_eating_speed([3, 6, 7, 11], 8) → 4
min_eating_speed([30, 11, 23, 4, 20], 5) → 30

Starter code:
import math


def min_eating_speed(piles, h):
    # TODO: binary search on the answer
    pass


print(min_eating_speed([3, 6, 7, 11], 8))
print(min_eating_speed([30, 11, 23, 4, 20], 5))

Solution:
import math


def min_eating_speed(piles, h):
    lo, hi = 1, max(piles)
    while lo < hi:
        mid = (lo + hi) // 2
        hours = sum(math.ceil(p / mid) for p in piles)
        if hours <= h:
            hi = mid
        else:
            lo = mid + 1
    return lo


print(min_eating_speed([3, 6, 7, 11], 8))
print(min_eating_speed([30, 11, 23, 4, 20], 5))


10 Bisect with Key Functions
Question:
Bisect with Key Functions
Python 3.10+ added a `key` parameter to bisect functions:

```python
from bisect import bisect_left

data = [(1, 'a'), (3, 'b'), (5, 'c'), (7, 'd')]
# Find insertion point for item with first element 4
idx = bisect_left(data, 4, key=lambda x: x[0])
```

For older Python, you can bisect on a separate sorted key-list, or use the classic trick of bisecting on a list of extracted keys.

Challenge
Given a sorted list of `(timestamp, value)` tuples, implement `get_value_at(data, t)` that returns the value at the largest timestamp <= t (or None if no such timestamp exists).

Expected output:
get_value_at([(1,'a'), (3,'b'), (7,'c')], 5) → 'b'
get_value_at([(1,'a'), (3,'b'), (7,'c')], 7) → 'c'
get_value_at([(1,'a'), (3,'b'), (7,'c')], 0) → None

Starter code:
from bisect import bisect_right


def get_value_at(data, t):
    # TODO: use bisect to find the right entry
    pass


print(get_value_at([(1,'a'), (3,'b'), (7,'c')], 5))
print(get_value_at([(1,'a'), (3,'b'), (7,'c')], 7))
print(get_value_at([(1,'a'), (3,'b'), (7,'c')], 0))

Solution:
from bisect import bisect_right


def get_value_at(data, t):
    timestamps = [item[0] for item in data]
    idx = bisect_right(timestamps, t) - 1
    if idx < 0:
        return None
    return data[idx][1]


print(get_value_at([(1,'a'), (3,'b'), (7,'c')], 5))
print(get_value_at([(1,'a'), (3,'b'), (7,'c')], 7))
print(get_value_at([(1,'a'), (3,'b'), (7,'c')], 0))


3 - Bit Manipulation

11 Bitwise Operators
Question:
Bitwise Operators
Python supports these bitwise operators on integers:

| Operator | Meaning | Example |
|----------|---------|---------|
| `&` | AND | `5 & 3` → 1 |
| `\|` | OR | `5 \| 3` → 7 |
| `^` | XOR | `5 ^ 3` → 6 |
| `~` | NOT (invert) | `~5` → -6 |
| `<<` | Left shift | `1 << 3` → 8 |
| `>>` | Right shift | `8 >> 2` → 2 |

Key insight: `1 << n` equals 2^n. This is how you create bit masks.

```python
print(bin(5))    # '0b101'
print(bin(3))    # '0b011'
print(bin(5&3))  # '0b001'
```

Challenge
Implement:
- `is_power_of_two(n)` → True if n is a power of 2 (use the trick: `n & (n-1) == 0`)
- `count_set_bits(n)` → number of 1-bits in n

Expected output:
is_power_of_two(16) → True
is_power_of_two(18) → False
count_set_bits(7) → 3
count_set_bits(255) → 8

Starter code:
def is_power_of_two(n):
    # TODO
    pass

def count_set_bits(n):
    # TODO
    pass


print(is_power_of_two(16))
print(is_power_of_two(18))
print(count_set_bits(7))
print(count_set_bits(255))

Solution:
def is_power_of_two(n):
    return n > 0 and (n & (n - 1)) == 0

def count_set_bits(n):
    count = 0
    while n:
        count += n & 1
        n >>= 1
    return count


print(is_power_of_two(16))
print(is_power_of_two(18))
print(count_set_bits(7))
print(count_set_bits(255))


12 bin() and int() Conversions
Question:
bin() and int() Conversions
Convert between integers and binary strings:

```python
bin(10)        # '0b1010'
int('1010', 2) # 10
```

`bin()` returns a string with `0b` prefix. `int(s, 2)` parses a binary string.

Other useful: `n.bit_length()` returns the number of bits needed (excluding sign and leading zeros).

```python
(10).bit_length()  # 4 — because 10 is 1010 in binary
```

Challenge
Implement:
- `binary_string(n)` → binary representation without '0b' prefix
- `from_binary(s)` → integer from binary string
- `num_bits(n)` → minimum bits needed to represent n

Expected output:
binary_string(42) → '101010'
from_binary('101010') → 42
num_bits(255) → 8

Starter code:
def binary_string(n):
    # TODO
    pass

def from_binary(s):
    # TODO
    pass

def num_bits(n):
    # TODO
    pass


print(binary_string(42))
print(from_binary('101010'))
print(num_bits(255))

Solution:
def binary_string(n):
    return bin(n)[2:]

def from_binary(s):
    return int(s, 2)

def num_bits(n):
    return n.bit_length()


print(binary_string(42))
print(from_binary('101010'))
print(num_bits(255))


13 XOR Patterns
Question:
XOR Patterns
XOR has these properties:
- `a ^ a = 0` (cancels itself)
- `a ^ 0 = a` (identity)
- Commutative and associative

This makes XOR perfect for "find the unique element" problems: XOR all elements together, and duplicates cancel out.

```python
nums = [2, 3, 2, 4, 3]
result = 0
for n in nums:
    result ^= n
# result == 4 (the only non-duplicate)
```

Challenge
Implement:
- `single_number(nums)` → the element that appears exactly once (all others appear twice)
- `swap_without_temp(a, b)` → returns (b, a) using only XOR (no temp variable)

Expected output:
single_number([4, 1, 2, 1, 2]) → 4
swap_without_temp(5, 9) → (9, 5)

Starter code:
def single_number(nums):
    # TODO
    pass

def swap_without_temp(a, b):
    # TODO: use XOR swap
    pass


print(single_number([4, 1, 2, 1, 2]))
print(swap_without_temp(5, 9))

Solution:
def single_number(nums):
    result = 0
    for n in nums:
        result ^= n
    return result

def swap_without_temp(a, b):
    a ^= b
    b ^= a
    a ^= b
    return (a, b)


print(single_number([4, 1, 2, 1, 2]))
print(swap_without_temp(5, 9))


14 Bit Masks and Subsets
Question:
Bit Masks and Subsets
An integer can represent a subset of n elements: bit i is 1 if element i is included.

```python
# All subsets of [a, b, c] (n=3):
for mask in range(1 << 3):  # 0 to 7
    subset = [i for i in range(3) if mask & (1 << i)]
    print(mask, bin(mask), subset)
```

Common operations:
- Check if bit i is set: `mask & (1 << i)`
- Set bit i: `mask | (1 << i)`
- Clear bit i: `mask & ~(1 << i)`
- Toggle bit i: `mask ^ (1 << i)`

Challenge
Implement `generate_subsets(nums)` that returns all subsets of `nums` using bitmasks.

Expected output:
generate_subsets([1, 2, 3]) → [[], [1], [2], [1,2], [3], [1,3], [2,3], [1,2,3]]

Starter code:
def generate_subsets(nums):
    # TODO: use bitmasks to generate all subsets
    pass


print(generate_subsets([1, 2, 3]))

Solution:
def generate_subsets(nums):
    n = len(nums)
    result = []
    for mask in range(1 << n):
        subset = [nums[i] for i in range(n) if mask & (1 << i)]
        result.append(subset)
    return result


print(generate_subsets([1, 2, 3]))


15 Common Bit Tricks
Question:
Common Bit Tricks
Interview favorites:

1. **Get lowest set bit**: `n & (-n)` isolates the rightmost 1-bit
2. **Remove lowest set bit**: `n & (n - 1)` turns off the rightmost 1-bit
3. **Check if n-th bit is set**: `(num >> n) & 1`
4. **Two's complement**: Python integers have unlimited precision, so `~n` equals `-(n+1)`

```python
n = 12  # binary: 1100
n & (-n)   # 4 (binary: 0100) — lowest set bit
n & (n-1)  # 8 (binary: 1000) — removed lowest set bit
```

Challenge
Implement `hamming_distance(x, y)` that returns the number of bit positions where x and y differ. Hint: XOR then count set bits using the "remove lowest set bit" trick.

Expected output:
hamming_distance(1, 4) → 2
hamming_distance(7, 0) → 3

Starter code:
def hamming_distance(x, y):
    # TODO
    pass


print(hamming_distance(1, 4))
print(hamming_distance(7, 0))

Solution:
def hamming_distance(x, y):
    xor = x ^ y
    count = 0
    while xor:
        xor &= xor - 1
        count += 1
    return count


print(hamming_distance(1, 4))
print(hamming_distance(7, 0))


16 Bit Manipulation Practice
Question:
Bit Manipulation Practice
Combine the bit tricks for a slightly harder problem.

Given an array where every element appears three times except one (which appears once), find the unique element. You can't just XOR everything — that only works for pairs.

Approach: count bits at each position modulo 3.

Challenge
Implement `single_number_iii(nums)` — every element appears 3 times except one. Find it.

Expected output:
single_number_iii([2, 2, 3, 2]) → 3
single_number_iii([0, 1, 0, 1, 0, 1, 99]) → 99

Starter code:
def single_number_iii(nums):
    # TODO: count bits mod 3
    pass


print(single_number_iii([2, 2, 3, 2]))
print(single_number_iii([0, 1, 0, 1, 0, 1, 99]))

Solution:
def single_number_iii(nums):
    result = 0
    for bit in range(32):
        bit_sum = sum(1 for n in nums if n & (1 << bit))
        if bit_sum % 3:
            result |= (1 << bit)
    return result


print(single_number_iii([2, 2, 3, 2]))
print(single_number_iii([0, 1, 0, 1, 0, 1, 99]))


4 - Math Utilities

17 Infinity and Float Comparisons
Question:
Infinity and Float Comparisons
In DSA, you often need "infinitely large" or "infinitely small" initial values:

```python
import math

math.inf       # positive infinity
-math.inf      # negative infinity
float('inf')   # same as math.inf
float('-inf')  # same as -math.inf
```

Any number compares less than `math.inf` and greater than `-math.inf`. Use them to initialize min/max searches:

```python
min_val = math.inf
for x in data:
    min_val = min(min_val, x)
```

Also useful: `math.isinf(x)` checks if a value is infinite.

Challenge
Implement `closest_pair_distance(points)` — given a list of (x, y) points, return the Euclidean distance between the closest pair. Use `math.inf` for initialization and `math.sqrt` for distance.

Expected output:
closest_pair_distance([(0,0), (3,4), (1,1)]) → 1.414...

Starter code:
import math


def closest_pair_distance(points):
    # TODO: brute force O(n^2), initialize with math.inf
    pass


print(closest_pair_distance([(0, 0), (3, 4), (1, 1)]))

Solution:
import math


def closest_pair_distance(points):
    min_dist = math.inf
    n = len(points)
    for i in range(n):
        for j in range(i + 1, n):
            dx = points[i][0] - points[j][0]
            dy = points[i][1] - points[j][1]
            dist = math.sqrt(dx * dx + dy * dy)
            min_dist = min(min_dist, dist)
    return min_dist


print(closest_pair_distance([(0, 0), (3, 4), (1, 1)]))


18 GCD, LCM, and math.comb
Question:
GCD, LCM, and math.comb
Python's `math` module provides:

```python
import math

math.gcd(12, 8)       # 4
math.lcm(4, 6)        # 12 (Python 3.9+)
math.comb(5, 2)       # 10 (5 choose 2)
math.perm(5, 2)       # 20 (permutations)
math.factorial(5)     # 120
```

For GCD of multiple numbers: `math.gcd(a, b, c)` works in Python 3.9+. For earlier versions, use `functools.reduce`.

Challenge
Implement:
- `gcd_of_list(nums)` → GCD of all numbers in the list
- `lcm_of_list(nums)` → LCM of all numbers in the list
- `paths_in_grid(m, n)` → number of paths in m×n grid using combinations (it's C(m+n-2, m-1))

Expected output:
gcd_of_list([12, 8, 16]) → 4
lcm_of_list([4, 6, 8]) → 24
paths_in_grid(3, 3) → 6

Starter code:
import math
from functools import reduce


def gcd_of_list(nums):
    # TODO
    pass

def lcm_of_list(nums):
    # TODO
    pass

def paths_in_grid(m, n):
    # TODO: use math.comb
    pass


print(gcd_of_list([12, 8, 16]))
print(lcm_of_list([4, 6, 8]))
print(paths_in_grid(3, 3))

Solution:
import math
from functools import reduce


def gcd_of_list(nums):
    return reduce(math.gcd, nums)

def lcm_of_list(nums):
    def lcm(a, b):
        return a * b // math.gcd(a, b)
    return reduce(lcm, nums)

def paths_in_grid(m, n):
    return math.comb(m + n - 2, m - 1)


print(gcd_of_list([12, 8, 16]))
print(lcm_of_list([4, 6, 8]))
print(paths_in_grid(3, 3))


19 Modular Arithmetic
Question:
Modular Arithmetic
Many interview problems ask for answers "modulo 10^9 + 7" to avoid integer overflow (though Python handles big ints natively, the mod is still required for correctness against test cases).

Key rules:
```python
MOD = 10**9 + 7
(a + b) % MOD == ((a % MOD) + (b % MOD)) % MOD
(a * b) % MOD == ((a % MOD) * (b % MOD)) % MOD
```

For modular exponentiation: `pow(base, exp, mod)` — Python's built-in 3-argument pow is efficient (O(log exp)).

```python
pow(2, 10, 10**9 + 7)  # 1024
pow(2, 100, 10**9 + 7) # computed efficiently
```

Challenge
Implement `count_subsequences(n)` — number of subsequences of a string of length n (which is 2^n, since each char is included or not). Return answer mod 10^9+7.

Expected output:
count_subsequences(3) → 8
count_subsequences(100) → 976371285

Starter code:
MOD = 10**9 + 7


def count_subsequences(n):
    # TODO: use pow with 3 args
    pass


print(count_subsequences(3))
print(count_subsequences(100))

Solution:
MOD = 10**9 + 7


def count_subsequences(n):
    return pow(2, n, MOD)


print(count_subsequences(3))
print(count_subsequences(100))


20 Ceiling, Floor, and Log
Question:
Ceiling, Floor, and Log
Useful math functions for DSA:

```python
import math

math.ceil(7 / 3)     # 3 (round up)
math.floor(7 / 3)    # 2 (round down)
math.log2(8)         # 3.0
math.log2(16)        # 4.0
math.log(1000, 10)   # 3.0 (log base 10)
```

Integer ceiling without importing math: `(a + b - 1) // b` computes ceil(a/b) for positive integers.

`math.log2(n)` tells you the depth of a balanced binary tree with n nodes, and how many bits are needed.

Challenge
Implement:
- `min_operations(n)` → minimum number of times you must halve n (rounding up each time) to reach 1. Hint: it's ceil(log2(n)).
- `int_ceil_div(a, b)` → ceiling division without using math.ceil

Expected output:
min_operations(8) → 3
min_operations(10) → 4
int_ceil_div(7, 3) → 3
int_ceil_div(9, 3) → 3

Starter code:
import math


def min_operations(n):
    # TODO
    pass

def int_ceil_div(a, b):
    # TODO: no math.ceil
    pass


print(min_operations(8))
print(min_operations(10))
print(int_ceil_div(7, 3))
print(int_ceil_div(9, 3))

Solution:
import math


def min_operations(n):
    return math.ceil(math.log2(n))

def int_ceil_div(a, b):
    return (a + b - 1) // b


print(min_operations(8))
print(min_operations(10))
print(int_ceil_div(7, 3))
print(int_ceil_div(9, 3))


21 Coordinate Math Patterns
Question:
Coordinate Math Patterns
Grid problems constantly use these patterns:

```python
# 4 directional neighbors
directions = [(0, 1), (0, -1), (1, 0), (-1, 0)]

# 8 directional neighbors (including diagonals)
directions_8 = [(dx, dy) for dx in (-1, 0, 1) for dy in (-1, 0, 1) if (dx, dy) != (0, 0)]

# Manhattan distance
def manhattan(p1, p2):
    return abs(p1[0] - p2[0]) + abs(p1[1] - p2[1])

# Check bounds
def in_bounds(r, c, rows, cols):
    return 0 <= r < rows and 0 <= c < cols
```

Challenge
Implement `count_islands(grid)` — given a 2D grid of '1' (land) and '0' (water), count the number of islands. An island is surrounded by water and formed by connecting adjacent lands horizontally or vertically. Use BFS or DFS with the direction pattern.

Expected output:
count_islands([['1','1','0'],['1','1','0'],['0','0','1']]) → 2

Starter code:
from collections import deque


def count_islands(grid):
    # TODO: use direction pattern + BFS/DFS
    pass


grid = [
    ['1', '1', '0', '0', '0'],
    ['1', '1', '0', '0', '0'],
    ['0', '0', '1', '0', '0'],
    ['0', '0', '0', '1', '1']
]
print(count_islands(grid))

Solution:
from collections import deque


def count_islands(grid):
    if not grid:
        return 0
    rows, cols = len(grid), len(grid[0])
    visited = set()
    directions = [(0, 1), (0, -1), (1, 0), (-1, 0)]
    count = 0

    for r in range(rows):
        for c in range(cols):
            if grid[r][c] == '1' and (r, c) not in visited:
                count += 1
                queue = deque([(r, c)])
                visited.add((r, c))
                while queue:
                    cr, cc = queue.popleft()
                    for dr, dc in directions:
                        nr, nc = cr + dr, cc + dc
                        if 0 <= nr < rows and 0 <= nc < cols and grid[nr][nc] == '1' and (nr, nc) not in visited:
                            visited.add((nr, nc))
                            queue.append((nr, nc))
    return count


grid = [
    ['1', '1', '0', '0', '0'],
    ['1', '1', '0', '0', '0'],
    ['0', '0', '1', '0', '0'],
    ['0', '0', '0', '1', '1']
]
print(count_islands(grid))


5 - String Algorithm Tools

22 ord() and chr()
Question:
ord() and chr()
`ord(c)` returns the Unicode code point of character `c`. `chr(n)` returns the character for code point `n`.

```python
ord('a')       # 97
ord('z')       # 122
chr(97)        # 'a'
ord('A')       # 65
ord('0')       # 48
```

Key ranges: lowercase a-z is 97-122, uppercase A-Z is 65-90, digits 0-9 is 48-57.

This is essential for:
- Building frequency arrays (index = ord(c) - ord('a'))
- Caesar cipher-style problems
- Character math

Challenge
Implement:
- `char_frequency(s)` → list of 26 integers, where index i is the count of the (i+1)th lowercase letter
- `caesar_cipher(s, shift)` → shift each lowercase letter by `shift` positions (wrapping around)

Expected output:
char_frequency("abcaab") → [3, 2, 1, 0, 0, ..., 0]
caesar_cipher("abc", 2) → "cde"
caesar_cipher("xyz", 3) → "abc"

Starter code:
def char_frequency(s):
    # TODO: use ord() to build frequency array
    pass

def caesar_cipher(s, shift):
    # TODO: use ord() and chr() with modular arithmetic
    pass


print(char_frequency("abcaab")[:5])
print(caesar_cipher("abc", 2))
print(caesar_cipher("xyz", 3))

Solution:
def char_frequency(s):
    freq = [0] * 26
    for c in s:
        freq[ord(c) - ord('a')] += 1
    return freq

def caesar_cipher(s, shift):
    result = []
    for c in s:
        new_pos = (ord(c) - ord('a') + shift) % 26
        result.append(chr(new_pos + ord('a')))
    return ''.join(result)


print(char_frequency("abcaab")[:5])
print(caesar_cipher("abc", 2))
print(caesar_cipher("xyz", 3))


23 String Classification Methods
Question:
String Classification Methods
Python strings have useful classification methods:

```python
"abc".isalpha()    # True — all alphabetic
"123".isdigit()    # True — all digits
"abc123".isalnum() # True — all alphanumeric
"ABC".isupper()    # True
"abc".islower()    # True
" \t\n".isspace()  # True
```

These are critical for problems like "Valid Palindrome" where you must ignore non-alphanumeric characters:

```python
cleaned = ''.join(c.lower() for c in s if c.isalnum())
```

Challenge
Implement `is_valid_palindrome(s)` that returns True if s is a palindrome considering only alphanumeric characters and ignoring case.

Expected output:
is_valid_palindrome("A man, a plan, a canal: Panama") → True
is_valid_palindrome("race a car") → False

Starter code:
def is_valid_palindrome(s):
    # TODO
    pass


print(is_valid_palindrome("A man, a plan, a canal: Panama"))
print(is_valid_palindrome("race a car"))

Solution:
def is_valid_palindrome(s):
    cleaned = ''.join(c.lower() for c in s if c.isalnum())
    return cleaned == cleaned[::-1]


print(is_valid_palindrome("A man, a plan, a canal: Panama"))
print(is_valid_palindrome("race a car"))


24 String ↔ List Conversion
Question:
String <-> List Conversion
Strings are immutable in Python. To modify characters, convert to a list, mutate, then join back:

```python
s = "hello"
chars = list(s)       # ['h', 'e', 'l', 'l', 'o']
chars[0] = 'H'
result = ''.join(chars)  # "Hello"
```

`''.join(iterable)` is O(n) and is the standard way to build strings from pieces. Avoid `+=` in a loop (it creates a new string each time — O(n²) total).

```python
# Bad — O(n²)
result = ""
for c in chars:
    result += c

# Good — O(n)
result = ''.join(chars)
```

Challenge
Implement `reverse_words(s)` — reverse the order of words in a string. Leading/trailing spaces should be removed, and multiple spaces between words reduced to one.

Expected output:
reverse_words("  the sky  is blue  ") → "blue is sky the"

Starter code:
def reverse_words(s):
    # TODO
    pass


print(reverse_words("  the sky  is blue  "))
print(reverse_words("hello world"))

Solution:
def reverse_words(s):
    words = s.split()
    return ' '.join(words[::-1])


print(reverse_words("  the sky  is blue  "))
print(reverse_words("hello world"))


25 String Building Patterns
Question:
String Building Patterns
Common string building patterns for interviews:

1. **List accumulator + join**: Build pieces in a list, join at the end
2. **StringBuilder equivalent**: Python has no StringBuilder, but list + join IS the equivalent
3. **str.translate / str.maketrans**: Fast character replacement

```python
# Remove vowels efficiently
table = str.maketrans('', '', 'aeiou')
"hello world".translate(table)  # "hll wrld"
```

Also useful: `str.zfill(width)` pads with zeros, `str.ljust/rjust/center` for padding.

Challenge
Implement `encode_string(s)` — run-length encoding. Consecutive repeated characters become the character followed by the count. Single characters have no count.

Expected output:
encode_string("aaabbc") → "a3b2c"
encode_string("abcd") → "abcd"

Starter code:
def encode_string(s):
    # TODO
    pass


print(encode_string("aaabbc"))
print(encode_string("abcd"))
print(encode_string("aabbccdd"))

Solution:
def encode_string(s):
    if not s:
        return ""
    result = []
    count = 1
    for i in range(1, len(s)):
        if s[i] == s[i-1]:
            count += 1
        else:
            result.append(s[i-1])
            if count > 1:
                result.append(str(count))
            count = 1
    result.append(s[-1])
    if count > 1:
        result.append(str(count))
    return ''.join(result)


print(encode_string("aaabbc"))
print(encode_string("abcd"))
print(encode_string("aabbccdd"))


26 String Matching Basics
Question:
String Matching Basics
Python's `in` operator and string methods handle most substring tasks:

```python
"abc" in "xabcy"          # True
"hello".find("ll")        # 2 (index, or -1 if not found)
"hello".index("ll")       # 2 (raises ValueError if not found)
"hello world".count("l")  # 3
"hello".startswith("he")  # True
"hello".endswith("lo")    # True
```

For pattern matching, `re` module is available but rarely needed in DSA interviews. Most problems can be solved with manual scanning.

Challenge
Implement `str_str(haystack, needle)` — return the index of the first occurrence of needle in haystack, or -1 if not found. Do NOT use `.find()` or `in` — implement manual scanning (this is the classic interview version).

Expected output:
str_str("sadbutsad", "sad") → 0
str_str("leetcode", "leeto") → -1

Starter code:
def str_str(haystack, needle):
    # TODO: manual sliding window match
    pass


print(str_str("sadbutsad", "sad"))
print(str_str("leetcode", "leeto"))

Solution:
def str_str(haystack, needle):
    if not needle:
        return 0
    n, m = len(haystack), len(needle)
    for i in range(n - m + 1):
        if haystack[i:i+m] == needle:
            return i
    return -1


print(str_str("sadbutsad", "sad"))
print(str_str("leetcode", "leeto"))


6 - Node Patterns & Graph Setup

27 ListNode Definition
Question:
ListNode Definition
Nearly every linked list problem uses this node class:

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next
```

That's it. Two attributes: a value and a pointer to the next node. Building a linked list:

```python
head = ListNode(1, ListNode(2, ListNode(3)))
# Represents: 1 -> 2 -> 3 -> None
```

Traversal:
```python
curr = head
while curr:
    print(curr.val)
    curr = curr.next
```

Challenge
Implement:
- `build_list(values)` → builds a linked list from a Python list, returns the head
- `to_list(head)` → converts a linked list back to a Python list

Expected output:
to_list(build_list([1, 2, 3, 4])) → [1, 2, 3, 4]

Starter code:
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next


def build_list(values):
    # TODO
    pass

def to_list(head):
    # TODO
    pass


print(to_list(build_list([1, 2, 3, 4])))
print(to_list(build_list([])))

Solution:
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next


def build_list(values):
    if not values:
        return None
    head = ListNode(values[0])
    curr = head
    for v in values[1:]:
        curr.next = ListNode(v)
        curr = curr.next
    return head

def to_list(head):
    result = []
    curr = head
    while curr:
        result.append(curr.val)
        curr = curr.next
    return result


print(to_list(build_list([1, 2, 3, 4])))
print(to_list(build_list([])))


28 Dummy Head Pattern
Question:
Dummy Head Pattern
When building or modifying a linked list, a **dummy node** simplifies edge cases (empty list, inserting at head):

```python
dummy = ListNode(0)
curr = dummy
for val in values:
    curr.next = ListNode(val)
    curr = curr.next
return dummy.next  # skip the dummy
```

Without a dummy, you'd need special handling for the first node. The dummy pattern is used in ~80% of linked list interview solutions.

Challenge
Implement `merge_two_sorted(l1, l2)` — merge two sorted linked lists into one sorted list using the dummy head pattern.

Expected output:
to_list(merge_two_sorted(build_list([1,3,5]), build_list([2,4,6]))) → [1,2,3,4,5,6]

Starter code:
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

def build_list(values):
    if not values:
        return None
    head = ListNode(values[0])
    curr = head
    for v in values[1:]:
        curr.next = ListNode(v)
        curr = curr.next
    return head

def to_list(head):
    result = []
    while head:
        result.append(head.val)
        head = head.next
    return result


def merge_two_sorted(l1, l2):
    # TODO: use dummy head pattern
    pass


print(to_list(merge_two_sorted(build_list([1, 3, 5]), build_list([2, 4, 6]))))
print(to_list(merge_two_sorted(build_list([]), build_list([1, 2]))))

Solution:
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

def build_list(values):
    if not values:
        return None
    head = ListNode(values[0])
    curr = head
    for v in values[1:]:
        curr.next = ListNode(v)
        curr = curr.next
    return head

def to_list(head):
    result = []
    while head:
        result.append(head.val)
        head = head.next
    return result


def merge_two_sorted(l1, l2):
    dummy = ListNode(0)
    curr = dummy
    while l1 and l2:
        if l1.val <= l2.val:
            curr.next = l1
            l1 = l1.next
        else:
            curr.next = l2
            l2 = l2.next
        curr = curr.next
    curr.next = l1 or l2
    return dummy.next


print(to_list(merge_two_sorted(build_list([1, 3, 5]), build_list([2, 4, 6]))))
print(to_list(merge_two_sorted(build_list([]), build_list([1, 2]))))


29 TreeNode Definition
Question:
TreeNode Definition
The standard binary tree node:

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right
```

Building a tree:
```python
root = TreeNode(1, TreeNode(2), TreeNode(3))
#     1
#    / \
#   2   3
```

Most tree problems are solved recursively. The three classic traversals:
- **Inorder** (left, root, right): gives sorted order for BSTs
- **Preorder** (root, left, right): useful for serialization
- **Postorder** (left, right, root): useful for deletion, bottom-up computation

Challenge
Implement all three traversals returning lists of values.

Expected output for tree [1, 2, 3, 4, 5]:
inorder → [4, 2, 5, 1, 3]
preorder → [1, 2, 4, 5, 3]
postorder → [4, 5, 2, 3, 1]

Starter code:
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right


def inorder(root):
    # TODO
    pass

def preorder(root):
    # TODO
    pass

def postorder(root):
    # TODO
    pass


root = TreeNode(1, TreeNode(2, TreeNode(4), TreeNode(5)), TreeNode(3))
print(inorder(root))
print(preorder(root))
print(postorder(root))

Solution:
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right


def inorder(root):
    if not root:
        return []
    return inorder(root.left) + [root.val] + inorder(root.right)

def preorder(root):
    if not root:
        return []
    return [root.val] + preorder(root.left) + preorder(root.right)

def postorder(root):
    if not root:
        return []
    return postorder(root.left) + postorder(root.right) + [root.val]


root = TreeNode(1, TreeNode(2, TreeNode(4), TreeNode(5)), TreeNode(3))
print(inorder(root))
print(preorder(root))
print(postorder(root))


30 Adjacency List Representation
Question:
Adjacency List Representation
Graphs in interviews are almost always represented as adjacency lists:

```python
from collections import defaultdict

graph = defaultdict(list)
edges = [(0, 1), (0, 2), (1, 3), (2, 3)]
for u, v in edges:
    graph[u].append(v)
    graph[v].append(u)  # for undirected graphs
```

Or sometimes as a dict of lists directly:
```python
graph = {0: [1, 2], 1: [0, 3], 2: [0, 3], 3: [1, 2]}
```

BFS template with adjacency list:
```python
from collections import deque

def bfs(graph, start):
    visited = {start}
    queue = deque([start])
    while queue:
        node = queue.popleft()
        for neighbor in graph[node]:
            if neighbor not in visited:
                visited.add(neighbor)
                queue.append(neighbor)
```

Challenge
Implement `shortest_path(n, edges, start, end)` — find the shortest path length in an unweighted undirected graph with n nodes and given edges. Return -1 if no path exists.

Expected output:
shortest_path(5, [(0,1),(0,2),(1,3),(2,3),(3,4)], 0, 4) → 3
shortest_path(4, [(0,1),(2,3)], 0, 3) → -1

Starter code:
from collections import defaultdict, deque


def shortest_path(n, edges, start, end):
    # TODO: build adjacency list, BFS for shortest path
    pass


print(shortest_path(5, [(0,1),(0,2),(1,3),(2,3),(3,4)], 0, 4))
print(shortest_path(4, [(0,1),(2,3)], 0, 3))

Solution:
from collections import defaultdict, deque


def shortest_path(n, edges, start, end):
    graph = defaultdict(list)
    for u, v in edges:
        graph[u].append(v)
        graph[v].append(u)

    visited = {start}
    queue = deque([(start, 0)])
    while queue:
        node, dist = queue.popleft()
        if node == end:
            return dist
        for neighbor in graph[node]:
            if neighbor not in visited:
                visited.add(neighbor)
                queue.append((neighbor, dist + 1))
    return -1


print(shortest_path(5, [(0,1),(0,2),(1,3),(2,3),(3,4)], 0, 4))
print(shortest_path(4, [(0,1),(2,3)], 0, 3))


31 __lt__ for Heaps and Sorting
Question:
__lt__ for Heaps and Sorting
Python's `heapq` compares elements directly. For custom objects, define `__lt__`:

```python
class Task:
    def __init__(self, priority, name):
        self.priority = priority
        self.name = name

    def __lt__(self, other):
        return self.priority < other.priority

import heapq
heap = []
heapq.heappush(heap, Task(3, "low"))
heapq.heappush(heap, Task(1, "high"))
print(heapq.heappop(heap).name)  # "high"
```

Alternative: push tuples like `(priority, tiebreaker, item)` — tuples compare element by element.

Challenge
Implement a priority queue that processes tasks by priority (lower = higher priority), breaking ties by arrival order.

Expected output:
Process order: ["urgent email", "meeting", "lunch"]

Starter code:
import heapq


class TaskQueue:
    def __init__(self):
        self.heap = []
        self.counter = 0

    def add(self, task_name, priority):
        # TODO: push with tie-breaking by arrival order
        pass

    def process_next(self):
        # TODO: pop and return task name
        pass


tq = TaskQueue()
tq.add("lunch", 3)
tq.add("urgent email", 1)
tq.add("meeting", 2)
print([tq.process_next() for _ in range(3)])

Solution:
import heapq


class TaskQueue:
    def __init__(self):
        self.heap = []
        self.counter = 0

    def add(self, task_name, priority):
        heapq.heappush(self.heap, (priority, self.counter, task_name))
        self.counter += 1

    def process_next(self):
        _, _, task_name = heapq.heappop(self.heap)
        return task_name


tq = TaskQueue()
tq.add("lunch", 3)
tq.add("urgent email", 1)
tq.add("meeting", 2)
print([tq.process_next() for _ in range(3)])


32 @dataclass for Quick Structures
Question:
@dataclass for Quick Structures
`@dataclass` auto-generates `__init__`, `__repr__`, and optionally `__eq__` and `__lt__`:

```python
from dataclasses import dataclass

@dataclass
class Point:
    x: int
    y: int

p = Point(3, 4)
print(p)  # Point(x=3, y=4)
```

With `order=True`, it generates comparison methods based on field order:
```python
@dataclass(order=True)
class Event:
    time: int
    name: str

events = [Event(3, "c"), Event(1, "a"), Event(2, "b")]
events.sort()  # sorted by time, then name
```

Challenge
Create a `@dataclass(order=True)` called `Interval` with `start` and `end` fields. Implement `merge_intervals(intervals)` that merges overlapping intervals (sort first, then merge).

Expected output:
merge_intervals([Interval(1,3), Interval(2,6), Interval(8,10), Interval(15,18)])
→ [Interval(start=1, end=6), Interval(start=8, end=10), Interval(start=15, end=18)]

Starter code:
from dataclasses import dataclass


@dataclass(order=True)
class Interval:
    start: int
    end: int


def merge_intervals(intervals):
    # TODO
    pass


intervals = [Interval(1,3), Interval(2,6), Interval(8,10), Interval(15,18)]
print(merge_intervals(intervals))

Solution:
from dataclasses import dataclass


@dataclass(order=True)
class Interval:
    start: int
    end: int


def merge_intervals(intervals):
    if not intervals:
        return []
    intervals.sort()
    merged = [intervals[0]]
    for curr in intervals[1:]:
        if curr.start <= merged[-1].end:
            merged[-1].end = max(merged[-1].end, curr.end)
        else:
            merged.append(curr)
    return merged


intervals = [Interval(1,3), Interval(2,6), Interval(8,10), Interval(15,18)]
print(merge_intervals(intervals))


7 - Bonus: Recursion & Backtracking Setup

33 sys.setrecursionlimit
Question:
sys.setrecursionlimit
Python's default recursion limit is ~1000. For deep recursion (DFS on large graphs, DP with large n), you may need to increase it:

```python
import sys
sys.setrecursionlimit(10000)
```

Be careful: setting it too high can cause a segfault if you actually hit deep recursion. A safer approach is to convert to iteration when possible.

Check current limit:
```python
sys.getrecursionlimit()  # default: 1000
```

Challenge
Implement `deep_sum(n)` that recursively sums 1+2+...+n. Test it with n=5000 (which exceeds default limit). Set the recursion limit appropriately.

Expected output:
deep_sum(5000) → 12502500

Starter code:
import sys

# TODO: set recursion limit


def deep_sum(n):
    # TODO: recursive sum
    pass


print(deep_sum(5000))

Solution:
import sys
sys.setrecursionlimit(6000)


def deep_sum(n):
    if n <= 0:
        return 0
    return n + deep_sum(n - 1)


print(deep_sum(5000))


34 Backtracking Template
Question:
Backtracking Template
Backtracking explores choices recursively, undoing ("backtracking") when a path fails:

```python
def backtrack(state, choices):
    if is_goal(state):
        results.append(state.copy())
        return
    for choice in choices:
        if is_valid(choice, state):
            state.add(choice)          # make choice
            backtrack(state, choices)   # explore
            state.remove(choice)        # undo choice
```

The key insight: you mutate state, recurse, then undo the mutation. This avoids creating copies at every level.

Challenge
Implement `permutations(nums)` using backtracking — return all permutations of the input list.

Expected output:
permutations([1, 2, 3]) → [[1,2,3], [1,3,2], [2,1,3], [2,3,1], [3,1,2], [3,2,1]]

Starter code:
def permutations(nums):
    result = []

    def backtrack(path, remaining):
        # TODO
        pass

    backtrack([], nums)
    return result


print(permutations([1, 2, 3]))

Solution:
def permutations(nums):
    result = []

    def backtrack(path, remaining):
        if not remaining:
            result.append(path[:])
            return
        for i in range(len(remaining)):
            path.append(remaining[i])
            backtrack(path, remaining[:i] + remaining[i+1:])
            path.pop()

    backtrack([], nums)
    return result


print(permutations([1, 2, 3]))


35 copy.deepcopy for State Snapshots
Question:
copy.deepcopy for State Snapshots
When your state is a nested structure (list of lists, dict of lists), a shallow copy isn't enough:

```python
import copy

grid = [[1, 2], [3, 4]]
shallow = grid[:]            # shares inner lists!
deep = copy.deepcopy(grid)   # fully independent

shallow[0][0] = 99
print(grid[0][0])  # 99 — corrupted!

deep[0][0] = 99
print(grid[0][0])  # 1 — safe
```

In backtracking, use `deepcopy` when you need to snapshot complex state. But prefer mutation + undo when possible (it's faster).

Challenge
Implement `solve_n_queens(n)` — return all solutions for placing n queens on an n×n board so no two attack each other. Return each solution as a list of strings where 'Q' is a queen and '.' is empty.

Expected output:
solve_n_queens(4) → 2 solutions

Starter code:
def solve_n_queens(n):
    results = []

    def backtrack(row, cols, diag1, diag2, board):
        # TODO
        pass

    backtrack(0, set(), set(), set(), [])
    return results


solutions = solve_n_queens(4)
print(f"Found {len(solutions)} solutions")
for sol in solutions:
    for row in sol:
        print(row)
    print()

Solution:
def solve_n_queens(n):
    results = []

    def backtrack(row, cols, diag1, diag2, board):
        if row == n:
            results.append([''.join(r) for r in board])
            return
        for col in range(n):
            if col in cols or (row - col) in diag1 or (row + col) in diag2:
                continue
            board.append(['.' * col + 'Q' + '.' * (n - col - 1)])
            cols.add(col)
            diag1.add(row - col)
            diag2.add(row + col)
            backtrack(row + 1, cols, diag1, diag2, board)
            board.pop()
            cols.remove(col)
            diag1.remove(row - col)
            diag2.remove(row + col)

    backtrack(0, set(), set(), set(), [])
    return results


solutions = solve_n_queens(4)
print(f"Found {len(solutions)} solutions")
for sol in solutions:
    for row in sol:
        print(row)
    print()


36 Converting Recursion to Iteration
Question:
Converting Recursion to Iteration
Any recursion can be converted to iteration using an explicit stack. This avoids stack overflow and is often required in interviews:

```python
# Recursive DFS
def dfs_recursive(node):
    if not node:
        return
    process(node)
    dfs_recursive(node.left)
    dfs_recursive(node.right)

# Iterative DFS (preorder)
def dfs_iterative(root):
    stack = [root]
    while stack:
        node = stack.pop()
        if not node:
            continue
        process(node)
        stack.append(node.right)  # right first so left is processed first
        stack.append(node.left)
```

Challenge
Implement iterative inorder traversal of a binary tree (left, root, right) using an explicit stack.

Expected output for tree [1, 2, 3, 4, 5]:
iterative_inorder → [4, 2, 5, 1, 3]

Starter code:
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right


def iterative_inorder(root):
    # TODO: use explicit stack
    pass


root = TreeNode(1, TreeNode(2, TreeNode(4), TreeNode(5)), TreeNode(3))
print(iterative_inorder(root))

Solution:
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right


def iterative_inorder(root):
    result = []
    stack = []
    curr = root
    while curr or stack:
        while curr:
            stack.append(curr)
            curr = curr.left
        curr = stack.pop()
        result.append(curr.val)
        curr = curr.right
    return result


root = TreeNode(1, TreeNode(2, TreeNode(4), TreeNode(5)), TreeNode(3))
print(iterative_inorder(root))


37 Tuple Comparison for Multi-Criteria
Question:
Tuple Comparison for Multi-Criteria
Python tuples compare element-by-element, which is perfect for multi-criteria sorting and heap operations:

```python
tasks = [(3, "low"), (1, "high"), (2, "med"), (1, "also high")]
tasks.sort()
# [(1, 'also high'), (1, 'high'), (2, 'med'), (3, 'low')]
```

This is why `heapq` works with tuples — it pops the smallest tuple, comparing first element, then second on ties, etc.

For sorting by one criteria ascending and another descending, negate the descending field:
```python
# Sort by score descending, name ascending
students.sort(key=lambda s: (-s.score, s.name))
```

Challenge
Implement `k_closest_points(points, k)` — given a list of (x, y) points, return the k closest to origin (0, 0). Use a heap with distance tuples.

Expected output:
k_closest_points([(3,3), (5,-1), (-2,4), (1,1)], 2) → [(1,1), (3,3)] or [(1,1), (-2,4)]

Starter code:
import heapq


def k_closest_points(points, k):
    # TODO: use heap with (distance, point) tuples
    pass


print(k_closest_points([(3, 3), (5, -1), (-2, 4), (1, 1)], 2))

Solution:
import heapq


def k_closest_points(points, k):
    heap = []
    for x, y in points:
        dist = x * x + y * y
        heapq.heappush(heap, (dist, (x, y)))
    return [heapq.heappop(heap)[1] for _ in range(k)]


print(k_closest_points([(3, 3), (5, -1), (-2, 4), (1, 1)], 2))


38 Practical Interview Setup
Question:
Practical Interview Setup
In a real coding interview, you often need to combine several tools. Here's a checklist of what to set up mentally:

1. **Import what you need**: `from collections import defaultdict, deque, Counter`
2. **Define node classes** if the problem involves linked lists or trees
3. **Choose your approach**: brute force first, optimize after
4. **Think about edge cases**: empty input, single element, duplicates
5. **State your complexity** before coding

Common imports for interviews:
```python
from collections import defaultdict, deque, Counter
from functools import cache, lru_cache
from bisect import bisect_left, bisect_right, insort
from heapq import heappush, heappop, heapify
import math
```

Challenge
Implement `top_k_frequent(nums, k)` — return the k most frequent elements. Use Counter + heap. O(n log k) time.

Expected output:
top_k_frequent([1,1,1,2,2,3], 2) → [1, 2]
top_k_frequent([1], 1) → [1]

Starter code:
from collections import Counter
from heapq import nlargest


def top_k_frequent(nums, k):
    # TODO
    pass


print(top_k_frequent([1, 1, 1, 2, 2, 3], 2))
print(top_k_frequent([1], 1))

Solution:
from collections import Counter
from heapq import nlargest


def top_k_frequent(nums, k):
    freq = Counter(nums)
    return nlargest(k, freq.keys(), key=freq.get)


print(top_k_frequent([1, 1, 1, 2, 2, 3], 2))
print(top_k_frequent([1], 1))
