# Algorithm

<!-- no toc -->
- [Binary Search](#binary-search)
- [DFS (Depth-First Search)](#dfs-depth-first-search)
- [BFS (Breadth-First Search)](#bfs-breadth-first-search)
- [Recursion](#recursion)
- [Divide and Conqure](#divide-and-conqure)
- [Sort](#sort)
  - [1. QuickSort](#1-quicksort)
    - [QuickSelect](#quickselect)
  - [2. InsertingSort](#2-insertingsort)
  - [3. BubbleSort](#3-bubblesort)
  - [4. MergeSort](#4-mergesort)
  - [5. HeapSort](#5-heapsort)
  - [6. SelectionSort](#6-selectionsort)
- [Dynamic Progamming](#dynamic-progamming)
  - [Knapsack Problem](#knapsack-problem)
  - [House Robber Problem](#house-robber-problem)
  - [Best Time to Buy and Sell Stock](#best-time-to-buy-and-sell-stock)

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

- **Time Complexity: O(N·logN)**
  - worst case: O(N<sup>2</sup>)
  - but the worst case doesn't happen often
- in-place

To sort an array `A[p...r]`, partition the array into 2 subarrays `A[p...q]`, `A[q+1...r]` (choose an element as **`pivot`**), such that each element of A[p...q] is smaller than or equal to each element in A[q+1...r]. Do this process to each subarray **recursively** until there is only one element in each subarray. (No adition work need to combine them.)

```java
public QuickSort{
  public int[] QuickSort(int[] nums){
    sort(nums, 0, nums.length - 1);
    return nums;
  } 

  private void sort(int[] nums, int start, int end){
    if(start >= end)  return;

    //for random pivot:
    //int pivot = nums[start + (int)(Math.random()*(end-start+1))];
    int pivot = nums[start];
    int i = start;
    int j = end+1;

    while(i<j){
      //loop j first then we will not need to worry about the index out of bounds
      do{   
        j--;
      }while(i<j && nums[j] >= pivot);
      do{
        i++;
      }while(i<j && nums[i] <= pivot);

      f(i < j){
        swap(nums, i, j);
      }
      else{
        // in ascending order, and with the origin position of pivot is in the head of the subarray, 
        //we swap it with the smaller one between nums[i] and nums[j]
        swap(nums, j, start);
      }
    }

    sort(nums, start, j-1);
    sort(nums, j+1, end);
  }

  private void swap(int nums[], int i, int j){
    int temp = nums[i];
    nums[i] = nums[j];
    nums[j] = temp;
  }
}
```

#### QuickSelect

- Is used to **find the kth** smallest / largest element in an unordered list.
- Instead of recurring for both sides after finding pivot, it recurs only for the part contains the kth element.
- **Time Complexity**: (reduced from O(N·logN) to) **O(N)**
  - worst case: O(N<sup>2</sup>)

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

    //compare the head of these two ordered array and put the smaller one into temp
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

- **Time Complexity: O(N·logN)**
- in-place
- In Java, we can use `PriorityQueue`
  
  ```java
  PriorityQueue<T> heap = new PriorityQueue<T>(Comparator<T> c);
  heap.add(T o);  
  heap.poll();  // return and remove the head of the PriorityQueue
  int size = heap.size();
  ```

  - can be used to find the kth smallest / largest element by limiting the length of `heap`

Related Information:

1. A heap is a nearly complete binary tree that is filled in order
2. The root is the maximum/minimum emlement of the heap
3. A heap can be stored as an array A (index starts from 1)
   - root = A[1] (`A[0]`)
   - Node i = A[i] (`A[i-1]`)
   - left child of Node i = A[2i] (`A[2i+1]`)
   - right chile of Node i = A[2i+1] (`A[2i+2]`)
   - Parent of Node i = A[i/2]  (`A[(i-1)/2]`)
   - A[n/2+1, ... , n] are leaves
4. Heap Types
   - Max-heaps: A[PARENT(i)] >= A[i]
   - Min-heaps: A[PARENT(i)] <= A[i]
5. New nodes are always inserted *at the bottom level* (left to right); Nodes are always removed *from the bottom level* (right to left)
6. **`MAX-HEAPIFY`**: maintian the max-heap property
   - If a node is smaller thean a child, exchange it with its larger child. Move down the tree and do this process **recursively** untill node is not smaller than children.

    ```java
    public void MaxHeapify(int[] nums, int curr, int end){
      int largest = curr;
      int leftchild = curr * 2 + 1;
      int rightchild = curr * 2 + 2;
    
      if(leftchild<=end && nums[leftchild]>nums[curr]){
        largest = leftchild;
      }
      if(rightchild<=end && nums[rightchild]>nums[largest]){
        largest = right;
      }

      if(largest != curr){
        swap(nums, curr, largest);
        MaxHeapify(nums, largest, end);
      }
    }

    private void swap(int[] nums, int i, int j){
      int temp = nums[i];
      nums[i] = nums[j];
      nums[j] = temp;
    }
    ```

7. **Building a Heap**: we can build a heap **in a bottom-up manner** by running MAX-HEAPIFY on successive subarrays
   - Since A[n/2+1, ..., n] (`A[n/2, ..., n-1]`) are leaves,
   - we only need to run MAX-HEAPIFY between A[1, ..., n/2] (`A[0, ..., n/2-1]`)
  
    ```java
    private void buildMaxHeap(int[] nums){
      int len = nums.length;
    
      for(int i=len-1; i>=0; i++){
        MaxHeapify(nums, i, len-1);
      }
    }
    ```

Build a max-heap from the array. Swap the root (the maximum element) with the last element in the array. Decrease the heap size by 1 (the last element will not be concerned any more). Call MAX-HEAPIFY on the new root to maintian the max-heap. Preat this process until only one node remains.

```java
class HeapSort{
  public int[] maxHeapSort(int[] nums){
    buildMaxHeap(nums);
    int size = nums.length-1;
    while(size > 0){
      swap(nums, 0, size);
      size--;
      MaxHeapify(nums, 0, size);
    }
    // the return array is in ascending order
    return nums;
  }
}
```

### 6. SelectionSort

- **Time Complexity: O(N<sup>2</sup>)**

Repeatedly find the minimum element (considering asceding order) from the unsorted part and put it at the beginning of this part. The first part of the array is always sorted and the ramianing part is unsorted. The length of the sorted subarray will `+1` after every iteration.

```java
public int[] SelectionSort(int[] nums){
  int len = nums.length;
  if(len <= 0)  return nums;

  for(int i=0; i<len-1; i++){
    int min = i;
    for(int j=i+1; j<len; j++){
      if(nums[j] < nums[min]){
        min = j;
      }
    }
    if(min != i){
      int temp = nums[i];
      nums[i] = nums[j];
      nums[j] = temp;
    }
  }

  return nums;
}
```

&nbsp;

## Dynamic Progamming

- Bottom-Up DP (Tabulation)
- Top-Down DP(Recersion + Memoization)

1. Defination of DP table and the index
2. Recursion formula for DP table
3. Initialization of the DP table
    > [63. Unique Paths II](https://leetcode.com/problems/unique-paths-ii/)
4. Traversal order for DP table
5. Deriving an example tabulation from processes above to check the correctness

### Knapsack Problem

#### 0-1 Knapsack Problem

Items have attribute A and B (weight and value), the container has a limit of attribute A(bagsize) and every item can be put into the container **only once**. (put or not put, a 0-1 problem) We want to get the max value of items put into the container.

1. 2D array  

   ```java
   // int bagsize, int[] weight, int[] value
   int len = weight.length;   // = value.length;
   int[][] dp = new int[len][bagsize+1];
   for(int i=0; i<len; i++){
    for(int j=0; j<=bagsize; j++){
      if(weight[i] > j){
        dp[i][j] = dp[i-1][j];
      }
      else{
        dp[i][j] = Math.max(dp[i-1][j], dp[i-1][j-weight[i]] + value[i]);
      }
    }
   }
    ```

2. 1D array (if the last row/column can be reused)
    - be care of the traversal order – **this is to make sure that every item only be added no more than once**

    ```java
    // int bagsize, int[] weight, int[] value
    int len = weight.length;   // = value.length;
    int[] dp = new int[bagsize+1];
    for(int i=0; i<len; i++){
      // travsersal starts from the last index to avoid the element in front from being covered
      for(j=bagsize; j>=weight[i]; j++){
        dp[j] = Math.max(dp[j], dp[j-weight[i]] + value[i]);
      }
    }
    ```

- If the question wants the minimum difference between 2 subarrays (or any question involves **subtraction or `-`**), than we can use **sum/2** as the volume of the bag.
    > [1049. Last Stone Weight II](https://leetcode.com/problems/last-stone-weight-ii/)
- The limitaion of the container can be 2 dimentions
    > [474. Ones and Zeroes](https://leetcode.com/problems/ones-and-zeroes/)

#### Complete Knapsack Problem

Every item can be put into the container **infinite times**.

- The traversal order is different from the 0-1 Knapsack Problems.
- The order of loop which dimention first is different between **Combination** and **Permutation**.
  - Combination:

  ``` java
  // int bagsize, int[] weight, int[] value
  int len = weight.length;   // = value.length;
  int[] dp = new int[bagsize+1];
  /* Initialization */
  for(int i=0; i<len; i++){
    // travsersal starts from the first index so we can but an item into the bag several times.
    for(j=weight[i]; j<=bagsize; j++){
      dp[j] = Math.max(dp[j], dp[j-weight[i]] + value[i]);
    }
  }
  ```

  - Permutation:
    > [377. Combination Sum IV](https://leetcode.com/problems/combination-sum-iv/)
  
  ```java
  // int bagsize, int[] weight, int[] value
  int len = weight.length;   // = value.length;
  int[] dp = new int[bagsize+1];
  /* Initialization */
  // Loop the bagsize first, so we can get the permutation of all the items of a specific bagsize
  for(int i=0; i<=bagsize; i++){
    for(j=0; j<length; j++){
      if(i >= weight[j])
        dp[i] = //dp formula;
    }
  }
  ```

- If we want to get a **minimum** result, be careful when we initialize the array. Set the initial value to **`Integer.MAX_VALUE`** if necessary.
    > [322. Coin Change](https://leetcode.com/problems/coin-change/)  
    > [279. Perfect Squares](https://leetcode.com/problems/perfect-squares/)

#### Multiple Knapsacks Problem

Every item can be put into the container m<sub>i</sub> times.

- consider item i as m<sub>i</sub> different items -> 0-1 knapsacks problems
- add a loop in 0-1 knapsacks problems
  
  ```java
  // int bagsize, int[] weight, int[] value, int num[]
  int len = weight.length;   // = value.length;
  int[] dp = new int[bagsize+1];
  for(int i = 0; i < len; i++) {
    // travsersal starts from the last index to avoid the element in front from being covered
    for(int j = bagsize; j >= weight[i]; j++) {
      // add a loop here to add item k times to the bag
      for(int k = 1; k <= num[i] && j >= k * weight[i]; k++){
        dp[j] = Math.max(dp[j], dp[j - k * weight[i]] + k * value[i]);
      }
    }
  }
  ```

&nbsp;

> <big>**Combination**</big>  
>
> **C<sup>k</sup><sub>n</sub> = (<sup>n</sup><sub>k</sub>) = n! / k!(n-k)! = n(n-1)...(n-k+1) / k!**
>
> - Time Complexity: O(k)
> - Space Complexity: O(1)
>
> ```java
> // we should keep dividing the numerator by the denominator when caculating to avoid over flow
> public int combination(int n, int k){
>   long numerator = 1; // 分子
>   int denominator = k; // 分母
>   int count = k;
>   int t = n;
>   while(count--){
>     numetator *= t--;
>     while(denominator != 0 && numerator % denominatoe == 0){
>       numerator /= denominator;
>       denominator--;
>     }
>   }
>   return numerator;
> }
> ```

### House Robber Problem

Rob a street of houses and cannot rob adjasant housese, get the maximum money can be robbed.

1. Recursion with Memorization
2. **Dynamic Programming with Tabulation**
  
  ```java
  //nums[] -> money can be robbed in each house
  int len = nums.length;
  if (len == 1) return nums[0];
  // dp[i] means the maximum money can be robbed in the first i houses
  int[] dp = new int[len+1];  
  // dp[i] = max(dp[i-1], dp[i-2] + nums[i])
  // Initialize dp[0] = 0, dp[1] = nums[0];
  for (int i = 2; i<=len; i++) {
    dp[i] = Math.max(dp[i-1], dp[i-2] + nums[i-1]);
  }
  return dp[len];
  ```

#### Rob a Cycle

If the houses are arranged in a **cycle**, consider three situations:  

  1. without the first house
  2. without the last house  
  3. without the first and the last house  
  
since situation 3 is contained in situation 1 and 2, so we only need to consider the first two situations and get the maximum one of them.

#### Rob a Binary Tree

Recursion (binary tree) + dp[2] (steal or not steal)

1. Parameter and return value of recursive function -> {parameter: `Node root`; return value: `int[] dp`}
2. Termination conditions -> `root == null`
3. Traversal order -> postorder
4. The logic of recursion (dp formula)

> [337. House Robber III](https://leetcode.com/problems/house-robber-iii/)  

### Best Time to Buy and Sell Stock

1. 2D Array (`dp[prices.length][2]`)
    - `dp[i][0]` is the most money we can have if we **hold stock** in the ith day; `dp[i][1]` is the the most money we can have if we **do not hold** stock in the ith day
    - `dp[i][0] = max(dp[i-1][0], -prices[i])` (if we hold stack in the ith day, the most money we can have is the max of these two situations: (1) we hold stock yesterday then we keep the same; (2) we buy stock today)  
    `dp[i][1] = max(dp[i-1][1], dp[i-1][0] + prices[i])` (if we do not hold stack in the ith day, the most money we can have is the max of these two situations: (1) we do not hold stock yesterday then we keep the same; (2) we hold stock yesterday but sold it today)  
    **The maximum profit we can finally get: `dp[prices.length][1]`**
    - Initialization: `dp[1][0] = -prices[0]`; `dp[1][1] = 0`
    - Traversal from front to back
2. 1D Array (dp[2])

    ```java
    int len = prices.length;
    int[] dp = new int[2];
    dp[0] = -prices[0];
    dp[1] = 0;
    for(int i=1; i<len; i++){
      dp[0] = Math.max(dp[0], -prices[i]);
      // if dp[0] is updated, it means that dp[0] in yesterday is less than -prices[i], which also means dp[0] + prices[i] < 0. Since dp[1] should always larger or equal than 0, the dp[1] can only be dp[1] in yesterday and the update of dp[0] will not affect the result of dp[1].
      dp[1] = Math.max(dp[1], dp[0] + prices[i]);
    }
    return dp[1];
    ```

### Subsuquence
