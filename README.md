# Bucket-Sort-Algorithm

<i>
Bucket sort is a sorting technique that involves dividing elements into various groups, or buckets. These buckets are formed by uniformly distributing the elements. Once the elements are divided into buckets, they can be sorted using any other sorting algorithm. Finally, the sorted elements are gathered together in an ordered fashion.
</i>

## Bucket Sort Algorithm:
Create n empty buckets (Or lists) and do the following for every array element arr[i].

- Insert arr[i] into bucket[n*array[i]]
- Sort individual buckets using insertion sort.
- Concatenate all sorted buckets.
  
## How does Bucket Sort work?
To apply bucket sort on the input array [0.78, 0.17, 0.39, 0.26, 0.72, 0.94, 0.21, 0.12, 0.23, 0.68], we follow these steps:

<h2>Step 1:</h2> Create an array of size 10, where each slot represents a bucket.


<div align="center">
  <img src="https://media.geeksforgeeks.org/wp-content/uploads/20230705162208/file.png" width='400'>
</div>


<h2>Step 2: </h2>Insert elements into the buckets from the input array based on their range.

Inserting elements into the buckets:

- Take each element from the input array.
- Multiply the element by the size of the bucket array (10 in this case). For example, for element 0.23, we get 0.23 * 10 = 2.3.
- Convert the result to an integer, which gives us the bucket index. In this case, 2.3 is -converted to the integer 2.
- Insert the element into the bucket corresponding to the calculated index.
- Repeat these steps for all elements in the input array.


<div align="center">
  <img src="https://media.geeksforgeeks.org/wp-content/uploads/20230705162234/file.png" width='400'>
</div>


<h2>Step 3: </h2>Sort the elements within each bucket. In this example, we use quicksort (or any stable sorting algorithm) to sort the elements within each bucket.

Sorting the elements within each bucket:

- Apply a stable sorting algorithm (e.g., Bubble Sort, Merge Sort) to sort the elements within each bucket.
- The elements within each bucket are now sorted.


<div align="center">
  <img src="https://media.geeksforgeeks.org/wp-content/uploads/20230705162300/file.png" width='400'>
</div>


<h2>Step 4: </h2>Gather the elements from each bucket and put them back into the original array.

Gathering elements from each bucket:

- Iterate through each bucket in order.
- Insert each individual element from the bucket into the original array.
- Once an element is copied, it is removed from the bucket.
- Repeat this process for all buckets until all elements have been gathered.


<div align="center">
  <img src="https://media.geeksforgeeks.org/wp-content/uploads/20230705162320/file.png" width='400'>
</div>


<h2>Step 5: </h2>The original array now contains the sorted elements.

The final sorted array using bucket sort for the given input is [0.12, 0.17, 0.21, 0.23, 0.26, 0.39, 0.68, 0.72, 0.78, 0.94].


<div align="center">
  <img src="https://media.geeksforgeeks.org/wp-content/uploads/20230705162345/file.png" width='400'>
</div>


# Implementation of Bucket Sort Algorithm:

```
#include <iostream>
#include <vector>
using namespace std;

// Insertion sort function to sort individual buckets
void insertionSort(vector<float>& bucket) {
    for (int i = 1; i < bucket.size(); ++i) {
        float key = bucket[i];
        int j = i - 1;
        while (j >= 0 && bucket[j] > key) {
            bucket[j + 1] = bucket[j];
            j--;
        }
        bucket[j + 1] = key;
    }
}

// Function to sort arr[] of size n using bucket sort
void bucketSort(float arr[], int n) {
    // 1) Create n empty buckets
    vector<float> b[n];

    // 2) Put array elements in different buckets
    for (int i = 0; i < n; i++) {
        int bi = n * arr[i];
        b[bi].push_back(arr[i]);
    }

    // 3) Sort individual buckets using insertion sort
    for (int i = 0; i < n; i++) {
        insertionSort(b[i]);
    }

    // 4) Concatenate all buckets into arr[]
    int index = 0;
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < b[i].size(); j++) {
            arr[index++] = b[i][j];
        }
    }
}

// Driver program to test above function
int main() {
    float arr[] = {0.897, 0.565, 0.656, 0.1234, 0.665, 0.3434};
    int n = sizeof(arr) / sizeof(arr[0]);
    bucketSort(arr, n);

    cout << "Sorted array is \n";
    for (int i = 0; i < n; i++) {
        cout << arr[i] << " ";
    }
    return 0;
}
```

# Output:

```
Sorted array is 
0.1234 0.3434 0.565 0.656 0.665 0.897
```

# Complexity:

- Time Complexity: O(n2)
- Auxiliary Space: O(n+k)
