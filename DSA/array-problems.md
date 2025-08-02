
# Array Problems and Solutions

## 1. Maximum Subarray Sum (Kadane's Algorithm)

### Problem
Given an integer array `nums`, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

### Visual Explanation
```
Array: [-2, 1, -3, 4, -1, 2, 1, -5, 4]

Start at index 3 → [4, -1, 2, 1] → Sum = 6 (Maximum)
```

### Brute Force Approach

```java
public int maxSubArray(int[] nums) {
    int maxSum = nums[0];
    for (int i = 0; i < nums.length; i++) {
        int sum = 0;
        for (int j = i; j < nums.length; j++) {
          for(int k=i; k<=j; k++){
              sum += nums[j];
           }
            maxSum = Math.max(maxSum, sum);
        }
    }
    return maxSum;
}
```

- **Time Complexity:** O(n^3)
- **Space Complexity:** O(1)

### Optimization of Brute Force
```java
public int maxSubArray(int[] nums) {
    int maxSum = nums[0];
    for (int i = 0; i < nums.length; i++) {
        int sum = 0;
        for (int j = i; j < nums.length; j++) {
            sum += nums[j];
            maxSum = Math.max(maxSum, sum);
        }
    }
    return maxSum;
}
```

- **Time Complexity:** O(n²)
- **Space Complexity:** O(1)

### Optimal solution using Kadane's Algorithm
**Observations:**
-  if we add 2 positive numbers, we get a postive number
-  if we add a higher postive number with lower negative number, we get a positive number
-  if we add a positive number with a higher negative number, we get a negative number
- At every step:
    - Either extend the previous subarray (currentSum + arr[i]), or
    - Start a new subarray from arr[i] when my currentsum becomes < 0.
- edge case:
    - what if all the numbers in the array are -ve, its sum is going to be -ve
    - to get exact answer, reset the current sum to 0 after assigning the maxSum value to the greater element of (currentSum, maxSum)
  
```java
public int maxSubArray(int[] nums) {
    int maxSum = nums[0];
    int currSum = 0;
    for (int i = 0; i < nums.length; i++) {
            currSum += nums[i];
            maxSum = Math.max(maxSum, currSum);
            if(currSum < 0){
               currSum = 0;
            }
    }
    return maxSum;
}
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

---
## 2. Maximum Subarray Product

### Problem
Given an integer array `nums`, find the contiguous subarray (containing at least one number) which has the largest product and return its product.

### Visual Explanation
```
Array: [2, 3, -3, -5, 6, -1, 4]

Start at index 0 → [2, 3, -3, -5, 6] → Product = 540 (Maximum)
```

### Brute Force Approach

```java
public int maxSubArrayProduct(int[] nums) {
    int maxProduct = nums[0];
    for (int i = 0; i < nums.length; i++) {
        int prod = 1;
        for (int j = i; j < nums.length; j++) {
          for(int k=i; k<=j; k++){
              prod *= nums[j];
           }
            maxProduct = Math.max(maxProduct, prod);
        }
    }
    return maxProduct;
}
```

- **Time Complexity:** O(n^3)
- **Space Complexity:** O(1)

### Optimization of Brute Force
```java
public int maxSubArrayProduct(int[] nums) {
    int maxProduct = nums[0];
    for (int i = 0; i < nums.length; i++) {
        int prod = 1;
        for (int j = i; j < nums.length; j++) {
            prod *= nums[j];
            maxProduct = Math.max(maxProduct, prod);
        }
    }
    return maxProduct;
}
```

- **Time Complexity:** O(n²)
- **Space Complexity:** O(1)

### Optimal solution
**Observations:**
- if arr has all positive numbers, max product = product of all elements in arr.
- if arr has even number of negative numbers, max product = product of all elements in arr.
- if arr has even number of negative numbers, we need to remove one negative element such that the subarray forming on its left or right gives the maximum product.
- if arr has zeroes, we need to find the subarray forming on its left or right that gives the maximum product.
- This means, our max product will be either somewhere on the prefix or suffix
- we keep track of having product from both prefix and suffix for each negative element we traverse.
- we handle zero by resetting the prefix/suffix sum to 1 and starting to calculate max product for new subarray, as multiplying by zero would lead to zero.

```java
public int maxSubArray(int[] nums) {
    int maxProduct = nums[0];
    int prefix = 1;
    int suffix = 1;
    int n = nums.length
    for (int i = 0; i < n; i++) {
            if(prefix == 0) prefix = 1;
            if(suffix == 0) suffix = 1;
            prefix *= nums[i];
            suffix *= nums[n-i-1];
            maxProduct = Math.max(maxProduct, Math.max(prefix, suffix));
    }
    return maxProduct;
}
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

