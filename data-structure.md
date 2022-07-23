# Data Structure

## Array

- Memory address is allocated succesively to elements in array.  
- Problems about 'sum' can be transformed into problems about 'difference'. Then we can use **HashMap** to decrease O().  
- Problems don't allow duplicated elements can be solved by **HashSet**.  
  - We sort the array first and put an element into the HashSet every time we meet an new one. Then finding a completment in the HashSet means this complement is in the array and it's an result we need.
