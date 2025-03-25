
## Experiment 1: Binary Search with Divide and Conquer

### Aim
Develop a program and measure the running time for Binary Search with Divide and Conquer.

### Description
Binary Search is an efficient searching algorithm that follows the divide-and-conquer paradigm. It works on sorted arrays by repeatedly dividing the search interval in half. The algorithm compares the target value with the middle element of the array and eliminates half of the remaining elements based on the comparison.

### Algorithm
1. Initialize `low = 0` and `high = n-1` (where `n` is array length).
2. While `low ≤ high`:
   - Calculate `mid = low + (high - low)/2`.
   - If `array[mid]` equals target, return `mid`.
   - If `array[mid] > target`, set `high = mid - 1`.
   - If `array[mid] < target`, set `low = mid + 1`.
3. If element not found, return `-1`.

### Program
```c
#include <stdio.h>
#include <time.h>
#include <stdlib.h>

// Binary Search function using divide and conquer
int binarySearch(int arr[], int low, int high, int target) {
    if (low <= high) {
        int mid = low + (high - low) / 2;
        
        // If element is found at mid
        if (arr[mid] == target)
            return mid;
            
        // If element is smaller than mid
        if (arr[mid] > target)
            return binarySearch(arr, low, mid - 1, target);
            
        // If element is larger than mid
        return binarySearch(arr, mid + 1, high, target);
    }
    return -1;  // Element not found
}

int main() {
    int n, target;
    clock_t start, end;
    double cpu_time_used;
    
    // Input array size
    printf("Enter the size of array: ");
    scanf("%d", &n);
    
    int arr[n];
    
    // Input sorted array
    printf("Enter %d sorted elements:\n", n);
    for(int i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }
    
    // Input search element
    printf("Enter the element to search: ");
    scanf("%d", &target);
    
    // Measure start time
    start = clock();
    
    // Perform binary search
    int result = binarySearch(arr, 0, n-1, target);
    
    // Measure end time
    end = clock();
    
    // Calculate time taken
    cpu_time_used = ((double) (end - start)) / CLOCKS_PER_SEC;
    
    // Output results
    if(result == -1)
        printf("\nElement %d not found in array", target);
    else
        printf("\nElement %d found at index %d", target, result);
        
    printf("\nTime taken: %f seconds\n", cpu_time_used);
    
    return 0;
}

```

### Experiment Analysis
- **Time Complexity**:
  - Best Case: O(1) - when element is found at the middle.
  - Average Case: O(log n).
  - Worst Case: O(log n).
- **Space Complexity**: O(log n) due to recursive calls.

---

## Experiment 2: Merge Sort with Divide and Conquer

### Aim
Develop a program and measure the running time for Merge Sort with Divide and Conquer.

### Description
Merge Sort is an efficient sorting algorithm that follows the divide-and-conquer paradigm. It works by recursively dividing the array into two halves, sorting them independently, and then merging the sorted halves to create a fully sorted array.

### Algorithm
1. If array length ≤ 1, return array (base case).
2. Find middle point: `mid = length/2`.
3. Recursively divide array into two halves:
   - Left half: elements from index `0` to `mid-1`.
   - Right half: elements from index `mid` to end.
4. Recursively sort both halves.
5. Merge the sorted halves:
   - Create temporary arrays for both halves.
   - Compare elements and merge in sorted order.
   - Copy remaining elements if any.

