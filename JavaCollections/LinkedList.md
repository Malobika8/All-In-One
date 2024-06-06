# LinkedList
The LinkedList class is almost identical to the ArrayList.

### ArrayList vs. LinkedList
The LinkedList class is a collection which can contain many objects of the same type, just like the ArrayList. The LinkedList class has all of the same methods as the ArrayList class because they both implement the List interface. 
This means that you can add items, change items, remove items and clear the list in the same way. However, while the ArrayList class and the LinkedList class can be used in the same way, they are built very differently.

### How the ArrayList works
The ArrayList class has a regular array inside it. When an element is added, it is placed into the array. If the array is not big enough, a new, larger array is created to replace the old one and the old one is removed.

### How the LinkedList works
The LinkedList stores its items in "containers." The list has a link to the first container and each container has a link to the next container in the list. To add an element to the list, the element is placed into a new container and that container is linked to one of the other containers in the list.

### LinkedList Methods
For many cases, the ArrayList is more efficient as it is common to need access to random items in the list, but the LinkedList provides several methods to do certain operations more efficiently:
  - addFirst(): Adds an item to the beginning of the list
  -  addLast(): Add an item to the end of the list	
  - removeFirst(): Remove an item from the beginning of the list	
  - removeLast(): Remove an item from the end of the list	
  - getFirst(): Get the item at the beginning of the list	
  - getLast(): Get the item at the end of the list

# Implementations

### LinkedList implementation using Collection function
      
      // Import the LinkedList class
      import java.util.LinkedList;

      public class Main {
      public static void main(String[] args) {
        LinkedList<Integer> list = new LinkedList<Integer>();
        list.add(1);
        list.add(2);
        list.add(3);
        list.add(4);
        System.out.println(list);
      }
      }

### LinkedList implementation from scratch

      public class LL {
          Node head;
          int size;
          public class Node{
              int data;
              Node next;

              Node(int data){
                  this.data=data;
                  next=null;
                  size++;
              }
          }
      public void addFirst(int data){
        Node newNode = new Node(data);
        newNode.next=head;
        head=newNode;
      }
      public void addLast(int data){
        Node newNode= new Node(data);
        Node current=head;
        if(head==null){
            head=newNode;
            return;
        }
        while(current.next!=null){
            current=current.next;
        }
        current.next=newNode;
      }
      public void removeFirst(){
        if(head==null){
            System.out.println("Empty");
            return;
        }
        size--;
        if(head.next==null){
            head=null;
            return;
        }
        head=head.next;
      }
      public void removeLast(){
        Node currlast =head;
        if(head==null){
            System.out.println("Empty");
            return;
        }
        size--;
        if(head.next==null){
            head=null;
            return;
        }
        while(currlast.next.next!=null){
            currlast=currlast.next;
        }
        currlast.next=null;
      }
      public void print(){
        Node current=head;
        while(current!=null){
            System.out.print(current.data + "->");
            current=current.next;
        }
        System.out.println("null");
      }

      public int getSize(){
        return size;
      }

      public static void main(String args[]){
        LL ll = new LL();
        ll.addFirst(1);
        ll.addFirst(0);
        ll.print();

        ll.addLast(2);
        ll.addLast(3);
        ll.print();

        ll.removeFirst();
        ll.removeLast();
        ll.print();

        System.out.println("Size=" + ll.getSize());
      }
      }

  ### Reverse a linked link(Traditional approach)
  
     *Code Snippet*

      public void reverse(){
        if(head==null || head.next==null){
            System.out.println("Nothing to reverse..");
            return;
        }
        Node previous = head;
        Node current = head.next;

        while(current!=null){
            Node next = current.next;
            current.next=previous;
            previous=current;
            current=next;
        }
        head.next=null;
        head = previous;
      }

  ### Reverse using recursion (TODO)

     *Code Snippet*

      public Node reverseRecursive(Node head){
        if( head==null || head.next==null ){
            return head;
        }
        Node newHead = reverseRecursive(head.next);
        head.next.next = head;
        head.next=null;

        return newHead;
       }

  # Important questions
  1) Find and delete nth node from the end of the list.
  2) Check if it's palindrome.
  3) Check if its cyclic and make it non-cyclic.
