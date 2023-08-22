# Heap
A heap is a specialized tree-based data structure that satisfies the heap property, which varies depending on whether it's a max-heap or a min-heap. The two main types of heaps are max-heaps and min-heaps:

# Max-Heap 
In a max-heap, the value of each parent node is greater than or equal to the values of its children nodes. This means that the largest element is at the root, and every subtree follows the same property.

# Min-Heap
In a min-heap, the value of each parent node is smaller than or equal to the values of its children nodes. This leads to the smallest element being at the root, and the same property holds for all subtrees.

Both types of heaps have applications in various algorithms, primarily because they provide efficient access to either the maximum or minimum element and also allow quick insertions and deletions while maintaining the heap property.

[Reference Link](https://www.programiz.com/dsa/heap-data-structure)

# MaxHeap Code
```cpp
#include<iostream>
#include <vector>
using namespace std;
#define pb push_back

void heapify(vector<int> &heapTree, int n, int i) {
    int largest = i;
    int left = 2 * i + 1, right = 2 * i + 2;
    if(left < n && heapTree[left] > heapTree[largest]) largest = left;
    if(right < n && heapTree[right] > heapTree[largest]) largest = right;
    if(largest != i) {
        swap(heapTree[i], heapTree[largest]);
        heapify(heapTree, n, largest);
    }
}

void insert(vector<int> &heapTree, int num) {
	int n = heapTree.size();
	if(n == 0) {
		heapTree.pb(num);
	} else {
		heapTree.pb(num);
		for(int i = (n / 2) - 1; i >= 0; i--) heapify(heapTree, n + 1, i);
	}
	
}

void deleteNode(vector<int> &heapTree, int num) {
	int n = heapTree.size(), i;
	while(i < n) {
		if(heapTree[i] == num) break;
		i++;
	}
	swap(heapTree[i], heapTree[n - 1]);
	heapTree.pop_back();
	n = heapTree.size();
	for(int i = n / 2 - 1; i >= 0; i--) heapify(heapTree, n, i);
}

int main() {
	int n, cur; cin >> n;
	vector<int> heapTree;
	for(int i = 0; i < n; i++) {
		cin >> cur;
		insert(heapTree, cur);
	} 
	for(int i = 0; i < heapTree.size(); i++) cout << heapTree[i] << " ";
	cout << endl;
	deleteNode(heapTree, 15);
	for(int i = 0; i < heapTree.size(); i++) cout << heapTree[i] << " ";
}
```
# MinHeap Code
```cpp
#include<iostream>
#include <vector>
using namespace std;
#define pb push_back

void heapify(vector<int> &heapTree, int n, int i) {
    int smallest = i;
    int left = 2 * i + 1, right = 2 * i + 2;
    if(left < n && heapTree[left] < heapTree[smallest]) smallest = left;
    if(right < n && heapTree[right] < heapTree[smallest]) smallest = right;
    if(smallest != i) {
        swap(heapTree[i], heapTree[smallest]);
        heapify(heapTree, n, smallest);
    }
}

void insert(vector<int> &heapTree, int num) {
	int n = heapTree.size();
	if(n == 0) {
		heapTree.pb(num);
	} else {
		heapTree.pb(num);
		for(int i = (n / 2) - 1; i >= 0; i--) heapify(heapTree, n + 1, i);
	}
}

void deleteNode(vector<int> &heapTree, int num) {
	int n = heapTree.size(), i = 0;
	while(i < n) {
		if(heapTree[i] == num) break;
		i++;
	}
	swap(heapTree[i], heapTree[n - 1]);
	heapTree.pop_back();
	n = heapTree.size();
	for(int i = n / 2 - 1; i >= 0; i--) heapify(heapTree, n, i);
}

int main() {
	int n, cur; cin >> n;
	vector<int> heapTree;
	for(int i = 0; i < n; i++) {
		cin >> cur;
		insert(heapTree, cur);
	} 
	for(int i = 0; i < heapTree.size(); i++) cout << heapTree[i] << " ";
	cout << endl;
	deleteNode(heapTree, 15);
	for(int i = 0; i < heapTree.size(); i++) cout << heapTree[i] << " ";
}
```

# Summary of Time Complexity

Insertion: Both insertion and deletion in heaps typically take O(log n) time complexity, where 'n' is the number of elements in the heap. This is because these operations involve traversing the height of the heap, which is logarithmic in the number of elements.

Finding Maximum/Minimum: Finding the maximum or minimum element in a heap (located at the root) takes constant time, O(1), as it's always accessible at the top of the heap.

Deletion of Maximum/Minimum: Deleting the maximum or minimum element and restructuring the heap afterward takes O(log n) time complexity. This involves replacing the root with the last element, "bubbling down" or "sifting down" the element to its correct position to restore the heap property.

Building a Heap: Constructing a heap from an array of elements takes O(n) time complexity using a method called "heapify," which involves starting from the last non-leaf node and performing the "sift down" operation to create a valid heap.

# Summary of Space Complexity

The space complexity of a heap is determined by the number of elements stored in the heap. In other words, it is O(n), where 'n' is the number of elements in the heap. The space is required to store the elements themselves and any additional data structures needed for heap operations.
