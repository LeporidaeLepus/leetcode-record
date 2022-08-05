# Data Structure

[Array](#Array)  
[Linked List](#Linked-List)

## Array

- Pay attention to the ***empty array*** and ***null.***
- Memory address is allocated succesively to elements in array.  
- Problems about 'sum' can be transformed into problems about 'difference'. Then we can use **HashMap** to decrease O().  
- Problems don't allow duplicated elements can be solved by **HashSet**.  
  - We sort the array first and put an element into the HashSet every time we meet an new one. Then finding a completment in the HashSet means this complement is in the array and it's an result we need.

### Two Pointers

- fast pointer & slow pointer
- right pointer & left pointer

**Used in:** *remove elements*;

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
><mark>TODO: [2326. Spiral Matrix IV](https://leetcode.com/problems/spiral-matrix-iv/)</mark>

## Linked List
