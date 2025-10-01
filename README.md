/*
# Experiment 22: Big-O-Notation
# Name:Ishika Singhal
# Class: ENTC A2
# PRN: 24070123048

---------------------------------------------------------------
# Title
Algorithm Analysis using Big O Notation

---------------------------------------------------------------
# Aim
To study and analyze the efficiency of algorithms using Big O Notation.

---------------------------------------------------------------
# Objectives
1. Understand the importance of algorithm analysis.
2. Study time and space complexity.
3. Learn asymptotic notations (O, Ω, Θ).
4. Analyze best, average, and worst case scenarios.
5. Compare the growth rates of algorithms.
6. Relate algorithm efficiency to real-world applications.

---------------------------------------------------------------
# Theory
- An algorithm is a step-by-step solution to a problem.
- Efficiency matters: some algorithms work well on large data, others do not.
- Time Complexity → how execution time increases with input size.
- Space Complexity → how much memory the algorithm requires.
- Big O Notation → standard way to represent upper bound (worst case).
- Growth classes:
  O(1), O(log n), O(n), O(n log n), O(n^2), O(2^n), O(n!)
- Best case → Ω, Average case → Θ, Worst case → O.

---------------------------------------------------------------
# Conclusion
1. Big O notation abstracts away machine details and focuses on input growth.
2. Efficient algorithms (O(log n), O(n)) scale better than inefficient ones (O(n^2), O(2^n)).
3. Choosing the right algorithm is critical for large datasets.
4. Algorithm analysis helps in building scalable and optimized systems.
*/

#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

// ---------------------------------------------------
// Linear Search - O(n)
int linearSearch(vector<int> arr, int key) {
    for (int i = 0; i < arr.size(); i++) {
        if (arr[i] == key)
            return i;
    }
    return -1;
}

// ---------------------------------------------------
// Binary Search - O(log n) (works on sorted arrays)
int binarySearch(vector<int> arr, int key) {
    int left = 0, right = arr.size() - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (arr[mid] == key)
            return mid;
        else if (arr[mid] < key)
            left = mid + 1;
        else
            right = mid - 1;
    }
    return -1;
}

// ---------------------------------------------------
// Bubble Sort - O(n^2)
void bubbleSort(vector<int>& arr) {
    int n = arr.size();
    for (int i = 0; i < n - 1; i++) {
        for (int j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1])
                swap(arr[j], arr[j + 1]);
        }
    }
}

// ---------------------------------------------------
// Quick Sort - O(n log n) average, O(n^2) worst case
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

// ---------------------------------------------------
// Main function
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

    // Sort array for Binary Search
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