---

## 3. Best Time To Buy And Sell Stocks

### Problem
You are given an array of prices where prices[i] is the price of a given stock on the ith day.
You want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock.
Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return 0.
Note that you can sell the stock at > i only if you buy a stock at i

### Visual Explanation
```
Array: [7, 1, 5, 3, 6, 4]

If we buy a stock at index 1 at price 1 → we can sell it at index 4 at price 6
Max Profit = 6 - 1 = 5
```

### Brute Force Approach
-   We run an outer loop for making a purchase of stock on each day
-   We run an inner loop from i+1 day and calculate the profit for each selling day
-   We keep the track of the max Profit gained and update accordingly

```java
public int maxProfit(int[] prices) {
    int maxProfit = 0;
    for (int i = 0; i < nums.length; i++) {
        for (int j = i+1; j < nums.length; j++) {
            int profit = prices[j] - prices[i];
            maxProfit = Math.max(maxProfit, profit);
        }
    }
    return maxProfit;
}
```

- **Time Complexity:** O(n^2)
- **Space Complexity:** O(1)

### Optimal solution

**Observations:**
- Treat each day as a selling day
- Keep track of the best buy for each selling price which is going to be the minimum price to be found, initially keep it the value at index 0.
- if my selling price is greater than best buy, calculate the maximum profit to be made and update.
- otherwise, we update the current best buy with the minimum of selling price & best buy and move forward.

```java
public int maxProfit(int[] prices) {
    int maxProfit = 0;
    int bestBuy = prices[0];
     for(int i=1; i<prices.length; i++){
         if(prices[i] > bestBuy){
             maxProfit = Math.max(maxProfit, prices[i] - bestBuy);
         }
         bestBuy = Math.min(prices[i], bestBuy);
    }
    return maxProfit;
}
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

---
## 4. Product Of Array Except Self

### Problem
You are given an array of integer.
You have to return an array where the value at each index = product of all element except the element at current index.
Note that you are not allowed to use division operation.

### Visual Explanation
```
Array: [5, 2, 3, 4]

Result = [24, 60, 40, 30]
24 =  2 * 3 * 4 (index value at 1 * index value at 2 * index value at 3)
60 = 5 * 3 * 4 (index value at 0 * index value at 2 * index value at 3)
40 = 5 * 2 * 4 (index value at 0 * index value at 1 * index value at 3)
30 = 5 * 2 * 3 (index value at 0 * index value at 1 * index value at 2)
```
### Solution 1
- calculate the total product and divide it by each element at curr index.
- This solution cannot be used as division operation is not allowed.

### Brute Force Approach
-   We run an outer loop for tp keep track of current index
-   We run an inner loop to calculate the product of all elements except the current index
-   We update and return the resultant array

```java
public int[] productExceptSelf(int[] nums) {
    int[] result = new int[nums.length];
    for (int i = 0; i < nums.length; i++) {
        int prod = 1;
        for (int j = 0; j < nums.length; j++){
            if(i!==j){
               prod*=nums[j];
            }
        }
        result[i] = prod;
    }
    return result;
}
```

- **Time Complexity:** O(n^2)
- **Space Complexity:** O(1) (Excluding the memory to return output)

### Optimal solution

**Observations:**
- For index i , we need the product of all elements on its left and product of all elements on its right.
- the value on that index will be = left product * right product.
- we create a resultant array, store the product of the prefix array for each index in the resultant array with a for loop
- we calculate the product of suffix array for each index and multiply with the prefix and update the resultant array in the next for loop

```java
public int[] productExceptSelf(int[] nums) {
    int n = nums.length;
    int[] result = new int[n];
    result[0] = 1; // since there are no elements to the left at index 0
    // set prefix products
    for(int i=1; i<n; i++){
         result[i] = result[i-1] * nums[i-1];
    }
    // calculate suffix product and update result array
    int suffix = 1; // suffix of last element since there are no elements to its right
    for(int i=n-2; i>=0; i--){
       suffix*=nums[i+1];
       result[i] *= suffix;
    }
    return result;
}
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(1) (Excluding the memory to return output)

