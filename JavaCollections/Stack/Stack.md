# Stack:
   
   i) Stack using array:
   - Underflow condition (Empty stack - Top with -1 value represents no data in the stack)
   - Overflow condittion (Stack is full)
   - Push (Insertion of an element)
   - Pop (Deletion of an element)
   - Display

         import java.io.IOException;
         import java.util.Scanner;

         public class StackDemoUsingArray {
           public static void main(String[] args) throws IOException {
             //Stack using array
             Scanner sc = new Scanner(System.in);
             Stack stack = new Stack();
             int choice;
             do{
                 System.out.println("Enter 1.Push 2.Pop 3.DisplayItems");
                 choice = sc.nextInt();
                 switch(choice){
                     case 1:
                         stack.push();
                         break;
                     case 2:
                         stack.pop();
                         break;
                     case 3:
                         stack.display();
                         break;
                 }
                 System.out.println("Enter 0 to go back to main menu.");
                 System.out.println("Enter any key to exit.");
                 choice = sc.nextInt();
             }
             while(choice==0);
           }
         }

         public class Stack{
           int size=5;
           int top=-1;
           int stack[]=new int[size];
           void push(){
               if(top==4){
                   System.out.println("Stack overflow!");
               }
               else{
                   Scanner sc = new Scanner(System.in);
                   System.out.println("Enter data:");
                   int num = sc.nextInt();
                   top++;
                   stack[top]=num;
                   System.out.println("Item inserted.");
               }
           }
           void pop(){
               if(top==-1){
                   System.out.println("Stack underflow!");
               }
               else {
                   top--;
                   System.out.println("Item deleted.");
               }
           }
           void display(){
               if(top==-1){
                   System.out.println("Stack empty!");
               }
               else{
                   System.out.println("Items are:");
                   for(int index=top;index>=0;index--){
                       System.out.println(stack[index]);
                   }
                 }
              }
           }
     
     ii)Using stack class(Java collection function):

            import java.io.IOException;
            import java.util.Scanner;
            import java.util.Stack;

            public class StackDemoUsingStackClass {
                public static void main(String[] args) throws IOException {

                    Stack<Integer> stack = new Stack<>();
                    Scanner sc = new Scanner(System.in);
                    int choice;
                    int num;
                    do{
                        System.out.println("Enter 1.Push 2.Pop 3.SearchItem 4.DisplayItems");
                        choice = sc.nextInt();
                        switch(choice){
                            case 1:
                                System.out.println("Enter data:");
                                num = sc.nextInt();
                                stack.push(num);
                                break;
                            case 2:
                                if(stack.empty())
                                  System.out.println("No data to delete");
                                else
                                  stack.pop();
                                break;
                            case 3:
                                System.out.println("Enter data:");
                                num  = sc.nextInt();
                                int position = stack.search(num);
                                if(position==-1)
                                    System.out.println("Data not found!");
                                else
                                    System.out.println("Data found!");
                                break;
                            case 4:
                                if(stack.empty())
                                    System.out.println("Stack empty");
                                else
                                    System.out.println("Items are:" + stack);
                        }
                        System.out.println("Enter 0 to go back to main menu");
                        System.out.println("Enter any key to exit.");
                        choice = sc.nextInt();
                    }
                    while(choice==0);
               }
             }
     iii) Using Linked List(Insert-O(1), Search-O(n))- Non contiguous memory

         public class StackUsingLL {
          private static class Node{
              int data;
              Node next;

              Node(int data){
                  this.data=data;
                  this.next=null;
              }
          }

          static class StackLL{
              static Node head=null;
              public void push(int data){
                  Node newNode=new Node(data);
                  newNode.next=head;
                  head=newNode;
              }
              public void peek(){
                  if(head==null){
                      System.out.println("Empty");
                      return;
                  }
                  System.out.println(head.data);
              }
              public void pop(){
                  if(head==null){
                      System.out.println("Empty");
                      return;
                  }
                  System.out.println(head.data);
                  head=head.next;
              }
          }
          public static void main(String args[]){
              StackLL stackLL=new StackLL();
              stackLL.push(1);
              stackLL.push(2);
              stackLL.push(3);
              System.out.println("Pushed 1,2,3");
              System.out.print("Peek: ");
              stackLL.peek();

              System.out.print("Pop: " );
              stackLL.pop();
              System.out.print("Peek: ");
              stackLL.peek();

              System.out.print("Pop: ");
              stackLL.pop();
              System.out.print("Peek: ");
              stackLL.peek();

              System.out.print("Pop: ");
              stackLL.pop();
              System.out.print("Peek: ");
              stackLL.peek();
             }
            }

iv) Using ArrayList(Insert-O(n), Search-O(1))- Contiguous memory

      import java.util.ArrayList;

      public class StackUsingAL {
          static class StackAL{
              ArrayList<Integer> arrayList=new ArrayList<>();

        public void push(int data){
            arrayList.add(data);
        }
        public void peek(){
            if(arrayList.size()==0){
                System.out.println("Empty");
                return;
            }
            System.out.println("Peak: " + arrayList.get(arrayList.size()-1));
        }
        public void pop(){
            if(arrayList.size()==0){
                System.out.println("Empty");
                return;
            }
            System.out.println("Pop: " + arrayList.remove(arrayList.size()-1));

        }
    }
    public static void main(String args[]){
        StackAL stackAL=new StackAL();
        stackAL.push(1);
        stackAL.push(2);
        stackAL.push(3);
        System.out.println("Pushed: 1,2,3");
        stackAL.peek();

        stackAL.pop();
        stackAL.peek();

        stackAL.pop();
        stackAL.peek();

        stackAL.pop();
        stackAL.peek();
    }}

### PROBLEM 1: TO PUSH AN ELEMENT AT THE BOTTOM OF THE STACK

      import java.util.Stack;

      //to push an element at the bottom of the stack
      public class StackProblem1 {
    public void pushAtBottom(Stack<Integer> stack, int data){
        if(stack.isEmpty()){
            stack.push(data);
            return;
        }
        int temp=stack.pop();
        pushAtBottom(stack,data);
        stack.push(temp);
    }
    public static void main(String args[]){
        Stack<Integer> stack = new Stack<>();
        stack.push(1);
        stack.push(2);
        stack.push(3);
        StackProblem1 stackProblem1=new StackProblem1();
        stackProblem1.pushAtBottom(stack,4);

        while(!stack.isEmpty()){
            System.out.println(stack.pop());
        }
       }
      }
    
### PROBLEM 2: TO REVERSE A STACK

      import java.util.Stack;

      //To reverse a stack
      public class StackProblem2 {
    public void reverse(Stack<Integer> stack){
        if(stack.isEmpty()){
            return;
        }
        int top=stack.pop();
        reverse(stack);
        pushAtBottom(stack,top);
    }
    public void pushAtBottom(Stack<Integer> stack, int data){
        if(stack.isEmpty()){
            stack.push(data);
            return;
        }
        int temp=stack.pop();
        pushAtBottom(stack,data);
        stack.push(temp);
    }
    public static void main(String args[]){
        Stack<Integer> stack = new Stack<>();
        stack.push(1);
        stack.push(2);
        stack.push(3);
        StackProblem2 stackProblem2=new StackProblem2();
        stackProblem2.reverse(stack);

        while(!stack.isEmpty()){
            System.out.println(stack.pop());
        }
       }
      }

   


              



  
