# DSA-Assignment-Stack-and-Queue
README.md
Data Structures & Algorithms
Practical Assignment Solution • GitHub Repository Upload
C++ Implementation
Q1. Array Implementation of Stack
Design and implement a stack using an array without built-in stack libraries. The program supports PUSH(x), POP(), PEEK(), and DISPLAY() while explicitly handling Stack Overflow and Underflow conditions.

#include <iostream>
using namespace std;

#define MAX_SIZE 5 // Fixed stack capacity

class Stack {
private:
    int arr[MAX_SIZE];
    int top;

public:
    Stack() { top = -1; }

    void push(int x) {
        if (top == MAX_SIZE - 1) {
            cout << "Stack Overflow! Cannot push " << x << endl;
            return;
        }
        arr[++top] = x;
        cout << x << " pushed into stack.\n";
    }

    void pop() {
        if (top == -1) {
            cout << "Stack Underflow! Stack is empty.\n";
            return;
        }
        cout << arr[top--] << " popped from stack.\n";
    }

    void peek() {
        if (top == -1) { cout << "Stack is empty.\n"; return; }
        cout << "Top element: " << arr[top] << endl;
    }

    void display() {
        if (top == -1) { cout << "Stack is empty.\n"; return; }
        cout << "Stack (Top to Bottom): ";
        for (int i = top; i >= 0; i--) cout << arr[i] << " ";
        cout << endl;
    }
};
Additional Task: Complexity & Capacity Analysis
1. Time & Space Complexity Analysis
Operation	Time Complexity	Space Complexity	Description
PUSH(x)	O(1)	O(1)	Direct array index access via top++.
POP()	O(1)	O(1)	Direct element removal via top--.
PEEK()	O(1)	O(1)	Reads arr[top] without modifying index.
DISPLAY()	O(N)	O(1)	Traverse from top down to index 0.
2. Fixed Stack Capacity Overflow Behavior
When the stack size is fixed (e.g., MAX_SIZE = 5) and a user attempts to insert an element beyond capacity:

Stack Overflow Condition: The index condition top == MAX_SIZE - 1 evaluates to true, triggering a boundary safeguard.
Memory Protection: Access is denied to prevent buffer overflow or memory corruption outside the array allocation.
DSA Assignment • Stack & Queue
Page 1 of 2
Q2. Array Implementation of Circular Queue
Implementation of a Circular Queue using an array. Supports ENQUEUE(x), DEQUEUE(), FRONT(), and DISPLAY() with modulo arithmetic to distinguish full vs empty states.

#include <iostream>
using namespace std;

#define SIZE 5 // Queue Capacity

class CircularQueue {
private:
    int items[SIZE], front, rear;
public:
    CircularQueue() { front = -1; rear = -1; }

    bool isFull() { return (front == (rear + 1) % SIZE); }
    bool isEmpty() { return (front == -1); }

    void enqueue(int x) {
        if (isFull()) { cout << "Queue Full! Cannot insert " << x << endl; return; }
        if (isEmpty()) front = 0;
        rear = (rear + 1) % SIZE;
        items[rear] = x;
        cout << x << " inserted.\n";
    }

    void dequeue() {
        if (isEmpty()) { cout << "Queue Empty!\n"; return; }
        cout << items[front] << " dequeued.\n";
        if (front == rear) { front = -1; rear = -1; } // Reset Queue
        else front = (front + 1) % SIZE;
    }

    void displayFront() {
        if (!isEmpty()) cout << "Front: " << items[front] << endl;
    }
};
Additional Task: Circular vs Linear Queue Analysis
1. Memory Utilization Comparison
In a standard linear queue, once REAR reaches the final array index SIZE - 1, no new elements can be added even if elements have been dequeued from the front. A Circular Queue connects the last position back to the first using (index + 1) % SIZE, reusing vacated memory slots efficiently.

2. Complexities & False Overflow Comparison
Parameter	Linear Queue	Circular Queue
ENQUEUE Time	O(1)	O(1)
DEQUEUE Time	O(1)	O(1)
Auxiliary Space	O(N)	O(N)
False Overflow Issue	Present: Occurs when REAR = SIZE - 1 while front slots are empty.	Resolved: Positions wrap around continuously to reuse freed memory slots.
DSA Assignment • Stack & Queue