### Program
```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

// Merge function to combine two sorted subarrays
void merge(int arr[], int left, int mid, int right) {
    int i, j, k;
    int n1 = mid - left + 1;
    int n2 = right - mid;
    
    // Create temporary arrays
    int L[n1], R[n2];
    
    // Copy data to temporary arrays
    for (i = 0; i < n1; i++)
        L[i] = arr[left + i];
    for (j = 0; j < n2; j++)
        R[j] = arr[mid + 1 + j];
    
    // Merge the temporary arrays back into arr
    i = 0;    // Initial index of first subarray
    j = 0;    // Initial index of second subarray
    k = left; // Initial index of merged subarray
    
    while (i < n1 && j < n2) {
        if (L[i] <= R[j]) {
            arr[k] = L[i];
            i++;
        }
        else {
            arr[k] = R[j];
            j++;
        }
        k++;
    }
    
    // Copy remaining elements of L[] if any
    while (i < n1) {
        arr[k] = L[i];
        i++;
        k++;
    }
    
    // Copy remaining elements of R[] if any
    while (j < n2) {
        arr[k] = R[j];
        j++;
        k++;
    }
}

// Merge Sort function
void mergeSort(int arr[], int left, int right) {
    if (left < right) {
        int mid = left + (right - left) / 2;
        
        // Sort first and second halves
        mergeSort(arr, left, mid);
        mergeSort(arr, mid + 1, right);
        
        // Merge the sorted halves
        merge(arr, left, mid, right);
    }
}

// Function to print array
void printArray(int arr[], int size) {
    for (int i = 0; i < size; i++)
        printf("%d ", arr[i]);
    printf("\n");
}

int main() {
    int n;
    clock_t start, end;
    double cpu_time_used;
    
    // Input array size
    printf("Enter the size of array: ");
    scanf("%d", &n);
    
    int arr[n];
    
    // Input array elements
    printf("Enter %d elements:\n", n);
    for(int i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }
    
    printf("\nOriginal array: ");
    printArray(arr, n);
    
    // Measure start time
    start = clock();
    
    // Perform merge sort
    mergeSort(arr, 0, n-1);
    
    // Measure end time
    end = clock();
    
    // Calculate time taken
    cpu_time_used = ((double) (end - start)) / CLOCKS_PER_SEC;
    
    printf("Sorted array: ");
    printArray(arr, n);
    
    printf("\nTime taken: %f seconds\n", cpu_time_used);
    
    return 0;
}
```

### Experiment Analysis
- **Time Complexity**:
  - Best Case: O(n log n).
  - Average Case: O(n log n).
  - Worst Case: O(n log n).
- **Space Complexity**: O(n).

---

## Experiment 3: Quick Sort with Divide and Conquer

### Aim
Develop a program and measure the running time for Quick Sort with Divide and Conquer.

### Description
Quick Sort is an efficient sorting algorithm that uses the divide-and-conquer strategy. It works by selecting a 'pivot' element from the array and partitioning the other elements into two sub-arrays according to whether they are less than or greater than the pivot.

### Algorithm
1. Choose a pivot element from the array.
2. Partition the array:
   - Place elements smaller than pivot to its left.
   - Place elements larger than pivot to its right.
3. Recursively apply steps 1-2 to the sub-array of elements with values less than the pivot.
4. Recursively apply steps 1-2 to the sub-array of elements with values greater than the pivot.

### Program
```c
#include <stdio.h>
#include <time.h>

void merge(int arr[], int left, int mid, int right) {
    int i, j, k;
    int n1 = mid - left + 1;
    int n2 = right - mid;
    
    int L[n1], R[n2];
    
    for (i = 0; i < n1; i++)
        L[i] = arr[left + i];
    for (j = 0; j < n2; j++)
        R[j] = arr[mid + 1 + j];
    
    i = 0;
    j = 0;
    k = left;
    
    while (i < n1 && j < n2) {
        if (L[i] <= R[j]) {
            arr[k] = L[i];
            i++;
        }
        else {
            arr[k] = R[j];
            j++;
        }
        k++;
    }
    
    while (i < n1) {
        arr[k] = L[i];
        i++;
        k++;
    }
    
    while (j < n2) {
        arr[k] = R[j];
        j++;
        k++;
    }
}

void mergeSort(int arr[], int left, int right) {
    if (left < right) {
        int mid = left + (right - left) / 2;
        mergeSort(arr, left, mid);
        mergeSort(arr, mid + 1, right);
        merge(arr, left, mid, right);
    }
}

int main() {
    int n;
    clock_t start, end;
    
    printf("Enter number of elements: ");
    scanf("%d", &n);
    
    int arr[n];
    
    printf("Enter %d elements: ", n);
    for(int i = 0; i < n; i++)
        scanf("%d", &arr[i]);
    
    printf("\nBefore Sorting: ");
    for(int i = 0; i < n; i++)
        printf("%d ", arr[i]);
    
    start = clock();
    mergeSort(arr, 0, n-1);
    end = clock();
    
    printf("\nAfter Sorting: ");
    for(int i = 0; i < n; i++)
        printf("%d ", arr[i]);
    
    double time_taken = ((double)(end - start)) / CLOCKS_PER_SEC;
    printf("\nExecution Time: %f seconds\n", time_taken);
    
    return 0;
}

```

