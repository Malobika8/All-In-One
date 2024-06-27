# Queue(FIFO)
   - Front(Deletion, Index 0)
   - Rear(Insertion, Index of last element)
     
### Operations:
   - Enqueue(Add)
   - Dequeue(Remove)
   - Peek(Front)
  
### Queue implementation using array: 

        import java.io.IOException;
        import java.util.Scanner;

        public class Main {
            public static void main(String[] args) throws IOException {
    
                Scanner sc = new Scanner(System.in);
                Queue queue = new Queue(5);
                int choice;
                int num;
                do{
                    System.out.println("Enter 1.Insert 2.Remove 3.Peak 4.DisplayItems");
                    choice = sc.nextInt();
                    switch(choice){
                        case 1:
                            System.out.println("Enter number:");
                            num = sc.nextInt();
                            queue.queue(num);
                            break;
                        case 2:
                            queue.dequeue();
                            break;
                        case 3:
                            queue.peek();
                            break;
                        case 4:
                            queue.display();
                            break;
                    }
                    System.out.println("Enter 0 to go to main menu.");
                    System.out.println("Press any key to exit.");
                    choice=sc.nextInt();
                }
                while(choice==0);
            }
        }

        public class Queue {
            int size;
            int queue[];
            int rear = -1;

            Queue(int size) {
                this.size = size;
                queue = new int[size];
            }

            public void queue(int num) {
                if (isFull()) {
                    System.out.println("Queue full.");
                }
                else {
                    rear++;
                    queue[rear] = num;
                }
            }

            public void dequeue() {
                if (isEmpty()) {
                    System.out.println("Empty queue.");
                }
                else {
                    int front = queue[0];
                    for (int i = 0; i < size-1; i++) {
                        queue[i] = queue[i + 1];
                    }
                    rear--;
                    System.out.println("Deleted " + front);
                }
            }

            public void peek() {
                if (isEmpty()) {
                    System.out.println("Empty queue");
                }
                else {
                    System.out.println(queue[0]);
                }
            }

            public void display() {
                if (isEmpty()) {
                    System.out.println("Empty queue");
                }
                else {
                    for(int index=0;index<=rear;index++)
                        System.out.println(queue[index]);
                }
            }

            boolean isEmpty() {
                if (rear == -1)
                    return true;
                else
                    return false;
            }

            boolean isFull() {
                if (rear == (size - 1))
                    return true;
                else
                    return false;
            }
        }
