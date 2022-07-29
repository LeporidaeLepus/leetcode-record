# Algorithm

## Binary Search

- Time complexity = O(log(n))
- Sorted arrays, no duplicated elements.

>[4. Median of two arays](https://leetcode.com/problems/median-of-two-sorted-arrays/)
>
>We need to find the kth large number. Since the left of Amid and Bmid are the smallest part of A and B and totally have k number.So if A\[Amid\] < B\[Bmid\], then A\[Amid\] and the left part of Amid must be smaller then the kth large number.
>
>The reason why Bmid and the right part of Bmid must be larger than the kth large number is the same as above.
>
> - After the search of k1 elements, we still have (k-k1) elements to search.
> - If the Amid_n is equan or larger to the length of A, then the next Amid_(n+1) should be cut down, which means we should deal it as AA\[Amid\] > B\[Bmid\].
