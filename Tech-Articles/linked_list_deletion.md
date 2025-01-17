=======================================================

Article Title: <linked_list_deletion>
Author Name: <Shivam Singh>
Author Profile: <https://github.com/Shivamgits>
Date: <08-10-2022>

=======================================================

Let us formulate the problem statement to understand the deletion process. Given a ‘key’, delete the first occurrence of this key in the linked list. 

Iterative Method:
To delete a node from the linked list, we need to do the following steps. 
1) Find the previous node of the node to be deleted. 
2) Change the next of the previous node. 
3) Free memory for the node to be deleted.
 

linkedlist_deletion

Recommended: Please solve it on “PRACTICE” first, before moving on to the solution.
 
Since every node of the linked list is dynamically allocated using malloc() in C, we need to call free() for freeing memory allocated for the node to be deleted.



// A complete working C++ program to
// demonstrate deletion in singly
// linked list with class
#include <bits/stdc++.h>
using namespace std;
 
// A linked list node
class Node{
public:
    int data;
    Node* next;
};
 
// Given a reference (pointer to pointer)
// to the head of a list and an int,
// inserts a new node on the front of the
// list.
void push(Node** head_ref, int new_data)
{
    Node* new_node = new Node();
    new_node->data = new_data;
    new_node->next = (*head_ref);
    (*head_ref) = new_node;
}
 
// Given a reference (pointer to pointer)
// to the head of a list and a key, deletes
// the first occurrence of key in linked list
void deleteNode(Node** head_ref, int key)
{
     
    // Store head node
    Node* temp = *head_ref;
    Node* prev = NULL;
     
    // If head node itself holds
    // the key to be deleted
    if (temp != NULL && temp->data == key)
    {
        *head_ref = temp->next; // Changed head
        delete temp;            // free old head
        return;
    }
 
    // Else Search for the key to be deleted,
    // keep track of the previous node as we
    // need to change 'prev->next' */
      else
    {
    while (temp != NULL && temp->data != key)
    {
        prev = temp;
        temp = temp->next;
    }
 
    // If key was not present in linked list
    if (temp == NULL)
        return;
 
    // Unlink the node from linked list
    prev->next = temp->next;
 
    // Free memory
    delete temp;
    }
}
 
// This function prints contents of
// linked list starting from the
// given node
void printList(Node* node)
{
    while (node != NULL)
    {
        cout << node->data << " ";
        node = node->next;
    }
}
 
// Driver code
int main()
{
     
    // Start with the empty list
    Node* head = NULL;
 
    // Add elements in linked list
    push(&head, 7);
    push(&head, 1);
    push(&head, 3);
    push(&head, 2);
 
    puts("Created Linked List: ");
    printList(head);
 
    deleteNode(&head, 1);
    puts("
Linked List after Deletion of 1: ");
     
    printList(head);
     
    return 0;
}
 
// This code is contributed by ac121102
Output:

Created Linked List: 
 2  3  1  7 
Linked List after Deletion of 1: 
 2  3  7
Time Complexity: O(n), where n represents the length of the given linked list.
Auxiliary Space: O(1), no extra space is required, so it is a constant.

Recursive Method:

To delete a node of a linked list recursively we need to do the following steps.

1.We pass node* (node pointer) as a reference to the function (as in node* &head)

2.Now since the current node pointer is derived from the previous node’s next (which is passed by reference) so now if the value of the current node pointer is changed, the previous next node’s value also gets changed which is the required operation while deleting a node (i.e points previous node’s next to current node’s (containing key) next).

3.Find the node containing the given value.

4.Store this node to deallocate it later using free() function.

5.Change this node pointer so that it points to its next and by performing this previous node’s next also get properly linked.

