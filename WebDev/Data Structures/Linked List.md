
### What is a Linked List?

A linked list is a linear data structure similar to an array. However, unlike arrays, elements are not store in a particular memory location or index. Rather each element is a separate object that contains a pointer or a link to the next object in that list. 

Each element is commonly referred to as a **node**. A node contains two items:
1. The data stored
2. A link to the next node
![[Pasted image 20240128103553.png]]

The entry point to a linked list is called the head. The head is a reference to the first node in the linked list. The last node on the list point to `null`. If a list is empty, the head is a null reference.

In JavaScript, a linked list looks like this:
![[Pasted image 20240128103708.png]]


### Advantages

- Nodes can easily be removed or added from a linked list without reorganizing the entire data structure. This is one advantage that it has over arrays.

### Disadvantages

- Search operations are slow in linked lists. Unlike arrays, random access of data elements is not allowed. Nodes are accessed sequentially starting from the first node.
- It uses more memory than arrays because of the storage of the pointers.

### Types of Linked Lists

There are three types of linked lists:

#### Singly Linked Lists
Each node contains only one pointer to the next node.

#### Doubly Linked Lists
Each node contains two pointers, a pointer to the next node and a pointer to the previous node.

#### Circular Linked Lists
Circular linked lists are a variation of a linked list in which the last node points to the first node or any other node before it, thereby forming a loop.


### Implementing a Linked List

#### Implementing a List Node in JavaScript
We can implement a list node in JavaScript as follows:

![[Pasted image 20240128104625.png]]

As stated previously, a list node contains two items:
1. The data
2. The pointer to the next node

#### Implementing a Linked List in JavaScript
We can implement a linked list class with a constructor. Notice that if the head node is not passed, the head is initialized to null.

![[Pasted image 20240128104948.png]]

#### Putting them together
Let's create a linked list with the class we just created. First, we'll create two list nodes, `node1` and `node2` and a pointer from `node1` to `node2`.

![[Pasted image 20240128105059.png]]

![[Pasted image 20240128105206.png]]


### Linked List methods

#### size()
This method returns the number of nodes present in the linked list.
![[Pasted image 20240128105256.png]]

#### clear()
This method empties out the list.
![[Pasted image 20240128105319.png]]

#### getLast()
This method returns the last node of the linked list.
![[Pasted image 20240128105347.png]]

#### getFirst()
This method returns the first node of the linked list.
![[Pasted image 20240128105414.png]]


