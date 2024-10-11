# LEETCODE-Arrays-1942
The code you provided solves the problem of finding which chair a specific friend (denoted by `targetFriend`) will sit on during an event. Each friend arrives and leaves at specific times, and the challenge is to assign chairs as they arrive, with previously vacated chairs being reused.

### Explanation of the Code

The main goal of the `smallestChair` function is to track when chairs become available and assign the smallest available chair number to each new arrival. Let’s go step by step through the solution:

1. **Priority Queues**:
   - `emptyChairs`: A min-heap (PriorityQueue) that keeps track of available chairs. It stores chair indices in ascending order, so the smallest chair available can be assigned.
   - `occupied`: A min-heap that stores pairs of `(leaving time, chair index)`. This helps determine which chairs will be freed up next.

2. **Preprocessing**:
   - Each `time` array (which consists of `[arrival time, leaving time]`) is extended by appending the index `i` of the friend. This allows the algorithm to track which friend arrives at which time.
   - The `times` array is then sorted by the arrival times.

3. **Assigning Chairs**:
   - For each event (each friend's arrival), the following happens:
     - Check if any chairs are becoming available (i.e., friends have left). If a friend's leaving time is less than or equal to the current friend's arrival time, their chair is added to the `emptyChairs` queue.
     - If the current friend is the `targetFriend`, return the smallest available chair. If no chairs are available, the next unsaturated chair (`nextUnsatChair`) is used.
     - If no chairs are free, assign the next unused chair to this friend, otherwise, assign the smallest available chair from `emptyChairs`.
   - Chairs are assigned based on the friend’s leaving time, meaning that as friends leave, their chairs are freed and available for future arrivals.

### Example Walkthrough

Consider an example:
```java
int[][] times = {{1, 4}, {2, 3}, {3, 5}};
int targetFriend = 0;
```

1. After extending the `times` array, it becomes:
   ```
   {{1, 4, 0}, {2, 3, 1}, {3, 5, 2}}
   ```
   Each tuple now represents `[arrival, leaving, friend_index]`.

2. After sorting by arrival time, the `times` array is the same because it is already sorted.

3. The algorithm proceeds:
   - Friend 0 arrives at time 1 and gets chair 0 (no other chairs are taken yet).
   - Friend 1 arrives at time 2, but no one has left yet, so they get chair 1.
   - Friend 2 arrives at time 3. At this point, Friend 1 is about to leave at time 3, so chair 1 is freed, and Friend 2 takes chair 1.

Since the `targetFriend` is Friend 0, they sit in chair 0, and that is the answer.

### Key Points
- The use of two priority queues efficiently handles chair assignment and availability.
- Sorting the `times` array by arrival time ensures we handle arrivals in the correct order.
- The chair selection is greedy, always giving the smallest available chair to a new arrival.

Let me know if you'd like more details or if you want to test specific cases!