### Experiment Analysis
- **Time Complexity**:
  - Best Case: O(n log n).
  - Average Case: O(n log n).
  - Worst Case: O(n²) - when array is already sorted or reverse sorted.
- **Space Complexity**: O(log n).

---

## Experiment 4: Graph Coloring with Backtracking

### Aim
Develop a program and measure the running time for Graph Coloring with Backtracking.

### Description
Graph coloring is a problem of assigning colors to vertices of a graph such that no two adjacent vertices have the same color. The program uses backtracking technique to find a valid coloring using minimum number of colors.

### Algorithm
1. Start with first vertex (vertex 0).
2. For current vertex, try colors from 1 to `m`:
   - Check if color is safe by verifying adjacent vertices.
   - If safe, assign color to current vertex.
   - Recursively color remaining vertices.
   - If coloring not possible, backtrack and try next color.
3. If all vertices are colored, solution is found.
4. If no valid coloring possible with `m` colors, return failure.

### Program
```c
#include <stdio.h>
#include <time.h>

#define V 4  // Number of vertices

// Check if color can be assigned
int isSafe(int graph[V][V], int color[], int vertex, int c) {
    for (int i = 0; i < V; i++) {
        if (graph[vertex][i] && c == color[i])
            return 0;
    }
    return 1;
}

// Recursive function for graph coloring
int graphColorUtil(int graph[V][V], int m, int color[], int vertex) {
    if (vertex == V)
        return 1;

    for (int c = 1; c <= m; c++) {
        if (isSafe(graph, color, vertex, c)) {
            color[vertex] = c;
            
            if (graphColorUtil(graph, m, color, vertex + 1))
                return 1;
                
            color[vertex] = 0;
        }
    }
    return 0;
}

// Main function for graph coloring
void graphColoring(int graph[V][V], int m) {
    int color[V] = {0};  // Initialize colors as 0
    clock_t start, end;
    
    printf("\nPossible coloring with %d colors:\n", m);
    
    start = clock();
    
    if (graphColorUtil(graph, m, color, 0)) {
        // Print the solution
        for (int i = 0; i < V; i++)
            printf("Vertex %d -> Color %d\n", i, color[i]);
    }
    else
        printf("Solution does not exist\n");
        
    end = clock();
    
    double time_taken = ((double)(end - start))/CLOCKS_PER_SEC;
    printf("\nExecution Time: %f seconds\n", time_taken);
}

int main() {
    // Example graph representation (adjacency matrix)
    int graph[V][V] = {
        {0, 1, 1, 1},
        {1, 0, 1, 0},
        {1, 1, 0, 1},
        {1, 0, 1, 0}
    };
    
    int m = 3;  // Number of colors
    
    printf("Graph Coloring using Backtracking\n");
    printf("Number of vertices: %d\n", V);
    printf("Maximum colors allowed: %d\n", m);
    
    graphColoring(graph, m);
    
    return 0;
}

```
### Sample Output:
Graph Coloring using Backtracking
- Number of vertices: 4
- Maximum colors allowed: 3

- Possible coloring with 3 colors:
Vertex 0 -> Color 1
Vertex 1 -> Color 2
Vertex 2 -> Color 3
Vertex 3 -> Color 2

