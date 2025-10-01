/*
# Experiment 22: Big-O-Notation
# Name:Ishika Singhal
# Class: ENTC A2
# PRN: 24070123048

## Title
Algorithm Analysis using Big O Notation

--------------------------------------------------------------------
## Aim
To learn how to measure the efficiency of algorithms using Big O Notation 
and to understand how execution time and memory requirements change 
with respect to input size.

--------------------------------------------------------------------
## Objectives
1. To explore why algorithm analysis is important in software development.  
2. To study time and space complexity of algorithms.  
3. To learn about asymptotic notations (Big O, Big Ω, Big Θ).  
4. To examine algorithms under best-case, worst-case, and average-case performance.  
5. To compare how algorithms scale when input size increases.  
6. To understand how complexity affects performance on practical applications.  

--------------------------------------------------------------------
## Theory
- An algorithm is a systematic method to solve a problem.  
- Multiple algorithms can solve the same problem, but their efficiency differs.  
- Algorithm analysis considers:  
   • Time Complexity – growth of execution time.  
   • Space Complexity – memory usage.  
- Big O Notation generalizes performance independent of hardware.  
- Growth classes include O(1), O(log n), O(n), O(n log n), O(n²), O(2ⁿ), O(n!).  
- Best case → Ω, Average case → Θ, Worst case → O.  

--------------------------------------------------------------------
## Growth of Functions
- O(1): Constant → Accessing an array element.  
- O(log n): Logarithmic → Binary Search.  
- O(n): Linear → Linear Search.  
- O(n log n): Linearithmic → Merge Sort.  
- O(n²): Quadratic → Bubble Sort.  
- O(2ⁿ): Exponential → Recursive Fibonacci.  
- O(n!): Factorial → Traveling Salesman Problem.  

--------------------------------------------------------------------
## Comparison Table

| Complexity | Category         | Example Algorithms          | n=10  | n=100  | n=1000  |
|------------|------------------|-----------------------------|-------|--------|---------|
| O(1)       | Constant         | Array access                | 1     | 1      | 1       |
| O(log n)   | Logarithmic      | Binary Search               | 3     | 7      | 10      |
| O(n)       | Linear           | Linear Search               | 10    | 100    | 1000    |
| O(n log n) | Linearithmic     | Merge Sort, Quick Sort      | 30    | 700    | 10000   |
| O(n²)      | Quadratic        | Bubble Sort, Selection Sort | 100   | 10000  | 1,000,000 |
| O(2ⁿ)      | Exponential      | Fibonacci recursion         | 1024  | Huge   | Extremely Huge |

--------------------------------------------------------------------
## Program Summary
- Linear Search → O(n)  
- Binary Search → O(log n)  
- Bubble Sort → O(n²)  
- Quick Sort → O(n log n) average, O(n²) worst case  

--------------------------------------------------------------------
## Steps in Big O Analysis
1. Define input size n.  
2. Identify basic operation(s).  
3. Count operation frequency.  
4. Express as function of n.  
5. Drop constants and lower terms.  
6. Represent using asymptotic notation.  

--------------------------------------------------------------------
## Conclusion
1. Big O notation provides a standard way to evaluate algorithms.  
2. It focuses on growth rate, not actual runtime.  
3. Efficient algorithms scale better for large inputs.  
4. Algorithm analysis is critical for real-world applications.  
====================================================================
*/

#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

// ---------------------------
// Linear Search - O(n)
int linearSearch(vector<int> arr, int key) {
    for (int i = 0; i < arr.size(); i++) {
        if (arr[i] == key)
            return i;
    }
    return -1;
}

// ---------------------------
// Binary Search - O(log n)
int binarySearch(vector<int> arr, int key) {
    int left = 0, right = arr.size() - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (arr[mid] == key) return mid;
        else if (arr[mid] < key) left = mid + 1;
        else right = mid - 1;
    }
    return -1;
}

// ---------------------------
// Bubble Sort - O(n²)
void bubbleSort(vector<int>& arr) {
    int n = arr.size();
    for (int i = 0; i < n - 1; i++) {
        for (int j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1])
                swap(arr[j], arr[j + 1]);
        }
    }
}

// ---------------------------
// Quick Sort - O(n log n) avg, O(n²) worst
int partition(vector<int>& arr, int low, int high) {
    int pivot = arr[high];
    int i = (low - 1);
    for (int j = low; j <= high - 1; j++) {
        if (arr[j] < pivot) {
            i++;
            swap(arr[i], arr[j]);
        }
    }
    swap(arr[i + 1], arr[high]);
    return (i + 1);
}

void quickSort(vector<int>& arr, int low, int high) {
    if (low < high) {
        int pi = partition(arr, low, high);
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}

// ---------------------------
// Main Demonstration
int main() {
    vector<int> arr = {34, 7, 23, 32, 5, 62};
    int key = 23;

    cout << "Original Array: ";
    for (int x : arr) cout << x << " ";
    cout << "\n";

    // Linear Search
    int pos1 = linearSearch(arr, key);
    cout << "Linear Search for " << key << ": ";
    if (pos1 != -1) cout << "Found at index " << pos1 << "\n";
    else cout << "Not Found\n";

    // Sort for Binary Search
    sort(arr.begin(), arr.end());

    // Binary Search
    int pos2 = binarySearch(arr, key);
    cout << "Binary Search for " << key << ": ";
    if (pos2 != -1) cout << "Found at index " << pos2 << "\n";
    else cout << "Not Found\n";

    // Bubble Sort
    vector<int> arrBubble = {34, 7, 23, 32, 5, 62};
    bubbleSort(arrBubble);
    cout << "Array after Bubble Sort: ";
    for (int x : arrBubble) cout << x << " ";
    cout << "\n";

    // Quick Sort
    vector<int> arrQuick = {34, 7, 23, 32, 5, 62};
    quickSort(arrQuick, 0, arrQuick.size() - 1);
    cout << "Array after Quick Sort: ";
    for (int x : arrQuick) cout << x << " ";
    cout << "\n";

    return 0;
}
