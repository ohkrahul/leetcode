# Game Play Analysis IV

## Problem Link
[LeetCode - Game Play Analysis IV](https://leetcode.com/problems/game-play-analysis-iv/)

## Difficulty
Medium

## Problem Description
<p>Table: <code>Activity</code></p>

<pre>
+--------------+---------+
| Column Name  | Type    |
+--------------+---------+
| player_id    | int     |
| device_id    | int     |
| event_date   | date    |
| games_played | int     |
+--------------+---------+
(player_id, event_date) is the primary key (combination of columns with unique values) of this table.
This table shows the activity of players of some games.
Each row is a record of a player who logged in and played a number of games (possibly 0) before logging out on someday using some device.
</pre>

<p>&nbsp;</p>

<p>Write a&nbsp;solution&nbsp;to report the <strong>fraction</strong> of players that logged in again on the day after the day they first logged in, <strong>rounded to 2 decimal places</strong>. In other words, you need to count the number of players that logged in for at least two consecutive days starting from their first login date, then divide that number by the total number of players.</p>

<p>The&nbsp;result format is in the following example.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> 
Activity table:
+-----------+-----------+------------+--------------+
| player_id | device_id | event_date | games_played |
+-----------+-----------+------------+--------------+
| 1         | 2         | 2016-03-01 | 5            |
| 1         | 2         | 2016-03-02 | 6            |
| 2         | 3         | 2017-06-25 | 1            |
| 3         | 1         | 2016-03-02 | 0            |
| 3         | 4         | 2018-07-03 | 5            |
+-----------+-----------+------------+--------------+
<strong>Output:</strong> 
+-----------+
| fraction  |
+-----------+
| 0.33      |
+-----------+
<strong>Explanation:</strong> 
Only the player with id 1 logged back in after the first day he had logged in so the answer is 1/3 = 0.33
</pre>


## Test Cases
```
{"headers":{"Activity":["player_id","device_id","event_date","games_played"]},"rows":{"Activity":[[1,2,"2016-03-01",5],[1,2,"2016-03-02",6],[2,3,"2017-06-25",1],[3,1,"2016-03-02",0],[3,4,"2018-07-03",5]]}}
```

## Initial Template
```python
# Code template not available
```

## Solution
1. Initial Thoughts:
   - The problem asks for the fraction of players who logged in on the day after their first login.
   - We need to find the first login date for each player.
   - Then, check if each player has a login record on the date after their first login date.
   - Finally, calculate the fraction by dividing the number of players who logged in on consecutive days by the total number of players.

2. Solution Implementation:
```python
import pandas as pd

def game_play_analysis_iv(activity: pd.DataFrame) -> pd.DataFrame:
    """
    Calculates the fraction of players who logged in on the day after their first login.

    Args:
        activity: The Activity table as a Pandas DataFrame.

    Returns:
        A Pandas DataFrame with the fraction of players.
    """

    # Find the first login date for each player
    first_login = activity.groupby('player_id')['event_date'].min().reset_index()
    first_login.rename(columns={'event_date': 'first_login_date'}, inplace=True)

    # Convert date columns to datetime objects
    activity['event_date'] = pd.to_datetime(activity['event_date'])
    first_login['first_login_date'] = pd.to_datetime(first_login['first_login_date'])

    # Merge the first login date with the activity table
    merged_activity = pd.merge(activity, first_login, on='player_id', how='left')

    # Calculate the next day after the first login date
    merged_activity['next_day'] = merged_activity['first_login_date'] + pd.DateOffset(days=1)

    # Check if the player logged in on the next day
    logged_in_next_day = merged_activity[merged_activity['event_date'] == merged_activity['next_day']]

    # Count the number of players who logged in on consecutive days
    consecutive_logins = logged_in_next_day['player_id'].nunique()

    # Calculate the total number of players
    total_players = activity['player_id'].nunique()

    # Calculate the fraction and round to 2 decimal places
    fraction = round(consecutive_logins / total_players, 2)

    return pd.DataFrame({'fraction': [fraction]})

```

3. Solution Explanation:
   - The code first finds the first login date for each player using `groupby` and `min`.
   - It then converts the date columns to datetime objects for easier date calculations.
   - The first login date is merged with the original activity table.
   - The next day after the first login is calculated using `pd.DateOffset`.
   - The code checks if each player has a login record on the calculated next day.
   - The number of players who logged in on consecutive days is counted using `nunique`.
   - The fraction is calculated by dividing the consecutive logins by the total number of players and rounded to 2 decimal places.
   - The result is returned as a DataFrame.

4. Complexity Analysis:
   - Time complexity: O(n log n) - Due to the sorting involved in `groupby` and `merge` operations.
   - Space complexity: O(n) - Because we store the activity data and intermediate DataFrames, which are proportional to the input size. 


## Topics
Database

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-04-29
