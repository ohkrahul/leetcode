# Rearrange Words in a Sentence

## Problem Link
[LeetCode - Rearrange Words in a Sentence](https://leetcode.com/problems/rearrange-words-in-a-sentence/)

## Difficulty
Medium

## Problem Description
<p>Given a sentence&nbsp;<code>text</code> (A&nbsp;<em>sentence</em>&nbsp;is a string of space-separated words) in the following format:</p>

<ul>
	<li>First letter is in upper case.</li>
	<li>Each word in <code>text</code> are separated by a single space.</li>
</ul>

<p>Your task is to rearrange the words in text such that&nbsp;all words are rearranged in an increasing order of their lengths. If two words have the same length, arrange them in their original order.</p>

<p>Return the new text&nbsp;following the format shown above.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> text = &quot;Leetcode is cool&quot;
<strong>Output:</strong> &quot;Is cool leetcode&quot;
<strong>Explanation: </strong>There are 3 words, &quot;Leetcode&quot; of length 8, &quot;is&quot; of length 2 and &quot;cool&quot; of length 4.
Output is ordered by length and the new first word starts with capital letter.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> text = &quot;Keep calm and code on&quot;
<strong>Output:</strong> &quot;On and keep calm code&quot;
<strong>Explanation: </strong>Output is ordered as follows:
&quot;On&quot; 2 letters.
&quot;and&quot; 3 letters.
&quot;keep&quot; 4 letters in case of tie order by position in original text.
&quot;calm&quot; 4 letters.
&quot;code&quot; 4 letters.
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> text = &quot;To be or not to be&quot;
<strong>Output:</strong> &quot;To be or to be not&quot;
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>text</code> begins with a capital letter and then contains lowercase letters and single space between words.</li>
	<li><code>1 &lt;= text.length &lt;= 10^5</code></li>
</ul>


## Test Cases
```
"Leetcode is cool"
"Keep calm and code on"
"To be or not to be"
```

## Initial Template
```python
# Code template not available
```

## Solution
1. Initial Thoughts:
   - Problem analysis: We need to split the input sentence into words, sort them based on length, and then reconstruct the sentence with the first letter capitalized.  We need to maintain the original order for words with the same length.
   - Key observations: We can use Python's built-in sorting capabilities.  A tuple containing (length, original_index, word) would be useful for sorting while preserving original word order for ties.
   - Possible approaches: Split the string into a list of words, create a list of tuples as described above, sort, then rebuild the string.

2. Solution Implementation:
```python
def arrangeWords(text: str) -> str:
    """
    Rearranges words in a sentence in increasing order of their lengths.

    Args:
        text: The input sentence.

    Returns:
        The rearranged sentence.
    """
    words = text.split()  # Split the sentence into words
    n = len(words)

    # Create a list of tuples (word length, original index, word)
    word_tuples = []
    for i in range(n):
        word_tuples.append((len(words[i]), i, words[i].lower())) # Store words in lowercase

    # Sort based on length, then original index for tie-breaking
    word_tuples.sort()

    # Reconstruct the sentence
    res = ""
    for i in range(n):
        res += word_tuples[i][2] + " "

    # Capitalize the first letter and remove trailing space
    res = res[0].upper() + res[1:-1]

    return res

```

3. Solution Explanation:
   - The `arrangeWords` function first splits the input `text` into a list of words.
   - Then, it creates a list of tuples where each tuple contains the word's length, its original index, and the lowercase version of the word.  Storing the original index allows us to maintain the original order for words of the same length.  Converting to lowercase simplifies the final capitalization step.
   - The `word_tuples` list is then sorted. Python's sort function will automatically sort by the elements of the tuple in order.  
   - The sorted tuples are used to reconstruct the sentence, adding spaces between words.
   - Finally, the first letter of the resulting sentence is capitalized, and the trailing space is removed before returning the result.


4. Complexity Analysis:
   - Time complexity: O(N log N) - Dominated by the sorting of `word_tuples`, where N is the number of words in the sentence. Splitting and joining the string are O(N) operations, which are less significant.
   - Space complexity: O(N) - We store the words and their associated information in the `word_tuples` list, which has a size proportional to the number of words. The resulting string `res` also has a size proportional to N.


## Topics
String, Sorting

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-03-10
