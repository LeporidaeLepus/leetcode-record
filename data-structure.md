# Data Structure

- [Array](#array)  
- [Linked List](#linked-list)
- [Hash Table](#hash-table)
- [Chracter](#character)
- [Stack and Queue](#stack-and-queue)
- [Binary Tree](#binary-tree)
- Important Problems
  - [15. 3Sum](https://leetcode.com/problems/3sum/)

## Array

- Pay attention to the ***empty array*** and ***null.***
- Memory address is allocated succesively to elements in array.  
- Problems about 'sum' can be transformed into problems about 'difference'. Then we can use **HashMap** to decrease O().  
- Problems don't allow duplicated elements can be solved by **HashSet**.  
  - We sort the array first and put an element into the HashSet every time we meet an new one. Then finding a completment in the HashSet means this complement is in the array and it's an result we need.
  
  ```java
  // from set to array
  Set<Integer> set = new HashSet<Integer>();
  int[] arr = new int[set.size()];
  int i = 0;
  for(int a : set){
    arr[i++] = a;
  }
  ```

### Two Pointers

- fast pointer & slow pointer
- right pointer & left pointer

**Used in:** *remove elements*; *multiple sum*

>[18. 4Sum](https://leetcode.com/problems/4sum/)

### Sliding Window

**Used in:** *minimum subarray*;

>[76. Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/)
>
>- Use ***Sliding Window** which is constructed by 2 pointers.
>- **HashMap** can be used to count how many different characters are in the string and the time they duplicated.
>
>[209. Minimum Size Subarray Sum](https://leetcode.com/problems/minimum-size-subarray-sum/)  
> Time complexity: O(n)  
> Space complexity: O(1)
>
>1. *left & right pointers* to represent the begining and the end of the sliding window, *subsum* to represent the sum of subarray. A *form {int,int}* to record the begining and end of the current minimum subarray.
>2. Every time subsum >= target, check whether the lenght of sub array is smaller than the one record in form. If it is, update the form.  
>3. Minus the subsum by the number the left pointer point to and move the left pointer one position right.
>4. Check whether the left pointer is smaller than the right pointer and the subsum is still >= target. If they are, repeat 2. and 3., if they arn't, move the right pointer one positin right.
>5. Repeat the above process while right pointer is smaller than the length of the array.

### Spiral Matrix

- Set and update boundries.

>[54.Spiral Matrix](https://leetcode.com/problems/spiral-matrix/)  
>
>[885. Spiral Matrix III](https://leetcode.com/problems/spiral-matrix-iii/)
>
>```Java
>class Solution {
>
>    public int[][] spiralMatrixIII(int rows, int cols, int rStart, int cStart) {
>        int [][] res = new int[rows*cols][2];
>        int left = cStart-1;
>        int right = cStart+1;
>        int up = rStart;
>        int down = rStart+1;      
>        int i=0;
>        
>        while(i<rows*cols){
>            for(int c=Math.max(0,left+1);c<=right && c< cols && up>=0;c++){ 
>                res[i][0] = up;
>                res[i][1] = c;
>                i++;
>            }
>            for(int r=Math.max(0,up+1);r<=down && r<rows && right<cols;r++){
>                res[i][0] = r;
>                res[i][1] = right;
>                i++;
>            }
>            for(int c=Math.min(cols-1,right-1); c>=left && c>=0 && down<rows; c--){
>                res[i][0] = down;
>                res[i][1] = c;
>                i++;
>            }
>            for(int r=Math.min(rows-1,down-1); r>=up && r>=0 && left>=0; r--){
>                res[i][0] = r;
>                res[i][1] = left;
>                i++;
>            }
>            
>            left--;
>            up--;
>            right++;
>            down++;
>            
>        }
>        return res;
>    }
>}
>```
>
><mark>**`TODO:`** [2326. Spiral Matrix IV](https://leetcode.com/problems/spiral-matrix-iv/)</mark>

&nbsp;

## Linked List

- Pay special attention to **NULL** linked list like [].  
- Be careful to whitch ListNode is the next pointer links to.
- If need to return a linked list, set a special head which will not be changed to return.(for examle the **dummyhead**)
- If need to remove the head node, add a **dummy head** before the head.
- When design Linked List, the head in the initiate function whose `val=0, next=null` is the **dummy head**.
- `node = new ListNode()` returns a List Node `node.val=0, node.next=null` but not NULL. So if we need NULL, let `node=null`.

>[19. Remove Nth Node From End of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list/)
>
>- fast pointer & slow pointer
>
>[160. Intersection of Two Linked Lists](https://leetcode.com/problems/intersection-of-two-linked-lists/)  
> \# Approach 3: Two Pointers

&nbsp;

## Hash Table

**Usage:** To quickly determine whether an element appears in the collection;

- Hash table uses more space.
- When it's about String or character (especially only contains lowercase / uppercase ), we can use an array whose `length=26` as the hash table.

>[202. Happy Number](https://leetcode.com/problems/happy-number/)  
>One way to  get each digit of a number `n`:
>
>```(java)
>while(n!=0){
>   int d = n % 10;
>   n = n /1 0;
>}
>```
>
>[454. 4Sum II](https://leetcode.com/problems/4sum-ii/solution/)  
>Read the solution about interview.

&nbsp;

## Character

- In Java, String cannot be modified directly. String should be transfered into charArray or use StringBuilder first.
  - (e.g. `String s; s.charAt(a) = s.charAt(b)` will report an error.)
- *Two Pointers*
- *KMP*

>[151. Reverse Words in a String](https://leetcode.com/problems/reverse-words-in-a-string/)
>
> - Reverse twice: reverse the whole string and then reverse each words.
> - [剑指 Offer 58 - II. 左旋转字符串](https://leetcode.cn/problems/zuo-xuan-zhuan-zi-fu-chuan-lcof/)

### KMP Algorithm

- **Key:** *partial match table / lookup table /  failure function table*
  - It stores the length of the longest prefix that is also a suffix.
- KMP is used when we are given **a text `txt[0..n-1`]** and **a pattern `pat[0..m-1]`** *(n>m)* and need to write a function search(char pat[], char txt[]) that **prints all occurrences of pat[] in txt[]**.  
- The basic idea behind KMP’s algorithm is:  
  - whenever we detect a mismatch (after some matches), we already know some of the characters in the text of the next window. We take advantage of this information to avoid matching the characters that we know will anyway match.

1. Preprocessing the pattern `pat[]` and create an integer array **`lps[]`** of size `m` (which is the same as the pattern). This array is used to skip character while matching.
   - lps: longest proper prefix which is also suffix.  
2. When `index = i`, `lps[i]` stores length of the maximum matching proper prefix which is also a suffix of the sub-pattern `pat[0..i]`.
3. When `txt[k]` is mismatched with `pat[i+1]`, we check `lps[i]`. Since the former `lps[i]` characters are the same as the first `lps[i]` character in the pattern, we don't need to campare them any more. We can skip to compare the `lps[i]+1` character whose index is `lps[i]`, which means compare `txt[k]` with `pat[lps[i]]`.

- >refer: [KMP Algorithm for Pattern Searching](https://www.geeksforgeeks.org/kmp-algorithm-for-pattern-searching/)

>[28. Find the Index of the First Occurrence in a String](https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/)
>
>```java
>class Solution {
>    public int strStr(String haystack, String needle) {
>        int m = needle.length();
>        int n = haystack.length();
>        int[] lps = new int[m];
>        
>        //Initiate lps
>        int j = 0;
>        lps[0] = 0;
>        for(int i=1; i<m; i++){
>            //If there is a subarray before .needle[i] be a suffix which is also a proper perfix,
>            //test whether the subarray still a suffix which is also a proper perfix
>            //after adding needle[i].
>            while(j>0 && needle.charAt(i) != needle.charAt(j)){
>                j = lps[j-1];
>            }
>            
>            if(needle.charAt(i) == needle.charAt(j)){
>                j++;
>            }
>            lps[i] = j;
>        }
>        
>        //Compare haystack with needle
>        j = 0;
>        for(int i=0; i<n; i++){
>            while(j>0 && haystack.charAt(i) != needle.charAt(j)){
>                j = lps[j-1];
>            }
>            
>            if(haystack.charAt(i) == needle.charAt(j)){
>                j++;
>            }
>            if(j == m){     //When j==m, needle is completely matched
>                return i-m+1;       //The index in haystack minus the length of needle and add 1 
>                                    //is the first index of the first occurrence
>            }
>        }
>        
>        return -1;
>    }
>}
>```
>
> - [Solustion](https://github.com/youngyangyang04/leetcode-master/blob/master/problems/0028.实现strStr.md)
>
> [459. Repeated Substring Pattern](https://leetcode.com/problems/repeated-substring-pattern/)

## Stack and Queue

- When we use **`Stack`**, elements after `stack[i]` will not affect elements before `stack[i]`.
  > [155. Min Stack](https://leetcode.com/problems/min-stack/)
  >
  > - The minimum number of the stack may be changed after pushing and popping. But to each elements, when it is at the peek of the stack, there is a fixed  minimum number mapping to it.

### Monitonic Stack

- Keep the elements in the Stack monotonic increasing / decreasing by popping all the in-stack elements which are larger / smaller than the element that is going to be pushed into the Stack.

>[84. Largest Rectangle in Histogram](https://leetcode.com/problems/largest-rectangle-in-histogram/)
>
> - Pay attention to the interval (which means width) when calculating the area.
> - Need to push -1 to the stack at the very beginning as a boundary.
>
>[85. Maximal Rectangle](https://leetcode.com/problems/maximal-rectangle/)
>
> - How to calculating the height of each row's histogram without extra time complexity.
>
> ```java
>int[] heights = new int[cols];
>        
>        for(int i=0; i<rows; i++){
>            for(int j=0; j<cols; j++){
>                heights[j] = matrix[i][j] == '1' ? heights[j] + 1 : 0;
>            }
>        }
> ```

### Monotonic Queue

- Keep the elements in the Queue monotonic increasing / decreasing by removing all the elements larger / smaller than the element which is going to be added to the Queue. Removing and adding elements should at the same end.

> [239. Sliding Window Maximum](https://leetcode.com/problems/sliding-window-maximum/)

&nbsp;

## Binary Tree

1. recursive
2. iterative + stack
3. Morris Traversal (without additional space)
   - > [114. Flatten Binary Tree to Linked List](https://leetcode.com/problems/flatten-binary-tree-to-linked-list/solution/)

### Traversal

Only DFS has traversal order.  
(the traversal order is the order in which the rood nodes are visited.)

- preorder traversal
- inorder traversal
- postorder traversal

### BST (Binary Search Tree)

recursion + memory -> Dynamic Problem

To test whether a binary tree is a **valid BST**, use **inorder traversal** to turn the tree into an array and test whether the array is ascending.

> [98. Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/)
