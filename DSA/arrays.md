# DATA STRUCTURE - ARRAYS
- it stores data in a continuous manner in the RAM
- it stores only homogenous type of data
- its index based starting from index 0
- internally -->
    - memory location is computed easily using indexes
    - memory value is set or updated
    - example: int[] arr = new int[10] --> memory of 40 bytes will be reserved
                                     each item having 4 bytes
    - if we want to set arr[2]
         -  0 + (4*2) = 8 --> this way memory location is computed
         -  and easily the value is set at this location
    - So, fetching or setting array item takes O(1) time complexity since its a constant operation.

### Advantage 
- Random access of memory - very fast (retrieve or set element at index)

### Drawbacks
- static size (fixed size known at compile time)
- adding or deleting elements in the beginning / middle of array is inefficient due to its fixed size.
- It involves shifting of its following elements which consumes more time
- Alternative for static size issue - use vectors / array list
- Alternative for insertion/deletion - use linked list
