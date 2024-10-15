# Keys and Rooms
## https://leetcode.com/problems/keys-and-rooms

There are n rooms labeled from 0 to n - 1 and all the rooms are locked except for room 0. Your goal is to visit all the rooms. However, you cannot enter a locked room without having its key.

When you visit a room, you may find a set of distinct keys in it. Each key has a number on it, denoting which room it unlocks, and you can take all of them with you to unlock the other rooms.

Given an array rooms where rooms[i] is the set of keys that you can obtain if you visited room i, return true if you can visit all the rooms, or false otherwise.
```
Example 1:

Input: rooms = [[1],[2],[3],[]]
Output: true
Explanation: 
We visit room 0 and pick up key 1.
We then visit room 1 and pick up key 2.
We then visit room 2 and pick up key 3.
We then visit room 3.
Since we were able to visit every room, we return true.

Example 2:

Input: rooms = [[1,3],[3,0,1],[2],[0]]
Output: false
Explanation: We can not enter room number 2 since the only key that unlocks it is in that room.
``` 

### Constraints:

1. n == rooms.length
2. 2 <= n <= 1000
3. 0 <= rooms[i].length <= 1000
4. 1 <= sum(rooms[i].length) <= 3000
5. 0 <= rooms[i][j] < n
6. All the values of rooms[i] are unique.

## Implementation 1 : Trying to visit the rooms in sequence (This approach doesn't work)
e.g. this approach will fail for inputs similar to this `[[2],[],[1]]`, for this input we can visit the rooms in order 0, 2, 1 but the below implementation will return false
```java
class Solution {
    public boolean canVisitAllRooms(List<List<Integer>> rooms) {
        Set<Integer> set = new HashSet<>();
        int n = rooms.size();
        set.addAll(rooms.get(0));
        for(int i = 1; i < n; i++) {
            if(!set.contains(i))
               return false;
            List<Integer> keys = rooms.get(i);
            set.addAll(keys);
        }
        return true;
    }
}
```

## Implementation 2 : BFS
```java
class Solution {
    public boolean canVisitAllRooms(List<List<Integer>> rooms) {
        Queue<Integer> queue = new LinkedList<>();
        int roomsVisited = 0;
        Set<Integer> visited = new HashSet<>();
        queue.add(0);
        while(!queue.isEmpty()) {
            int room = queue.remove();
            if(visited.contains(room)) continue;
            roomsVisited++;
            visited.add(room);
            List<Integer> keys = rooms.get(room);
            for(int key : keys) {
                if(!visited.contains(key))
                   queue.add(key);
            }
        }
        return roomsVisited == rooms.size();
    }
}
```

