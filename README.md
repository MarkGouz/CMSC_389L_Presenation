# Find the Longest Valid Obstacle Course at Each Position

Problem Statement:

You want to build some obstacle courses. You are given a 0-indexed integer array obstacles of length n, where obstacles[i] describes the height of the ith obstacle.

For every index i between 0 and n - 1 (inclusive), find the length of the longest obstacle course in obstacles such that:

You choose any number of obstacles between 0 and i inclusive.
You must include the ith obstacle in the course.
You must put the chosen obstacles in the same order as they appear in obstacles.
Every obstacle (except the first) is taller than or the same height as the obstacle immediately before it.
Return an array ans of length n, where ans[i] is the length of the longest obstacle course for index i as described above.



Example 1:

Input: obstacles = [1,2,3,2]
Output: [1,2,3,3]
Explanation: The longest valid obstacle course at each position is:
- i = 0: [1], [1] has length 1.
- i = 1: [1,2], [1,2] has length 2.
- i = 2: [1,2,3], [1,2,3] has length 3.
- i = 3: [1,2,3,2], [1,2,2] has length 3.
Example 2:

Input: obstacles = [2,2,1]
Output: [1,2,1]
Explanation: The longest valid obstacle course at each position is:
- i = 0: [2], [2] has length 1.
- i = 1: [2,2], [2,2] has length 2.
- i = 2: [2,2,1], [1] has length 1.
Example 3:

Input: obstacles = [3,1,5,6,4,2]
Output: [1,1,2,3,2,2]
Explanation: The longest valid obstacle course at each position is:
- i = 0: [3], [3] has length 1.
- i = 1: [3,1], [1] has length 1.
- i = 2: [3,1,5], [3,5] has length 2. [1,5] is also valid.
- i = 3: [3,1,5,6], [3,5,6] has length 3. [1,5,6] is also valid.
- i = 4: [3,1,5,6,4], [3,4] has length 2. [1,4] is also valid.
- i = 5: [3,1,5,6,4,2], [1,2] has length 2.
 

Constraints:

n == obstacles.length
1 <= n <= 10^5
1 <= obstacles[i] <= 10^7

Approach:
When I first looked at his problem my idea was to go one at a time and somehow sort the array at each i so I could check the length up to that point. This is very similar to what I eventually ended up with but I decided to use a method called bisect_right to get the correct place to insert elements and keep them sorted while not required it requires a lot less lines.

Solution:
1. For this problem you need to get the total number of obstacles, an answer array, and a list to store the obstacles
2. The main idea behind this approach is to go through every index 1 at at a time and keep a sorted list to get all the elements equal or smaller than the ith element.
3. At each step we'll update the ith spot in the answer array with the idx + 1 that the new element would be in our sorted list. This would repsent how many obstacles smaller or equal to this element at the ith position.


Coding: 
```python
class Solution:

    def longestObstacleCourseAtEachPosition(self, obstacles: List[int]) -> List[int]:
        n = len(obstacles)
        answer = [1] * n
        lis = []
        for i, height in enumerate(obstacles):
            idx = bisect.bisect_right(lis, height)
            if idx == len(lis):
                lis.append(height)
            else:
                lis[idx] = height
            answer[i] = idx + 1
            
        return answer
```
Time complexity: O(nlogn), since we're going through every element n and use bisect_right which uses binary search so n * logn.
Space complexity: O(n), I use 2 arrays that take n space.

Takeaways: This problem is very good to practice your array manipulation and use some lesser used methods such as enumerate and bisect.bisect_right. It also gives you more experience with working with sorting and binary search by using bisect_right.
