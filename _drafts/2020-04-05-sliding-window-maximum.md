---
layout: post
title: Sliding Window Maximum
categories: [Deques,Queue,Sliding Window]
tags: [Sliding Window Maximum,Deques]
---

## **[Sliding Window Maximum](http://ismaildemirbilek.com)**

Given an array nums, there is a sliding window of size k which is moving from the very left of the array to the very right. You can only see the k numbers in the window. Each time the sliding window moves right by one position. Return the max sliding window.

__Follow up:__
Could you solve it in linear time?

__Example:__

```
Input: nums = [1,3,-1,-3,5,3,6,7], and k = 3
Output: [3,3,5,5,6,7] 
Explanation: 

Window position                Max
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7

```

### Solution:

### Using Deque: Time complexity O(n)


__Deque:__

>In computer science, a __double-ended queue__ (abbreviated to __deque__, pronounced _deck_) is an abstract data type that generalizes a queue, for which elements can be added to or removed from either the front (head) or back (tail).


Here __Deque__ is used to store elements in decreasing order <br/>
and only the elements which are possible to be maximum of the window.

Since we will require the position of an element in Deque to find if the 
element falls out of window, we will use Deque to store indexes instead of
elements.

In every time the front of the deque will hold the max element in the window!.


__Algorithm__:
First create a window of k elements – <br/>
    Every new element going into window(deque):
    1. Remove all the smaller elements indexes from the deque 
    (since these elements are no longer required) and 
    1. add the new element at the end. 
Once the window is created for first k elements then <br/>
    For every new element going into window(deque):
    1. Save the front index (since it is the index of max element of current window!).
    1. Remove the element index which falls outside the window.
    >i.e indexs (_from the front of window_) which are less than __i-k+1__.<br/>
    >Since a k size window will hold j-i+1 elements,
    where j and i are end and starting index of window.
    1. And again remove all the smaller elements indexes from the deque 
    (since these elements are no longer required) and 
    1. add the new element index at the end.
At the end max element the last window is yet to be saved,
    so we save it.


__C++__
{% highlight cpp %}
vector<int> maxSlidingWindow(vector<int>& nums, int k) {
    deque <int> dq;
        
    for(int i=0;i<k;i++){
        while(!dq.empty() && nums[dq.back()]<= nums[i]){
            dq.pop_back();
        }
        dq.push_back(i);
    }
        
    vector<int> res;
    for(int i=k;i<nums.size();i++){
            
        if(!dq.empty())
            res.push_back(nums[dq.front()]);
            
        while(!dq.empty() && dq.front()<i-k+1){
            dq.pop_front();
        }
            
        while(!dq.empty() && nums[dq.back()]<= nums[i]){
            dq.pop_back();
        }
        
        dq.push_back(i);
    }
    if(!dq.empty())
        res.push_back(nums[dq.front()]);
        
        
    return res;
}
{% endhighlight %}