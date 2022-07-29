# Data Structure

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
