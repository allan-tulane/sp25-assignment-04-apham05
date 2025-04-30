# CMPS 2200 Assignment 5
## Answers

**Name:**______Anh Pham___________________






- **1a.**
- log_d(n)


- **1b.**
- In a d-ary heap, delete-min removes the root and moves the last leaf to the top. To swap down the heap, we look through up to d children at each level, so the work is O(d log_d(n)). For insert, we add the new element at the end and move it up by comparing with its parent, which takes O(log_d(n))


- **1c.**
- Using a d-ary heap in Dijkstra’s algorithm, we make n = |V| deletions and m = |E| insertions. Each deletion costs O(d log_d(n)), and each insert costs O(log_d(n)). So the total work is O(nd log_d(n) + m log_d(n)).

- **1d.**
- To make Dijkstra’s algorithm as fast as possible, we want to pick a value of d that keeps both insert and delete-min operations balanced. If = m/n, both operations cost is about the same, and the total time becomes O(m log_m⁄n(n)). If we assume m = |V|^(1+𝜖), this log term simplifies to a constant (1/𝜖), so the total time becomes O(m). 



- **2a.**
Base case: APSP(i, j, 0)
APSP(0,0,0) = 0
APSP(0,1,0) = -2
APSP(0,2,0) = 2
APSP(1,0,0) = ∞
APSP(1,1,0) = 0
APSP(1,2,0) = 1
APSP(2,0,0) = ∞
APSP(2,1,0) = ∞
APSP(2,2,0) = 0

k = 1:
APSP(0,0,1) = min(0, -2 + ∞) = 0
APSP(0,1,1) = min(-2, -2 + 0) = -2
APSP(0,2,1) = min(2, -2 + 1) = -1

APSP(1,0,1) = min(∞, ∞ + ∞) = ∞
APSP(1,1,1) = min(0, ∞ + 0) = 0
APSP(1,2,1) = min(1, ∞ + 1) = 1

APSP(2,0,1) = ∞
APSP(2,1,1) = ∞
APSP(2,2,1) = 0

k = 2:
APSP(0,0,2) = min(0, -1 + ∞) = 0
APSP(0,1,2) = min(-2, -1 + ∞) = -2
APSP(0,2,2) = min(-1, -1 + 0) = -1

APSP(1,0,2) = ∞
APSP(1,1,2) = 0
APSP(1,2,2) = 1

APSP(2,0,2) = ∞
APSP(2,1,2) = ∞
APSP(2,2,2) = 0

- **2b.**
- Yes, there’s a pattern. To get APSP(i, j, 2), we just take the shorter of these two options: the shortest path from i to j without using vertex 2, or the path that goes from i to 2 and then from 2 to j. So APSP(i, j, 2) = min(APSP(i, j, 1), APSP(i, 2, 1) + APSP(2, j, 1))


- **2c.**
- To find the shortest path from i to j using up to vertex k, we compare two options: the best path from i to j that doesn’t go through k, and a path that goes from i to k and then k to j. Hence APSP(i, j, k) = min(APSP(i, j, k–1), APSP(i, k, k–1) + APSP(k, j, k–1))

- **2d.**
- If we use memoization and only compute each subproblem once, the number of unique subproblems is based on all possible combinations of (i, j, k). Since each of i, j, and k can be any of the |V| vertices, there are O(|V^3) total subproblems. So the total work is also O(|V|^3).

- **2e.**
- Johnson’s algorithm runs in O(|V| · |E| log |E|), while the dynamic programming version takes O(|V|^3). So we should use the DP version when the number of edges is small, hence, |E| log |E| is much less than |V|^2



- **3a.**
- Yes, every MST is also a valid solution to the MMET problem. If we had another tree with a smaller maximum edge than the MST, then we could swap that edge into the MST and get a better tree, which would be a contradiction. So the MST must already minimize the maximum edge too.


- **3b.**
- If we can’t use the MST, we can try building the next best option by looking at trees that are just one edge different from the MST. Try removing each edge in the MST one at a time, and replace it with a different edge that still keeps the tree connected. For all these swap options, pick the one with the next lowest total weight.




- **3c.**
- It takes O(|E| log |E|) to find the MST. Then we look at up to |E| swaps to try new trees. So the total work is O(|E| log |E|) overall.