---

## 5. Rotate Array By K Positions

### 4 Problems
- Left rotate an array by one place
- Right rotate an array by one place
- Left rotate an array by k places
- Right rotate an array by k places

### Visual Explanation
```
Array: [1, 2, 3, 4, 5]

Left rotate by 1 place : Result = [2, 3, 4, 5, 1]
Right rotate by 1 place : Result = [5, 1, 2, 3, 4]
Left rotate by k places (k=3) : Result = [4, 5, 1, 2, 3]
Right rotate by k places (k=3) : Result = [3, 4, 5, 1, 2]
```
### Rotate by one place 
- Left rotate
```java
public int[] leftRotateByOnePlace(int[] nums) {
    int temp = nums[0];
    int n = nums.length;
    for (int i = 1; i < n; i++) {
        nums[i-1] = nums[i];
    }
    nums[n-1] = temp;
    return nums;
}
```
- Right rotate
```java
public int[] rightRotateByOnePlace(int[] nums) {
    int n = nums.length;
    int temp = nums[n-1];
   // we reverse the loop to avoid data loss due to data overwrite when shifting to right.
   // nums[1] = nums[0] data lost at one in first iteration.
    for (int i = n-2; i >= 0; i--) {
        nums[i] = nums[i+1];
    }
    nums[0] = temp;
    return nums;
}
```

- **Time Complexity:** O(n)
- **Space Complexity:** O(1) (No extra space needed)

### Observations
-   To rotate the array to the left or right by k places, one thing to observe is that, we get the same original array on n rotation when n is the length of array.
-   For example: n = 7, k = 9, we need to perform 2 extra rotations, because the 7 rotation will give us the original array.
-   For k < n, we need to perform given k rotations.
-   For k > n, we need to calculate extra rotations to perform, that is, k = k % n

### Brute Force Approach

- Create a temp array and store the first `k` elements (for **left rotate**) or the last `k` elements (for **right rotate**) in it.
- For **left rotate**:
  - Shift `n - k` elements to `k` places to the left.
  - i.e., for `i = k` to `n-1`, shift: `arr[i - k] = arr[i]`.
    - Example: For `k = 3`, `n = 6`, bring index `i = 3` to `i = 0` to shift by 3 places.
  - Then copy the elements from the temp array to the remaining `k` positions.
  - i.e., for `i = n-k` to `n-1`, copy: `arr[i] = temp[i - (n - k)]`
- For **right rotate**:
  - Shift `n - k` elements to `k` places to the right.
  - i.e., for `i = 0` to `n-k-1`, shift: `arr[i + k] = arr[i]`
    - Example: For `k = 3`, `n = 6`, bring index `i = 0` to `i = 3` to shift by 3 places.
  - Then copy the elements from the temp array to the first `k` positions.
  - i.e., for `i = 0` to `k-1`, copy: `arr[i] = temp[i]`
    
**✅ Left Rotate**
```java
public int[] leftRotateByk(int[] nums, int k, int n) {
    // calculate extra rotations if k greater than n
    k = k%n;
    int[] temp = new int[k];
    // copy first k elements
    for(int i=0; i<k; i++){
      temp[i] = nums[i];
    }
    // shift n-k elements to the left by k places
    for (int i = k; i < n; i++) {
      nums[i-k] = nums[i];
    }
    // copy the elements in temp after n-k elements
    for(int i = n-k; i<n; i++){
        nums[i] = temp[i-n-k];
    }
    return nums;
}
```
**✅ Right Rotate**
```java
public int[] rightRotateByk(int[] nums, int k, int n) {
    // calculate extra rotations if k greater than n
    k = k%n;
    int[] temp = new int[k];
    // copy last k elements
    for(int i=0; i<k; i++){
      temp[i] = nums[n-k+i];
    }
    // shift n-k elements to the right by k places
    // to preserve data i.e avoid data loss due to data overwrite while shifting to the right, we shift in reverse
    for (int i = n-k-1; i >=0; i--) {
      nums[i+k] = nums[i];
    }
    // copy the elements in temp before n-k elements
    for(int i = 0; i < k; i++){
        nums[i] = temp[i];
    }
    return nums;
}
```

