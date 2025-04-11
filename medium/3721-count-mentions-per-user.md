# Count Mentions Per User

## Problem Link
[LeetCode - Count Mentions Per User](https://leetcode.com/problems/count-mentions-per-user/)

## Difficulty
Medium

## Problem Description
<p>You are given an integer <code>numberOfUsers</code> representing the total number of users and an array <code>events</code> of size <code>n x 3</code>.</p>

<p>Each <code inline="">events[i]</code> can be either of the following two types:</p>

<ol>
	<li><strong>Message Event:</strong> <code>[&quot;MESSAGE&quot;, &quot;timestamp<sub>i</sub>&quot;, &quot;mentions_string<sub>i</sub>&quot;]</code>

	<ul>
		<li>This event indicates that a set of users was mentioned in a message at <code>timestamp<sub>i</sub></code>.</li>
		<li>The <code>mentions_string<sub>i</sub></code> string can contain one of the following tokens:
		<ul>
			<li><code>id&lt;number&gt;</code>: where <code>&lt;number&gt;</code> is an integer in range <code>[0,numberOfUsers - 1]</code>. There can be <strong>multiple</strong> ids separated by a single whitespace and may contain duplicates. This can mention even the offline users.</li>
			<li><code>ALL</code>: mentions <strong>all</strong> users.</li>
			<li><code>HERE</code>: mentions all <strong>online</strong> users.</li>
		</ul>
		</li>
	</ul>
	</li>
	<li><strong>Offline Event:</strong> <code>[&quot;OFFLINE&quot;, &quot;timestamp<sub>i</sub>&quot;, &quot;id<sub>i</sub>&quot;]</code>
	<ul>
		<li>This event indicates that the user <code>id<sub>i</sub></code> had become offline at <code>timestamp<sub>i</sub></code> for <strong>60 time units</strong>. The user will automatically be online again at time <code>timestamp<sub>i</sub> + 60</code>.</li>
	</ul>
	</li>
</ol>

<p>Return an array <code>mentions</code> where <code>mentions[i]</code> represents the number of mentions the user with id <code>i</code> has across all <code>MESSAGE</code> events.</p>

<p>All users are initially online, and if a user goes offline or comes back online, their status change is processed <em>before</em> handling any message event that occurs at the same timestamp.</p>

<p><strong>Note </strong>that a user can be mentioned <strong>multiple</strong> times in a <strong>single</strong> message event, and each mention should be counted <strong>separately</strong>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<div class="example-block">
<p><strong>Input:</strong> <span class="example-io">numberOfUsers = 2, events = [[&quot;MESSAGE&quot;,&quot;10&quot;,&quot;id1 id0&quot;],[&quot;OFFLINE&quot;,&quot;11&quot;,&quot;0&quot;],[&quot;MESSAGE&quot;,&quot;71&quot;,&quot;HERE&quot;]]</span></p>

<p><strong>Output:</strong> <span class="example-io">[2,2]</span></p>

<p><strong>Explanation:</strong></p>

<p>Initially, all users are online.</p>

<p>At timestamp 10, <code>id1</code> and <code>id0</code> are mentioned. <code>mentions = [1,1]</code></p>

<p>At timestamp 11, <code>id0</code> goes <strong>offline.</strong></p>

<p>At timestamp 71, <code>id0</code> comes back <strong>online</strong> and <code>&quot;HERE&quot;</code> is mentioned. <code>mentions = [2,2]</code></p>
</div>

<p><strong class="example">Example 2:</strong></p>

<div class="example-block">
<p><strong>Input:</strong> <span class="example-io">numberOfUsers = 2, events = [[&quot;MESSAGE&quot;,&quot;10&quot;,&quot;id1 id0&quot;],[&quot;OFFLINE&quot;,&quot;11&quot;,&quot;0&quot;],[&quot;MESSAGE&quot;,&quot;12&quot;,&quot;ALL&quot;]]</span></p>

<p><strong>Output:</strong> <span class="example-io">[2,2]</span></p>

<p><strong>Explanation:</strong></p>

<p>Initially, all users are online.</p>

<p>At timestamp 10, <code>id1</code> and <code>id0</code> are mentioned. <code>mentions = [1,1]</code></p>

<p>At timestamp 11, <code>id0</code> goes <strong>offline.</strong></p>

<p>At timestamp 12, <code>&quot;ALL&quot;</code> is mentioned. This includes offline users, so both <code>id0</code> and <code>id1</code> are mentioned. <code>mentions = [2,2]</code></p>
</div>

<p><strong class="example">Example 3:</strong></p>

<div class="example-block">
<p><strong>Input:</strong> <span class="example-io">numberOfUsers = 2, events = [[&quot;OFFLINE&quot;,&quot;10&quot;,&quot;0&quot;],[&quot;MESSAGE&quot;,&quot;12&quot;,&quot;HERE&quot;]]</span></p>

<p><strong>Output:</strong> <span class="example-io">[0,1]</span></p>

<p><strong>Explanation:</strong></p>

<p>Initially, all users are online.</p>

<p>At timestamp 10, <code>id0</code> goes <strong>offline.</strong></p>

<p>At timestamp 12, <code>&quot;HERE&quot;</code> is mentioned. Because <code>id0</code> is still offline, they will not be mentioned. <code>mentions = [0,1]</code></p>
</div>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= numberOfUsers &lt;= 100</code></li>
	<li><code>1 &lt;= events.length &lt;= 100</code></li>
	<li><code>events[i].length == 3</code></li>
	<li><code>events[i][0]</code> will be one of <code>MESSAGE</code> or <code>OFFLINE</code>.</li>
	<li><code>1 &lt;= int(events[i][1]) &lt;= 10<sup>5</sup></code></li>
	<li>The number of <code>id&lt;number&gt;</code> mentions in any <code>&quot;MESSAGE&quot;</code> event is between <code>1</code> and <code>100</code>.</li>
	<li><code>0 &lt;= &lt;number&gt; &lt;= numberOfUsers - 1</code></li>
	<li>It is <strong>guaranteed</strong> that the user id referenced in the <code>OFFLINE</code> event is <strong>online</strong> at the time the event occurs.</li>
</ul>


## Test Cases
```
2
[["MESSAGE","10","id1 id0"],["OFFLINE","11","0"],["MESSAGE","71","HERE"]]
2
[["MESSAGE","10","id1 id0"],["OFFLINE","11","0"],["MESSAGE","12","ALL"]]
2
[["OFFLINE","10","0"],["MESSAGE","12","HERE"]]
```

## Initial Template
```python
# Code template not available
```

## Solution
1. Initial Thoughts:
   - The problem asks us to count mentions for each user based on a series of events.
   - We need to keep track of which users are online at any given time. Since offline events have a duration of 60, we can store offline times for users.
   - For each message event, we need to parse the mentions string and update the mention count for corresponding users based on their online status (for HERE mentions).
   - ALL mentions always increment the counter for everyone regardless of their online status.
   - We can process the events chronologically.

2. Solution Implementation:
```python
def count_mentions(numberOfUsers, events):
    """
    Counts mentions per user based on a series of events.

    Args:
        numberOfUsers: The total number of users.
        events: A list of events.

    Returns:
        A list of mention counts for each user.
    """
    mentions = [0] * numberOfUsers
    offline_times = {}  # Store offline times for users

    for event in events:
        event_type, timestamp, data = event
        timestamp = int(timestamp)

        # Process offline events first
        if event_type == "OFFLINE":
            user_id = int(data)
            offline_times[user_id] = timestamp + 60  # Store offline end time

        elif event_type == "MESSAGE":
            if data == "ALL":
                for user_id in range(numberOfUsers):
                    mentions[user_id] += 1
            elif data == "HERE":
                for user_id in range(numberOfUsers):
                    if user_id not in offline_times or offline_times[user_id] <= timestamp:
                        mentions[user_id] += 1
            else:  # Individual mentions
                mentioned_users = data.split()
                for user_str in mentioned_users:
                    user_id = int(user_str[2:])  # Extract user ID from "id<number>"
                    mentions[user_id] += 1

    return mentions

```

3. Solution Explanation:
   - We initialize a `mentions` array to store mention counts and an `offline_times` dictionary to keep track of users' offline end times.
   - We iterate through the `events` list.
   - For each "OFFLINE" event, we store the user's offline end time (timestamp + 60) in `offline_times`.
   - For each "MESSAGE" event:
     - If the message is "ALL", we increment the mention count for all users.
     - If the message is "HERE", we check if each user is online (not in `offline_times` or offline end time is before the current timestamp) and increment their count if they are online.
     - If the message contains individual mentions, we split the mentions string, extract user IDs, and increment the corresponding mention counts.
   - Finally, we return the `mentions` array.

4. Complexity Analysis:
   - Time complexity: O(n * m) where n is the number of events and m is the maximum number of mentions in a single message or the number of users (for ALL/HERE). In the worst case, we might have to iterate through all users for each message.
   - Space complexity: O(k) where k is the number of users who went offline. This is the space used by the `offline_times` dictionary. In the worst case, k can be equal to the number of users.  Since the number of users is at most 100, it can also be considered O(1) in that sense.


## Topics
Array, Math, Sorting, Simulation

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-04-11
