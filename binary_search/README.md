# binary search

## Approach 1: Find the Exact Value

### Intuition

We start from the most basic and elementary template.

First, we define the search space using two boundary indexes, `left and right `, all possible indexes are within the inclusive range`[left, right]`. We shall continue searching over the search space as long as it is not empty. A general way is to use a while loop with the condition `left <= right`, so we can break out of this loop if we empty the range or trigger other conditions which we will discuss later.

![Tux, the Linux mascot](https://assets.leetcode.com/static_assets/media/original_images/704_fix/b1_fix.png)

The next step is to find the 'pivot point', the middle index that divides the search space into two halves. We need to compare the value at the middle index nums[mid] with target, the purpose of this step is to cut one half that is guaranteed not to contain target.

  - If nums[mid] = target, it means we find target, and the job is done! We can break the loop by returning mid.
  - If nums[mid] < target, combined with the array is sorted, we know that all values in the left half are smaller than target, so we can safely cut this half by letting left = mid + 1.
  - If nums[mid] > target, it means all values in the right half are larger than target and can be cut safely!


![Tux, the Linux mascot](https://assets.leetcode.com/static_assets/media/original_images/704_fix/b2_fix.png)

Does this loop ever stop? Yes, take the following picture as an example, suppose we are searching over an array of size 1, in this case, left, right, and mid all stand for the only index in the array. In any of the three conditions, we trigger one of the break statements and stop the loop.

![Tux, the Linux mascot](https://assets.leetcode.com/static_assets/media/original_images/704_fix/b3_fix.png)

### Algorithm

  - Initialize the boundaries of the search space as left = 0 and right = nums.size - 1.
  - If there are elements in the range [left, right], we find the middle index mid = (left + right) / 2 and compare the middle value nums[mid] with target:
        - If nums[mid] = target, return mid.
        - If nums[mid] < target, let left = mid + 1 and repeat step 2.
        - If nums[mid] > target, let right = mid - 1 and repeat step 2.
    - We finish the loop without finding target, return -1.

### Implementation
```cpp
class Solution {
public:
    int search(vector<int>& nums, int target) {
        // Set the left and right boundaries
        int left = 0, right = int(nums.size()) - 1;
        
        // Under this condition
        while (left <= right) {
            // Get the middle index and the middle value.
            int mid = left + (right - left) / 2;
            
            // Case 1, return the middle index.
            if (nums[mid] == target) {
                return mid;
            } 
            // Case 2, discard the smaller half.
            else if (nums[mid] < target) {
                left = mid + 1;   
            } 
            // Case 3, discard the larger half.
            else {
                right = mid - 1;
            }
        }
        
        // If we finish the search without finding target, return -1.
        return -1;
    }
};
```