- **Time Complexity:** O(k) + O(n-k) + O(k) = O(n+k)
- **Space Complexity:** O(k) (Since we are taking extra space to store k elements)

### Optimal solution

**Observations:**
- For left rotation:
   - arr = [1, 2, 3, 4, 5] Left rotate by k places (k=3) : Result = [4, 5, 1, 2, 3]
   - looking at the pattern
   - reverse first 3 elements = [ 3, 2, 1, 4, 5]
   - reverse remaining n-k elements = [3, 2, 1, 5, 4]
   - reverse entire array = [4, 5, 1, 2, 3] = same as o/p 
- For right rotation:
   - arr = [1, 2, 3, 4, 5] Right rotate by k places (k=3) : Result = [3, 4, 5, 1, 2]
   - looking at the pattern
   - reverse entire array = [5, 4, 3, 2, 1]
   - reverse first k elements = [ 3, 4, 5, 2, 1]
   - reverse remaining n-k elements = [3, 4, 5, 1, 2] = same as o/p.
     
**✅ Left Rotate**
```java
public int[] leftRotate(int[] nums, int k, int n) {
   if (n == 0 || k == 0 || k % n == 0) return nums;
   k = k % n; // handle rotations for k > n 
   reverse(nums, 0, k-1);
   reverse(nums, k, n-1);
   reverse(nums, 0, n-1);
   return nums;
}
private void reverse(int[] nums, int start, int end){
      while(start<end){
        int temp = nums[start];
         nums[start] = nums[end];
         nums[end] = temp;
         start++;
         end--;
      }
}
```
**✅ Right Rotate**
```java
public int[] rightRotate(int[] nums, int k, int n) {
   if (n == 0 || k == 0 || k % n == 0) return nums;
   k = k % n; // handle rotations for k > n
   reverse(nums, 0, n-1);
   reverse(nums, 0, k-1);
   reverse(nums, k, n-1);
   return nums;
}
private void reverse(int[] nums, int start, int end){
      while(start<end){
        int temp = nums[start];
         nums[start] = nums[end];
         nums[end] = temp;
         start++;
         end--;
      }
}
```

- **Time Complexity:** O(k)+O(n-k)+O(n) --> O(2n) --> O(n)
- **Space Complexity:** O(1) (No extra space is used)

---

## 2. Custom Resizable Array Implementation in Java

### Problem
Create a custom ArrayList class from scratch.

### Code

```java
public class MyArrayList<T> {
    private Object[] data;
    private int size = 0;
    private static final int INITIAL_CAPACITY = 10;

    public MyArrayList() {
        data = new Object[INITIAL_CAPACITY];
    }

    public void add(T value) {
        ensureCapacity();
        data[size++] = value;
    }

    public T get(int index) {
        checkIndex(index);
        return (T) data[index];
    }

    public void remove(int index) {
        checkIndex(index);
        for (int i = index; i < size - 1; i++) {
            data[i] = data[i + 1];
        }
        data[--size] = null; // avoid memory leak
    }

    private void ensureCapacity() {
        if (size == data.length) {
            Object[] newData = new Object[data.length * 2];
            for (int i = 0; i < size; i++) {
                newData[i] = data[i];
            }
            data = newData;
        }
    }

    private void checkIndex(int index) {
        if (index < 0 || index >= size)
            throw new IndexOutOfBoundsException("Index: " + index + ", Size: " + size);
    }

    public int size() {
        return size;
    }
}
```

### Key Concepts
- Internal array doubling when full
- Manual shift of elements during remove
- `data[--size] = null` prevents memory leak (object still referenced if not set to null)

---

## 3. Loop Analysis: `while(i < n) { i = 2 * i; }`

### Question
Why does this run `k+1` times?

### Explanation
If `i = 1` and `i` doubles each time until `i >= n`:
Let `2^k < n ≤ 2^{k+1}` → then it runs `k+1` times.

### Example
```
n = 20
i: 1 → 2 → 4 → 8 → 16 → 32 → stop
Steps = 6 (k = 5, so k+1 = 6)
```

---

## GitHub Directory Addition

### To add a new directory on GitHub:

1. Go to your repository on GitHub.
2. Click **"Add file"** → **"Create new file"**.
3. In the filename box, type: `folder-name/README.md` (or any file).
4. GitHub will auto-create that folder.
5. Add content, commit → Done!
