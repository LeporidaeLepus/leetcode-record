# Algorithm

- [Algorithm](#algorithm)
  - [Binary Search](#binary-search)
  - [DFS (Depth-First Search)](#dfs-depth-first-search)
  - [BFS (Breadth-First Search)](#bfs-breadth-first-search)
  - [Recursion](#recursion)
  - [Divide and Conqure](#divide-and-conqure)
  - [Sort](#sort)
    - [1. QuickSort](#1-quicksort)
      - [QuickSelection](#quickselection)
    - [2. InsertingSort](#2-insertingsort)
    - [3. BubbleSort](#3-bubblesort)
    - [4. MergeSort](#4-mergesort)
    - [5. HeapSort](#5-heapsort)
    - [6. SelectionSort](#6-selectionsort)

## Binary Search

- Time complexity = O(log(n))
- Sorted arrays, no duplicated elements.
- Be careful of the bounds

>[4. Median of two arays](https://leetcode.com/problems/median-of-two-sorted-arrays/)
>
>We need to find the kth large number. Since the left of Amid and Bmid are the smallest part of A and B and totally have k number.So if A\[Amid\] < B\[Bmid\], then A\[Amid\] and the left part of Amid must be smaller then the kth large number.
>
>The reason why Bmid and the right part of Bmid must be larger than the kth large number is the same as above.
>
> - After the search of k1 elements, we still have (k-k1) elements to search.
> - If the Amid_n is equan or larger to the length of A, then the next Amid_(n+1) should be cut down, which means we should deal it as AA\[Amid\] > B\[Bmid\].
>
>[33. Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/)

## DFS (Depth-First Search)

- recursion
- iteration + stack
  
  - ```java
    Deque<TreeNode> stack = new ArrayDeque<>();
    stack.push(root);
    while(!stack.isEmpty()){
        TreeNode node = stack.pop();
        if(node.left != null)
            stack.push(node.left);
        if(node.right != null)
            stack.push(node.right);
    }
    ```

>[236. Lowest Common Ancestor of a Binary Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/)

## BFS (Breadth-First Search)

- iteration + queue

  - ```java
    Queue<TreeNode> queue = new linkedList<>();
    queue.add(root);
    while(!queue.isEmpty()){
        TreeNode node = queue.remove();
        if(node.left != null)
            queue.add(node.left);
        if(node.right != null)
            queue.add(node.right);
    }

&nbsp;

## Recursion

Space Complexity: O(N)

- For a recursive solution there is always stack space used as internal function states are saved onto a stack during recursion. The maximum depth of recursion decides the stack space used.  

&nbsp;

## Divide and Conqure

- resursion

> [53. Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)  
> divideed into 3 parts (left, right, combine), calculate the conbine part in every recursion function and use recursion get the left and right part. Compare the 3 part at the end of the recursion function.

## Sort

- In Place Sort:
- Stability:

### 1. QuickSort

#### QuickSelection

### 2. InsertingSort

### 3. BubbleSort

### 4. MergeSort

### 5. HeapSort

### 6. SelectionSort
