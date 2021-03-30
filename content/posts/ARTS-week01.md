---
title: "ARTS Week01"
date: 2020-05-23T11:43:03+08:00
categories: ["arts"]
GHissueID: 1
---

### Algorithm

> Given an array of integers, return indices of the two numbers such that they add up to a specific target.
>
> You may assume that each input would have exactly one solution, and you may not use the same element twice.
>
> Example:
>
> Given nums = [2, 7, 11, 15], target = 9,
>
> Bacause nums[0] + num[1] = 2 + 7 =.9
>
> return [0, 1].

``` python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        key_map = {}
        for idx, num in enumerate(nums):
            if (target - num) in key_map:
                return [key_map[target-num], idx]
             key_map[num] = idx
            
        return [-1, -1]
```

### Review

learn about how Dict is implemented in Python.

Keynotes:

1, python use hash tables behind Dict.

2, Use Open addressing as method of collision resolution. j =( (5 * j) + 1 + perturb) mod (2** i); perturb >>= PERTURB_SHIFT;

3, AddItem will trigger resize when active + dummy is greater than 2/3



### Tips

Don't use `keys` command in redis, unless you know what you are doning.

`keys` command will **block** redis until it finish searching all the keys.

`keys` will be slower and  slower as keys' number grows. which is pretty unpredictable. Even the smallest database can grow really large.

If you must to, use `scan` instead, scan command will only return a few keys and a cursor, you can continue to iterate all keys.

### Share

an good article about **Dict** implementation in Python.

[python-dictionary-implementation](https://www.laurentluce.com/posts/python-dictionary-implementation/)