- Execution Time: 0.000034 seconds

### Experiment Analysis
- **Time Complexity**: O(m^V), where `m` is the number of colors and `V` is the number of vertices.
- **Space Complexity**: O(V) for recursive call stack and color array.

---

## Experiment 5: Hamiltonian Cycle with Backtracking

### Aim
Develop a program and measure the running time to generate a solution for the Hamiltonian Cycle problem with Backtracking.

### Description
A Hamiltonian cycle is a path in a graph that visits each vertex exactly once and returns to the starting vertex. The program uses backtracking to find such a cycle if it exists.

### Algorithm
1. Start from vertex 0.
2. For current vertex, try connecting to unvisited adjacent vertices:
   - Mark current vertex as visited.
   - Recursively try to construct path from next vertex.
   - If path not possible, backtrack (unmark vertex).
3. If all vertices visited and path returns to start, cycle found.
4. If no valid path possible, return failure.

### Program
```c
#include <stdio.h>
#include <time.h>
#include <stdbool.h>

#define V 5  // Number of vertices

// Check if vertex v can be added at index 'pos' in the path
bool isSafe(int v, bool graph[V][V], int path[], int pos) {
    // Check if vertex is adjacent to previous vertex
    if (!graph[path[pos - 1]][v])
        return false;

    // Check if vertex is already included in path
    for (int i = 0; i < pos; i++)
        if (path[i] == v)
            return false;

    return true;
}

// Recursive function to find Hamiltonian cycle
bool hamCycleUtil(bool graph[V][V], int path[], int pos) {
    // Base case: if all vertices are included
    if (pos == V) {
        // Check if there is an edge from last vertex to first vertex
        if (graph[path[pos - 1]][path[0]])
            return true;
        return false;
    }

    // Try different vertices as next candidate
    for (int v = 1; v < V; v++) {
        if (isSafe(v, graph, path, pos)) {
            path[pos] = v;

            if (hamCycleUtil(graph, path, pos + 1))
                return true;

            // Backtrack
            path[pos] = -1;
        }
    }
    return false;
}

// Function to find Hamiltonian cycle
void hamCycle(bool graph[V][V]) {
    int *path = malloc(V * sizeof(int));
    clock_t start, end;
    
    // Initialize path array with -1
    for (int i = 0; i < V; i++)
        path[i] = -1;

    // Start from vertex 0
    path[0] = 0;

    printf("\nSearching for Hamiltonian Cycle...\n");
    
    start = clock();
    
    if (hamCycleUtil(graph, path, 1)) {
        printf("\nHamiltonian Cycle exists:\n");
        for (int i = 0; i < V; i++)
            printf("%d -> ", path[i]);
        printf("%d\n", path[0]);
    }
    else {
        printf("\nNo Hamiltonian Cycle exists\n");
    }
    
    end = clock();
    
    double time_taken = ((double)(end - start))/CLOCKS_PER_SEC;
    printf("\nExecution Time: %f seconds\n", time_taken);
    
    free(path);
}

int main() {
    // Example graph representation (adjacency matrix)
    bool graph[V][V] = {
        {0, 1, 0, 1, 0},
        {1, 0, 1, 1, 1},
        {0, 1, 0, 0, 1},
        {1, 1, 0, 0, 1},
        {0, 1, 1, 1, 0}
    };
    
    printf("Hamiltonian Cycle using Backtracking\n");
    printf("Number of vertices: %d\n", V);
    
    hamCycle(graph);
    
    return 0;
}

```
### Sample Output:
Hamiltonian Cycle using Backtracking
Number of vertices: 5

Searching for Hamiltonian Cycle...

Hamiltonian Cycle exists:
0 -> 1 -> 2 -> 4 -> 3 -> 0

Execution Time: 0.000042 seconds

### Experiment Analysis
- **Time Complexity**: O(n!), where `n` is the number of vertices.
- **Space Complexity**: O(n) for recursive call stack and path array.
