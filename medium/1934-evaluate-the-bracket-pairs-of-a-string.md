# Evaluate the Bracket Pairs of a String

## Problem Link
[LeetCode - Evaluate the Bracket Pairs of a String](https://leetcode.com/problems/evaluate-the-bracket-pairs-of-a-string/)

## Difficulty
Medium

## Problem Description
<p>You are given a string <code>s</code> that contains some bracket pairs, with each pair containing a <strong>non-empty</strong> key.</p>

<ul>
	<li>For example, in the string <code>&quot;(name)is(age)yearsold&quot;</code>, there are <strong>two</strong> bracket pairs that contain the keys <code>&quot;name&quot;</code> and <code>&quot;age&quot;</code>.</li>
</ul>

<p>You know the values of a wide range of keys. This is represented by a 2D string array <code>knowledge</code> where each <code>knowledge[i] = [key<sub>i</sub>, value<sub>i</sub>]</code> indicates that key <code>key<sub>i</sub></code> has a value of <code>value<sub>i</sub></code>.</p>

<p>You are tasked to evaluate <strong>all</strong> of the bracket pairs. When you evaluate a bracket pair that contains some key <code>key<sub>i</sub></code>, you will:</p>

<ul>
	<li>Replace <code>key<sub>i</sub></code> and the bracket pair with the key&#39;s corresponding <code>value<sub>i</sub></code>.</li>
	<li>If you do not know the value of the key, you will replace <code>key<sub>i</sub></code> and the bracket pair with a question mark <code>&quot;?&quot;</code> (without the quotation marks).</li>
</ul>

<p>Each key will appear at most once in your <code>knowledge</code>. There will not be any nested brackets in <code>s</code>.</p>

<p>Return <em>the resulting string after evaluating <strong>all</strong> of the bracket pairs.</em></p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;(name)is(age)yearsold&quot;, knowledge = [[&quot;name&quot;,&quot;bob&quot;],[&quot;age&quot;,&quot;two&quot;]]
<strong>Output:</strong> &quot;bobistwoyearsold&quot;
<strong>Explanation:</strong>
The key &quot;name&quot; has a value of &quot;bob&quot;, so replace &quot;(name)&quot; with &quot;bob&quot;.
The key &quot;age&quot; has a value of &quot;two&quot;, so replace &quot;(age)&quot; with &quot;two&quot;.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;hi(name)&quot;, knowledge = [[&quot;a&quot;,&quot;b&quot;]]
<strong>Output:</strong> &quot;hi?&quot;
<strong>Explanation:</strong> As you do not know the value of the key &quot;name&quot;, replace &quot;(name)&quot; with &quot;?&quot;.
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;(a)(a)(a)aaa&quot;, knowledge = [[&quot;a&quot;,&quot;yes&quot;]]
<strong>Output:</strong> &quot;yesyesyesaaa&quot;
<strong>Explanation:</strong> The same key can appear multiple times.
The key &quot;a&quot; has a value of &quot;yes&quot;, so replace all occurrences of &quot;(a)&quot; with &quot;yes&quot;.
Notice that the &quot;a&quot;s not in a bracket pair are not evaluated.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 10<sup>5</sup></code></li>
	<li><code>0 &lt;= knowledge.length &lt;= 10<sup>5</sup></code></li>
	<li><code>knowledge[i].length == 2</code></li>
	<li><code>1 &lt;= key<sub>i</sub>.length, value<sub>i</sub>.length &lt;= 10</code></li>
	<li><code>s</code> consists of lowercase English letters and round brackets <code>&#39;(&#39;</code> and <code>&#39;)&#39;</code>.</li>
	<li>Every open bracket <code>&#39;(&#39;</code> in <code>s</code> will have a corresponding close bracket <code>&#39;)&#39;</code>.</li>
	<li>The key in each bracket pair of <code>s</code> will be non-empty.</li>
	<li>There will not be any nested bracket pairs in <code>s</code>.</li>
	<li><code>key<sub>i</sub></code> and <code>value<sub>i</sub></code> consist of lowercase English letters.</li>
	<li>Each <code>key<sub>i</sub></code> in <code>knowledge</code> is unique.</li>
</ul>


## Test Cases
```
"(name)is(age)yearsold"
[["name","bob"],["age","two"]]
"hi(name)"
[["a","b"]]
"(a)(a)(a)aaa"
[["a","yes"]]
```

## Initial Template
```python
# Code template not available
```

## Solution
1. Initial Thoughts:
   - The problem asks us to replace bracket pairs in a string `s` with their corresponding values from a `knowledge` array. 
   - If a key within a bracket pair is not found in `knowledge`, we replace it with "?".
   - No nested brackets simplifies things. We can iterate through the string and handle each bracket pair individually.
   - A hash map (dictionary in Python) seems like a good way to store the `knowledge` for fast lookups.

2. Solution Implementation:
```python
def evaluate(s: str, knowledge: list[list[str]]) -> str:
    """
    Evaluates bracket pairs in a string based on a knowledge base.

    Args:
        s: The input string with bracket pairs.
        knowledge: A list of key-value pairs.

    Returns:
        The resulting string after evaluating the bracket pairs.
    """

    knowledge_map = {key: value for key, value in knowledge} # Create a dictionary for O(1) key lookups
    result = []
    i = 0
    while i < len(s):
        if s[i] == '(':  # Start of a bracket pair
            j = i + 1
            key = ""
            while j < len(s) and s[j] != ')': # Extract the key
                key += s[j]
                j += 1
            
            if key in knowledge_map:
                result.append(knowledge_map[key]) # Replace with the value
            else:
                result.append("?") # Replace with "?" if key not found
            i = j + 1 # Skip the entire bracket pair
        else:
            result.append(s[i]) # Append characters outside bracket pairs
            i += 1

    return "".join(result) # Join the characters to form the final string
```

3. Solution Explanation:
   - We first create a dictionary `knowledge_map` from the `knowledge` list. This allows us to look up values by key in O(1) time.
   - We iterate through the string `s` character by character.
   - When we encounter an opening bracket '(', we extract the key within the brackets.
   - We then check if the key exists in `knowledge_map`. If it does, we append the corresponding value to the `result` list. Otherwise, we append "?".
   - We skip the entire bracket pair in the input string.
   - For characters outside bracket pairs, we simply append them to the `result` list.
   - Finally, we join the characters in the `result` list to form the output string.

4. Complexity Analysis:
   - Time complexity: O(N + M) - where N is the length of `s` and M is the length of `knowledge`. We iterate through both `s` and `knowledge` once.  Dictionary lookups are O(1) on average.
   - Space complexity: O(M + N) -  The `knowledge_map` dictionary takes O(M) space to store the key-value pairs. In the worst case (all characters are outside brackets), the `result` list could take up to O(N) space. Therefore, the overall space complexity is O(M + N).




## Topics
Array, Hash Table, String

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-03-27
