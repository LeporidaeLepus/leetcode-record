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

- **In Place Sort**: the amount of extra space required to sort the data is constant with the input size. (Which means ***Space Compexity = O(1)***.)
- **Stability**: a STABLE sort preserves relative order records with equal keys

### 1. QuickSort

#### QuickSelection

### 2. InsertingSort

- **Time Complexity: O(N<sup>2</sup>)**
  - Best Case: O(N)
- In-place
- stable
- **For nearly sorted suquences**

In the ith loop, insert the (i+1)th element into an appropriate place of the first well-ordered ith elements. The top of the array should always be in order.

```java
public int[] InsertingSort(int[] nums){
    int len = nums.length;
    if(len <= 1)    return nums;

    for(int i=1; i<len; i++){
        int cur = nums[i];
        int j = i-1;
        while(j>=0 && nums[j]>cur){
            nums[j+1] = nums[j];
            j+--;
        }
        nums[j+1] = cur;
    }
}
```

### 3. BubbleSort

- **Time Complexity: O(N<sup>2</sup>)**
- in-place
- stable

Repeatedly pass through the array and swap adjacent elements that are out of order.

```java
public int[] BubbleSort(int[] nums){
    int len = nums.length;
    if(len <= 1)    return nums;

    for(int i=0; i<len-1; i++){
        //flag to test whether the rest part of the array is in order.
        boolean flag = true;    
        for(int j=0; j<len-i-1; j++){
            if(nums[j] > nums[j+1]){
                int temp = nums[j];
                nums[j] = nums[j+1];
                nums[j+1] = temp;
                flag = false;
            }
        }
        if(flag == true)    break;
    }
    return nums;
}
```

### 4. MergeSort

- **Time Complexity: O(N·logN)**
- Space Complexity: O(N)
- Not in-space

**Divide**: Divide the n-element sequence to be sorted into two subsequences of n/2 elements each. Do this dividing resursively until the size of the subsuquence is 1.  
**Conqure and Merge**: Merge the two subsequences in order recursively.

```java
class Solution{
    public int[] mergeSortSolution(int[] nums){
        MergeSort(nums, 0, nums.length-1);
        return nums;
    }

    public void MergeSort(int[] nums, int start, int end){
        if(start == end)    return;

        int mid = (start + end) / 2;
        MergeSort(nums, start, mid);
        MergeSort(nums, mid+1, end);
        merge(nums, start, mid, end);
    }

    public void merge(int[] nums, int start, int mid, int end){
        int[] temp = new int[end - start + 1];
        int left = start;
        int right = mid+1;
        int i = 0;

        //compare the head of these two ordered aray and put the smaller one into temp
        while(left<=mid && right<=end){
            if(nums[left] <= nums[right]){
                temp[i++] = nums[left++];
            }else{
                temp[i++] = nums[right++];
            }
        }
        //put the rest part into temp
        if(left == mid){
            while(right <= end){
                temp[i++] = nums[right++];
            }
        }else{
            while(left <= mid){
                temp[i++] =nums[left++];
            }
        }
        //cover the original array with temp 
        for(int j=0; j<temp.length; j++){
            nums[start+j] = temp[j];
        }
}
```

### 5. HeapSort

- Time Complexity:
- in-place

Related Information:
1. A heap is a nearly complete binary tree that is filled in order
2. The root is the maximum/minimum emlement of the heap
3. A heap can be stored as an array A (index starts from 1)
   - root = A[1]
   - Node i = A[i]
   - left child of Node i = A[2i]
   - right chile of Node i = A[2i+1]
   - Parent of Node i = A[i/2]
   - A[n/2+1, ... , n] are leaves
4. Heap Types
   - Max-heaps: A[PARENT(i)] >= A[i]
   - Min-heaps: A[PARENT(i)] <= A[i]
5. New nodes are always inserted *at the bottom level* (left to right); Nodes are always removed *from the bottom level* (right to left)
6. **`MAX-HEAPIFY`**: maintian the max-heap property
   - If a node is smaller thean a child, exchange it with its larger child. Move down the tree and do this process recursively untill node is not smaller than children.

    ```java
    public void MaxHeapify(int[] nums, int i, int end){
        
    }
    ```

Build a max-heap from the array. Swap the root (the maximum element) with the last element in the array. Decrease the heap size by 1 (the last element will not be concerned any more). Call MAX-HEAPIFY on the new root to maintian the max-heap. Preat this process until only one node remains.

### 6. SelectionSort
