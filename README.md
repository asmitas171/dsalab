# dsalab
# 1  Stack
#include <iostream>
using namespace std;

#define SIZE 5   

class Stack {
    int arr[SIZE];
    int top;

public:
    Stack() { top = -1; }

    
    void push(int value) {
        if (top == SIZE - 1) {
            cout << "Stack Overflow! Cannot push " << value << endl;
        } else {
            top++;
            arr[top] = value;
            cout << value << " pushed into stack." << endl;
        }
    }

    
    void pop() {
        if (top == -1) {
            cout << "Stack Underflow! No elements to pop." << endl;
        } else {
            cout << arr[top] << " popped from stack." << endl;
            top--;
        }
    }

    
    void display() {
        if (top == -1) {
            cout << "Stack is empty." << endl;
        } else {
            cout << "Stack elements: ";
            for (int i = top; i >= 0; i--) {
                cout << arr[i] << " ";
            }
            cout << endl;
        }
    }
};

// Main function
int main() {
    Stack s;
    int choice, value;

    do {
        cout << "\n--- Stack Menu ---" << endl;
        cout << "1. Push\n2. Pop\n3. Display\n4. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
        case 1:
            cout << "Enter value to push: ";
            cin >> value;
            s.push(value);
            break;
        case 2:
            s.pop();
            break;
        case 3:
            s.display();
            break;
        case 4:
            cout << "Exiting..." << endl;
            break;
        default:
            cout << "Invalid choice!" << endl;
        }
    } while (choice != 4);

    return 0;
}

# 2 Binary Search
#include <iostream>
using namespace std;

int binarysearch(int arr[], int size, int target) {
    int low = 0;
    int high = size - 1;
    while (low <= high) {
        int mid = low + (high - low) / 2;  // ✅ fixed midpoint
        if (arr[mid] == target) {
            return mid;
        } else if (arr[mid] < target) {
            low = mid + 1;
        } else {
            high = mid - 1;
        }
    }
    return -1;
}

int main() {
    int sortedArray[] = {10, 20, 30, 40, 50, 60, 70, 80, 90, 100};
    int size = sizeof(sortedArray) / sizeof(sortedArray[0]);  
    int targetElement = 90;

    int result = binarysearch(sortedArray, size, targetElement);

    if (result != -1) {
        cout << "Element " << targetElement << " found at index: " << result << endl;
    } else {
        cout << "Element " << targetElement << " not found in the Array" << endl;
    }

    return 0;
}


# 3 Heap sort 
def heapify(arr, n, i):
    largest = i         
    left = 2 * i + 1     
    right = 2 * i + 2    

    
    if left < n and arr[left] > arr[largest]:
        largest = left

    
    if right < n and arr[right] > arr[largest]:
        largest = right

    
    if largest != i:
        arr[i], arr[largest] = arr[largest], arr[i]
        heapify(arr, n, largest)


def heap_sort(arr):
    n = len(arr)

    
    for i in range(n // 2 - 1, -1, -1):
        heapify(arr, n, i)

    
    for i in range(n - 1, 0, -1):
        arr[i], arr[0] = arr[0], arr[i]  
        heapify(arr, i, 0)               



arr = [50, 20, 40, 10, 60, 30]
print("Original array:", arr)

heap_sort(arr)
print("Sorted array:  ", arr)

# 4 Fraction Knapsack
class Item:
    def __init__(self, weight, value):
        self.weight = weight
        self.value = value
        self.ratio = value / weight


def fractional_knapsack(items, capacity):
    # Sort items by value/weight ratio in descending order
    items.sort(key=lambda x: x.ratio, reverse=True)

    total_value = 0.0

    for i in items:
        if capacity >= i.weight:
            
            capacity -= i.weight
            total_value += i.value
        else:
           
            fraction = capacity / i.weight
            total_value += i.value * fraction
            capacity = 0
            break  

    return total_value



items = [
    Item(10, 60),
    Item(20, 100),
    Item(30, 120)
]

capacity = 50
max_value = fractional_knapsack(items, capacity)

print("Maximum value in knapsack =", max_value)



