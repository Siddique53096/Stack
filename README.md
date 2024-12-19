# Stack

///////////////////// Node.h //////////////////////////


#include <iostream>
using namespace std;

class Node {
private:
    int data;
    Node* next;

public:
    Node() {
        data = 0;
        next = NULL;
    }
    Node(int value) {
        data = value;
        next = NULL;
    }
    void setData(int value) {
        data = value;
    }
    void setNext(Node* link) {
        next = link;
    }
    int getData() {
        return data;
    }
    Node* getNext() {
        return next;
    }
};




////////////////////////// Stack.h //////////////////////////////



#include "Node.h"

class Stack {
private:
    Node* top;

public:
    Stack();
    void push(int);
    void pop();
    bool isEmpty();
    int getTop();
    void print();
};






///////////////////////// implementatio.cpp ////////////////////////////




#include "Stack.h"
#include <iostream>
using namespace std;

Stack::Stack() {
    top = NULL; // Initialize the top pointer to NULL
}

bool Stack::isEmpty() {
    return (top == NULL);
}

void Stack::push(int value) {
    Node* temp = new Node(value);
    temp->setNext(top); // Link new node to the previous top
    top = temp;         // Update top to point to the new node
}

void Stack::pop() {
    if (isEmpty()) {
        cout << "Stack underflow! Cannot pop from an empty stack." << endl;
        return;
    }
    Node* temp = top;
    top = top->getNext(); // Move top to the next node
    delete temp;          // Delete the old top node
}

int Stack::getTop() {
    if (isEmpty()) {
        cout << "Stack is empty!" << endl;
        return -1; // Return an error value
    }
    return top->getData();
}

void Stack::print() {
    if (isEmpty()) {
        cout << "Stack is empty!" << endl;
        return;
    }
    Node* temp = top;
    while (temp != NULL) {
        cout << temp->getData() << endl;
        temp = temp->getNext();
    }
}




///////////////////////////// main.cpp //////////////////////



#include "Stack.h"
#include <iostream>
using namespace std;

void displayMenu() {
    cout << "\n----- Stack Operations -----\n";
    cout << "1. Push\n";
    cout << "2. Pop\n";
    cout << "3. Display Top Element\n";
    cout << "4. Display Stack\n";
    cout << "5. Exit\n";
    cout << "Enter your choice: ";
}

int main() {
    Stack S;
    int choice, value;

    do {
        displayMenu();
        cin >> choice;

        switch (choice) {
        case 1:
            cout << "Enter the value to push: ";
            cin >> value;
            S.push(value);
            cout << "Value " << value << " pushed onto the stack.\n";
            break;

        case 2:
            if (S.isEmpty()) {
                cout << "Stack is empty! Nothing to pop.\n";
            }
            else {
                cout << "Popping the top element...\n";
                S.pop();
            }
            break;

        case 3:
            if (S.isEmpty()) {
                cout << "Stack is empty! No top element.\n";
            }
            else {
                cout << "Top element: " << S.getTop() << endl;
            }
            break;

        case 4:
            cout << "Current stack:\n";
            S.print();
            break;

        case 5:
            cout << "Exiting program...\n";
            break;

        default:
            cout << "Invalid choice! Please try again.\n";
        }
    } while (choice != 5);

    return 0;
}
