# Allow One Function Call

## Problem Link
[LeetCode - Allow One Function Call](https://leetcode.com/problems/allow-one-function-call/)

## Difficulty
Easy

## Problem Description
<p>Given a function <code>fn</code>, return a new function that is identical to the original function except that it ensures&nbsp;<code>fn</code>&nbsp;is&nbsp;called at most once.</p>

<ul>
	<li>The first time the returned function is called, it should return the same result as&nbsp;<code>fn</code>.</li>
	<li>Every subsequent time it is called, it should return&nbsp;<code>undefined</code>.</li>
</ul>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> fn = (a,b,c) =&gt; (a + b + c), calls = [[1,2,3],[2,3,6]]
<strong>Output:</strong> [{&quot;calls&quot;:1,&quot;value&quot;:6}]
<strong>Explanation:</strong>
const onceFn = once(fn);
onceFn(1, 2, 3); // 6
onceFn(2, 3, 6); // undefined, fn was not called
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> fn = (a,b,c) =&gt; (a * b * c), calls = [[5,7,4],[2,3,6],[4,6,8]]
<strong>Output:</strong> [{&quot;calls&quot;:1,&quot;value&quot;:140}]
<strong>Explanation:</strong>
const onceFn = once(fn);
onceFn(5, 7, 4); // 140
onceFn(2, 3, 6); // undefined, fn was not called
onceFn(4, 6, 8); // undefined, fn was not called
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>calls</code> is a valid JSON array</li>
	<li><code>1 &lt;= calls.length &lt;= 10</code></li>
	<li><code>1 &lt;= calls[i].length &lt;= 100</code></li>
	<li><code>2 &lt;= JSON.stringify(calls).length &lt;= 1000</code></li>
</ul>


## Test Cases
```
(a,b,c) => (a + b + c)
[[1,2,3],[2,3,6]]
(a,b,c) => (a * b * c)
[[5,7,4],[2,3,6],[4,6,8]]
```

## Initial Template
```python
# Code template not available
```

## Solution
1. Initial Thoughts:
   - The problem asks us to create a higher-order function `once` that takes a function `fn` as input and returns a new function.
   - This new function should behave exactly like `fn` the first time it's called.  
   - On subsequent calls, it should return `undefined`.
   - This is a classic example where we can use a closure to keep track of whether the function has been called before. We can use a boolean variable inside the closure to achieve this.

2. Solution Implementation:
```python
def once(fn):
    """
    Returns a new function that's identical to fn except that it ensures fn is called at most once.

    Args:
        fn: The function to be wrapped.

    Returns:
        A new function that calls fn at most once.
    """
    called = False  # Keep track of whether fn has been called

    def inner(*args, **kwargs):
        nonlocal called  # Important! We need nonlocal to modify the closure variable
        if not called:
            called = True
            return fn(*args, **kwargs)
            

    return inner
```

3. Solution Explanation:
   - The `once` function takes the original function `fn` as an argument.
   - Inside `once`, we define a nested function `inner`. This `inner` function is the one that will be returned.
   - We initialize a boolean variable `called` to `False` inside `once`. This variable will be enclosed within the `inner` function's scope.
   - When `inner` is called, it checks the value of `called`.
   - If `called` is `False` (meaning `fn` hasn't been called yet), we set `called` to `True` and then call `fn` with the provided arguments using `*args` and `**kwargs` to handle any number of positional and keyword arguments.  The result of `fn` is returned.
   - If `called` is `True` (meaning `fn` has already been called), we simply return `None` which is the Python equivalent of `undefined`.
   - The `nonlocal called` statement is crucial.  Without it, the `called = True` assignment inside `inner` would create a new local variable named `called` within `inner` instead of modifying the `called` variable in the enclosing scope of `once`.

4. Complexity Analysis:
   - Time complexity: O(1) - The overhead of the `once` function and the `inner` function is constant. The time complexity is dominated by the call to `fn`, which we assume to be constant in this analysis.
   - Space complexity: O(1) - We use a constant amount of extra space to store the `called` variable.  The space complexity of calling `fn` is not considered here.


## Topics


## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-02-28
