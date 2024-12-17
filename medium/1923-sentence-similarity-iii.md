# Sentence Similarity III

## Problem Link
[LeetCode - Sentence Similarity III](https://leetcode.com/problems/sentence-similarity-iii/)

## Difficulty
Medium

## Problem Description
<p>You are given two strings <code>sentence1</code> and <code>sentence2</code>, each representing a <strong>sentence</strong> composed of words. A sentence is a list of <strong>words</strong> that are separated by a <strong>single</strong> space with no leading or trailing spaces. Each word consists of only uppercase and lowercase English characters.</p>

<p>Two sentences <code>s1</code> and <code>s2</code> are considered <strong>similar</strong> if it is possible to insert an arbitrary sentence (<em>possibly empty</em>) inside one of these sentences such that the two sentences become equal. <strong>Note</strong> that the inserted sentence must be separated from existing words by spaces.</p>

<p>For example,</p>

<ul>
	<li><code>s1 = &quot;Hello Jane&quot;</code> and <code>s2 = &quot;Hello my name is Jane&quot;</code> can be made equal by inserting <code>&quot;my name is&quot;</code> between <code>&quot;Hello&quot;</code><font face="monospace"> </font>and <code>&quot;Jane&quot;</code><font face="monospace"> in s1.</font></li>
	<li><font face="monospace"><code>s1 = &quot;Frog cool&quot;</code> </font>and<font face="monospace"> <code>s2 = &quot;Frogs are cool&quot;</code> </font>are <strong>not</strong> similar, since although there is a sentence <code>&quot;s are&quot;</code> inserted into <code>s1</code>, it is not separated from <code>&quot;Frog&quot;</code> by a space.</li>
</ul>

<p>Given two sentences <code>sentence1</code> and <code>sentence2</code>, return <strong>true</strong> if <code>sentence1</code> and <code>sentence2</code> are <strong>similar</strong>. Otherwise, return <strong>false</strong>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<div class="example-block">
<p><strong>Input:</strong> <span class="example-io">sentence1 = &quot;My name is Haley&quot;, sentence2 = &quot;My Haley&quot;</span></p>

<p><strong>Output:</strong> <span class="example-io">true</span></p>

<p><strong>Explanation:</strong></p>

<p><code>sentence2</code> can be turned to <code>sentence1</code> by inserting &quot;name is&quot; between &quot;My&quot; and &quot;Haley&quot;.</p>
</div>

<p><strong class="example">Example 2:</strong></p>

<div class="example-block">
<p><strong>Input:</strong> <span class="example-io">sentence1 = &quot;of&quot;, sentence2 = &quot;A lot of words&quot;</span></p>

<p><strong>Output:</strong> <span class="example-io">false</span></p>

<p><strong>Explanation:</strong></p>

<p>No single sentence can be inserted inside one of the sentences to make it equal to the other.</p>
</div>

<p><strong class="example">Example 3:</strong></p>

<div class="example-block">
<p><strong>Input:</strong> <span class="example-io">sentence1 = &quot;Eating right now&quot;, sentence2 = &quot;Eating&quot;</span></p>

<p><strong>Output:</strong> <span class="example-io">true</span></p>

<p><strong>Explanation:</strong></p>

<p><code>sentence2</code> can be turned to <code>sentence1</code> by inserting &quot;right now&quot; at the end of the sentence.</p>
</div>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= sentence1.length, sentence2.length &lt;= 100</code></li>
	<li><code>sentence1</code> and <code>sentence2</code> consist of lowercase and uppercase English letters and spaces.</li>
	<li>The words in <code>sentence1</code> and <code>sentence2</code> are separated by a single space.</li>
</ul>


## Test Cases
```
"My name is Haley"
"My Haley"
"of"
"A lot of words"
"Eating right now"
"Eating"
```

## Initial Template
```python
# Code template not available
```

## Solution
### 1. Initial Thoughts:
 
- The problem is essentially asking whether we can transform one sentence into another by inserting a sentence between words.
- The key is to identify the missing words and insert them at the correct position.
- We can use a sliding window approach to keep track of the words in both sentences.

### 2. Solution Implementation:
```python
def areSentencesSimilar(sentence1: str, sentence2: str) -> bool:
    """
    :type sentence1: str
    :type sentence2: str
    :rtype: bool
    """
    def split_sentences(sentence):
        words = sentence.split()
        return words, len(words)
    
    def find_missing_words(words1, words2):
        m, n = len(words1), len(words2)
        
        i = 0
        j = 0
        missing_words = []
        while i < m and j < n:
            if words1[i] == words2[j]:
                i += 1
                j += 1
            else:
                missing_words.append(words2[j])
                j += 1
        while j < n:
            missing_words.append(words2[j])
            j += 1
        
        return missing_words
    
    words1, m = split_sentences(sentence1)
    words2, n = split_sentences(sentence2)
    
    if m == n:
        return True
    elif m < n:
        return words1 == find_missing_words(words1, words2)
    else:
        return words2 == find_missing_words(words2, words1)
```

### 3. Solution Explanation:

- We first split both sentences into lists of words and calculate their lengths.
- If the lengths are the same, the sentences are obviously similar.
- Otherwise, we identify the missing words by comparing the two lists.
- The missing words are appended to a list, and we check if they match the other sentence.
- If they do, the sentences are similar; otherwise, they are not.

### 4. Complexity Analysis:
- **Time complexity:** O(max(m, n)), where m and n are the lengths of the two sentences. We iterate through the longer sentence at most once, appending words to the missing words list.
- **Space complexity:** O(max(m, n)), since we store the missing words in a list.

## Topics
Array, Two Pointers, String

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2024-12-17
