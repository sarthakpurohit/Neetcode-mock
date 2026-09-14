# Neetcode-mock

Interactive **Jupyter notebook** courses for learning Python with an eye toward **coding interviews** and **system design**. The material is inspired by [NeetCode](https://neetcode.io/) and expanded with extra sections and exercises.

Across four tracks you get **217 numbered challenges** in **36 notebooks**:

| Track | Challenge IDs | Notebooks |
| --- | --- | --- |
| **Python for Beginners** | 0–92 (93 challenges) | 13 |
| **Python for Coding Interviews** | 0–43 (44 challenges) | 9 |
| **Python for OOP** | 0–40 (41 challenges) | 7 |
| **Python DSA Toolkit** | 0–38 (39 challenges) | 7 |

Each notebook is one section: markdown explanations, starter code (often `# TODO` or `pass`), and collapsible **Show Solution** blocks when you are ready to compare.

## How to use

1. Open this folder in **Cursor**, **VS Code**, or **JupyterLab**.
2. Pick a notebook below (links open the file in your editor or notebook UI).
3. Read the markdown cells, then edit the **starter code** cell for each challenge.
4. Run the cell (**Shift + Enter** in Jupyter / VS Code) and check the output.
5. Expand **Show Solution** only after you have tried the problem yourself.

**Beginners note:** The first sections of *Python for Beginners* include a few **intentionally broken** starter cells (bad quotes, illegal names, and so on) so you can practice reading `SyntaxError` messages. That is deliberate until you fix them per the challenge text.

**Authoring:** Each course folder also contains an `info.md` file that was used as the source outline (free challenges preserved verbatim where applicable; additional titles were expanded into full notebook content).

---

## Python for Beginners

Foundations: variables, control flow, collections, stdin, exceptions, plus a **bonus** DSA-prep module (recursion, comprehensions, `collections`, Big-O, and more).

| # | Notebook | Challenges | Topics |
| --- | --- | --- | --- |
| 1 | [Introduction](Python-for-Beginners/01_Introduction.ipynb) | 0–5 | Hello World, what Python is, execution order, printing text, code errors, comments |
| 2 | [Variables](Python-for-Beginners/02_Variables.ipynb) | 6–15 | Declaration, naming, conventions, reassignment, multiple assignment, types, casting, `None` |
| 3 | [Math](Python-for-Beginners/03_Math.ipynb) | 16–21 | Arithmetic, comparisons, shorthand operators, booleans |
| 4 | [Functions](Python-for-Beginners/04_Functions.ipynb) | 22–30 | Defining functions, parameters, return, type hints, scope, defaults |
| 5 | [Conditional statements](Python-for-Beginners/05_Conditional_Statements.ipynb) | 31–37 | `if` / `elif` / `else`, logic, truthy and falsy values |
| 6 | [Loops](Python-for-Beginners/06_Loops.ipynb) | 38–46 | `while`, `for`, `range`, nesting, `break` / `continue` / `pass` |
| 7 | [Strings](Python-for-Beginners/07_Strings.ipynb) | 47–56 | `len`, indexing, looping, concatenation, slicing, reversing, immutability, formatting |
| 8 | [Lists](Python-for-Beginners/08_Lists.ipynb) | 57–65 | Creating lists, methods, looping, slicing, tuples |
| 9 | [Sets](Python-for-Beginners/09_Sets.ipynb) | 66–68 | Uniqueness, unions, intersections, differences |
| 10 | [Dictionaries](Python-for-Beginners/10_Dictionaries.ipynb) | 69–74 | Key–value usage, looping, frequency counting, comprehensions |
| 11 | [Reading stdin](Python-for-Beginners/11_Reading_Stdin.ipynb) | 75–78 | `input()`, parsing, multi-line input |
| 12 | [Exception handling](Python-for-Beginners/12_Exception_Handling.ipynb) | 79–81 | `try` / `except`, specific exceptions, multiple handlers |
| 13 | [Bonus: DSA prep](Python-for-Beginners/13_Bonus_DSA_Prep.ipynb) | 82–92 | Recursion, comprehensions, generators, `lambda`, `map` / `filter`, sorting, `collections`, `itertools`, Big-O |

---

## Python for Coding Interviews

Python idioms and built-ins you reach for in interviews: sorting, comprehensions, stacks, queues, grids, hash maps, heaps, ordered structures, and common patterns.

| # | Notebook | Challenges | Topics |
| --- | --- | --- | --- |
| 1 | [Sorting](Python-for-Coding-Interviews/01_Sorting.ipynb) | 0–4 | `list.sort`, `sorted`, `reverse`, `key`, lambdas, non-mutating sort |
| 2 | [Pythonic code](Python-for-Coding-Interviews/02_Pythonic_Code.ipynb) | 5–10 | Unpacking, `enumerate`, `zip`, chained comparisons, `min` / `max` with `key` |
| 3 | [Lists](Python-for-Coding-Interviews/03_Lists.ipynb) | 11–16 | Dynamic lists, concatenation, matrix init, cloning, comprehensions |
| 4 | [Stacks and queues](Python-for-Coding-Interviews/04_Stacks_and_Queues.ipynb) | 17–19 | List-as-stack, `deque` as queue, `deque.rotate` |
| 5 | [2D lists](Python-for-Coding-Interviews/05_2D_Lists.ipynb) | 20–22 | Grid shape, neighbor sums, nested comprehensions |
| 6 | [Hash maps and hash sets](Python-for-Coding-Interviews/06_Hashmaps_and_Hashsets.ipynb) | 23–30 | `dict`, `defaultdict`, `Counter`, set patterns, tuple keys |
| 7 | [Heaps](Python-for-Coding-Interviews/07_Heaps.ipynb) | 31–37 | `heapq`, `heapify`, kth largest, tuples in heaps, `nsmallest` / `nlargest` |
| 8 | [Sorted dicts and sorted sets](Python-for-Coding-Interviews/08_Sorted_Dicts_and_Sorted_Sets.ipynb) | 38–39 | Ordered keys and unique values with `bisect` |
| 9 | [Bonus: interview patterns](Python-for-Coding-Interviews/09_Bonus_Interview_Patterns.ipynb) | 40–43 | Two pointers, sliding anagram window, Big-O warm-ups, `itertools.product` |

---

## Python for OOP

Classes, encapsulation, inheritance, polymorphism, abstraction, and a **bonus** module tying patterns to design-style interview discussion.

| # | Notebook | Challenges | Topics |
| --- | --- | --- | --- |
| 1 | [Classes and objects](Python-for-OOP/01_Classes_And_Objects.ipynb) | 0–8 | Classes, instances, attributes, methods, `self`, `__init__`, docstrings |
| 2 | [Encapsulation](Python-for-OOP/02_Encapsulation.ipynb) | 9–15 | Public vs internal state, `_` / `__`, properties |
| 3 | [Class attributes](Python-for-OOP/03_Class_Attributes.ipynb) | 16–20 | Class vs instance state, `@classmethod`, `@staticmethod` |
| 4 | [Inheritance](Python-for-OOP/04_Inheritance.ipynb) | 21–26 | Subclassing, `super()`, multiple inheritance, MRO |
| 5 | [Polymorphism](Python-for-OOP/05_Polymorphism.ipynb) | 27–31 | Shared interfaces, duck typing, overload-style defaults |
| 6 | [Abstraction](Python-for-OOP/06_Abstraction.ipynb) | 32–36 | `ABC`, `@abstractmethod`, contracts across subtypes |
| 7 | [Bonus: design interview prep](Python-for-OOP/07_Bonus_Design_Interview_Prep.ipynb) | 37–40 | SOLID-style composition, factory, strategy, dependency injection |

---

## Python DSA Toolkit

The Python-specific implementation tools and patterns you'll use constantly when solving algorithm problems. Bridges the gap between "I know Python" and "I'm implementing Dijkstra's in Python."

| # | Notebook | Challenges | Topics |
| --- | --- | --- | --- |
| 1 | [Memoization & Caching](Python-DSA-Toolkit/01_Memoization_and_Caching.ipynb) | 0–5 | Dict memoization, `@cache`, `@lru_cache`, tuple keys, tabulation, space optimization |
| 2 | [Binary Search Utilities](Python-DSA-Toolkit/02_Binary_Search_Utilities.ipynb) | 6–10 | `bisect_left`, `bisect_right`, `insort`, custom binary search template, search on answer |
| 3 | [Bit Manipulation](Python-DSA-Toolkit/03_Bit_Manipulation.ipynb) | 11–16 | Bitwise operators, `bin()`/`int()`, XOR patterns, bitmask subsets, bit tricks |
| 4 | [Math Utilities](Python-DSA-Toolkit/04_Math_Utilities.ipynb) | 17–21 | `math.inf`, GCD/LCM, `math.comb`, modular arithmetic, `pow(b,e,m)`, coordinate math |
| 5 | [String Algorithm Tools](Python-DSA-Toolkit/05_String_Algorithm_Tools.ipynb) | 22–26 | `ord()`/`chr()`, frequency arrays, `isalnum()`, string↔list, run-length encoding, `str_str` |
| 6 | [Node Patterns & Graph Setup](Python-DSA-Toolkit/06_Node_Patterns_and_Graph_Setup.ipynb) | 27–32 | `ListNode`, dummy head, `TreeNode`, adjacency lists, `__lt__` for heaps, `@dataclass` |
| 7 | [Bonus: Recursion & Backtracking](Python-DSA-Toolkit/07_Bonus_Recursion_and_Backtracking.ipynb) | 33–38 | `sys.setrecursionlimit`, backtracking template, `deepcopy`, iterative conversion, tuple comparison, interview setup |

---

## Suggested order

1. **Python for Beginners** — run front to back (or skip ahead if you already know a topic).
2. **Python for Coding Interviews** — best after you are comfortable with lists, dicts, and functions.
3. **Python for OOP** — can overlap with interview prep once basics are solid; useful before system design rounds that emphasize APIs and extensibility.
4. **Python DSA Toolkit** — complete before starting dedicated DSA courses; gives you all the Python-specific implementation tools.

After these tracks, you are ready for dedicated **DSA** courses (e.g. NeetCode's *Algorithms and Data Structures for Beginners* → *Advanced Algorithms*).
