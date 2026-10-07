# DSA-Assignment-Stack-and-Queue
README.md
Question 1: Stack Implementation Using Array
​Code Implementation (stack.cpp)
#include <iostream>
using namespace std;

#define MAX_SIZE 5 // Fixed capacity for the stack

class Stack {
private:
    int arr[MAX_SIZE];
    int top;

public:
    Stack() {
        top = -1; // Stack is initially empty
    }

    // Insert an element into the stack
    void push(int x) {
        if (top == MAX_SIZE - 1) {
            cout << "Stack Overflow! Cannot push " << x << ". Stack is full.\n";
            return;
        }
        arr[++top] = x;
        cout << x << " pushed into stack.\n";
    }

    // Remove the top element from the stack
    void pop() {
        if (top == -1) {
            cout << "Stack Underflow! Cannot pop. Stack is empty.\n";
            return;
        }
        cout << arr[top--] << " popped from stack.\n";
    }

    // View the top element without removing it
    void peek() {
        if (top == -1) {
            cout << "Stack is empty. No top element.\n";
            return;
        }
        cout << "Top element is: " << arr[top] << "\n";
    }

    // Display all elements in the stack
    void display() {
        if (top == -1) {
            cout << "Stack is empty.\n";
            return;
        }
        cout << "Stack elements (top to bottom): ";
        for (int i = top; i >= 0; i--) {
            cout << arr[i] << " ";
        }
        cout << "\n";
    }
};

int main() {
    Stack s;

    // Testing Stack Operations
    s.push(10);
    s.push(20);
    s.push(30);
    s.push(40);
    s.push(50);

    // Overflow Condition
    s.push(60);

    s.display();
    s.peek();

    s.pop();
    s.pop();

    s.display();

    // Emptying stack to test Underflow
    s.pop();
    s.pop();
    s.pop();
    s.pop(); // Underflow Condition

    return 0;
}
​Question 2: Circular Queue Implementation Using Array
​Code Implementation (circular_queue.cpp)
#include <iostream>
using namespace std;

#define SIZE 5 // Capacity of the circular queue

class CircularQueue {
private:
    int items[SIZE];
    int front, rear;

public:
    CircularQueue() {
        front = -1;
        rear = -1;
    }

    // Check if the queue is full
    bool isFull() {
        return (front == (rear + 1) % SIZE);
    }

    // Check if the queue is empty
    bool isEmpty() {
        return (front == -1);
    }

    // Insert an element into the circular queue
    void enqueue(int element) {
        if (isFull()) {
            cout << "Queue is Full! Cannot enqueue " << element << ".\n";
            return;
        }
        if (isEmpty()) {
            front = 0;
        }
        rear = (rear + 1) % SIZE;
        items[rear] = element;
        cout << element << " inserted successfully.\n";
    }

    // Remove an element from the circular queue
    void dequeue() {
        if (isEmpty()) {
            cout << "Queue is Empty! Cannot dequeue.\n";
            return;
        }
        cout << items[front] << " removed from queue.\n";
        
        if (front == rear) { // Queue has only one element, reset after removal
            front = -1;
            rear = -1;
        } else {
            front = (front + 1) % SIZE;
        }
    }

    // View front element
    void displayFront() {
        if (isEmpty()) {
            cout << "Queue is Empty.\n";
            return;
        }
        cout << "Front element is: " << items[front] << "\n";
    }

    // Display all elements in circular order
    void display() {
        if (isEmpty()) {
            cout << "Queue is Empty.\n";
            return;
        }
        cout << "Circular Queue elements: ";
        int i = front;
        while (true) {
            cout << items[i] << " ";
            if (i == rear) break;
            i = (i + 1) % SIZE;
        }
        cout << "\n";
    }
};

int main() {
    CircularQueue q;

    // Test Enqueue
    q.enqueue(10);
    q.enqueue(20);
    q.enqueue(30);
    q.enqueue(40);
    q.enqueue(50); // Queue full

    q.enqueue(60); // Full condition check

    q.display();
    q.displayFront();

    // Test Dequeue
    q.dequeue();
    q.dequeue();

    q.display();

    // Test Circular Enqueue in newly freed spaces
    q.enqueue(60);
    q.enqueue(70);

    q.display();

    return 0;
}
