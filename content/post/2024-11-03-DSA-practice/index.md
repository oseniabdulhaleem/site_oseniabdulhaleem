---
title: "Practicing DSA: Using the `cycle` Method in Python"
subtitle: "Exploring Efficient Solutions for Repeating Iterations"
description: "Learning about Python’s `cycle` method for cyclic iteration"
date: 2024-11-03
author: "oseniabdulhaleem"
tags: ["DSA", "Python", "Algorithms"]
categories: ["Tech"]
---

In a recent problem on Codewars, I tackled a challenge that required creating a looper function. This function would return individual letters from a string in a cyclic manner, returning each letter one at a time and starting over when it reaches the end. Here’s the **Codewars kata** for reference:

[Link to the kata](https://www.codewars.com/kata/51fc3beb41ecc97ee20000c3)

Below, I’ll share my initial solution, how I refined it, and how I discovered the power of Python’s `cycle` method from `itertools` to simplify the solution further.

## Initial Solution: Creating a Looper Function

Here’s my first approach to solving the problem:

```python
def make_looper(string):
    global return_tracker
    global letters
    return_tracker = -1
    letters = [val for val in string]
    return abc

def abc():
    global return_tracker
    letters_len = len(letters)
    if return_tracker == letters_len - 1:
        return_tracker = -1
    while True:
        return_tracker += 1
        return letters[return_tracker]

# Testing the function
dao = make_looper("folake")
for _ in range(10):
    print(dao())

```

## Observations

- Global Variables: I used global to make return_tracker and letters accessible in both functions. However, using global variables can lead to messy code, especially for simple functions.

- Unnecessary While Loop: The while True loop in abc() was redundant because the function exits immediately after return is called.

## Refining the Solution for Readability

To make the code more efficient and readable, I eliminated the while loop and avoided global variables by restructuring the abc function as a nested function inside make_looper:

```python

def make_looper(string):
    return_tracker = -1
    letters = [val for val in string]

    def abc():
        nonlocal return_tracker
        letters_len = len(letters)
        return_tracker += 1
        if return_tracker >= letters_len:
            return_tracker = 0  # Reset to the beginning
        return letters[return_tracker]

    return abc

```

In this version:

- Nonlocal Keyword: nonlocal return_tracker allows abc to modify return_tracker in the enclosing scope of make_looper.
- Cleaner Flow: The function now resets and loops through the string naturally without redundant code.

## Optimal Solution: Using itertools.cycle

While browsing solutions, I found an elegant approach that used itertools.cycle to cycle through characters effortlessly:

```python

from itertools import cycle

def make_looper(s):
    g = cycle(s)
    return lambda: next(g)

```

With cycle, we no longer need to handle indexes or resetting manually. Here’s how it works:

- cycle(s): cycle creates an iterator that loops over s infinitely.
- next(g): Each call to next(g) retrieves the next character in s and automatically loops back when it reaches the end.

### Practical Uses of cycle

The cycle method is useful beyond this problem. Here are some scenarios where cycle can simplify your code:

## Round-Robin Task Scheduling

When distributing tasks evenly across servers or workers, cycle lets you rotate through a list repeatedly:

```
from itertools import cycle

servers = ["Server1", "Server2", "Server3"]
task_scheduler = cycle(servers)

for task in range(10):  # Assign 10 tasks
    assigned_server = next(task_scheduler)
    print(f"Task {task} assigned to {assigned_server}")

```

Overall, learning about itertools.cycle has helped me write more concise and expressive code. It’s a great tool for handling repetitive sequences without complex logic, just like in my make_looper function! 😊
