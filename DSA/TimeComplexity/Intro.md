# Algorithm & Time/Space Complexity

**Algorithm:** Series of steps that are to be taken to find a solution.
We take the help of time and space consumed by the algorithm to assess the performane. However, we dont go by exact numbers. Rather, there are mathematical models that helps in determining time and space complexity. The analysis which deals with those algorithms is called as asymptotic analysis. It helps in determining how time and space taken by algorithm
increases with input size.
Asymptotic analysis is done by asymptotic notations(Omega,Theta,Big O)
Asymptotic Notations are the mathematical tools used to describe the running time of an algorithm in terms of input size.
Asymptotic Notations help us in determining
- *Best Case:* Omega (2) Notation
  • It is the formal way to express the lower bound of an algorithm's running time. Lower bound means for any given input this notation determines best amount of time an algorithm
    can take to complete.
  • For example -
    If we say certain algorithm takes 100 secs as best amount of time. So, 100 secs will be lower bound of that algorithm. The algorithm can take more than 100 secs but it will not take less than 100 secs.

- *Average Case:* Theta(0) Notation
  
  It is the formal way to express both the upper and lower bound of an algorithm's running time. By Lower and Upper bound means for any given input this notation determines average
  amount of time an algorithm can take to complete.
  For example - If we run certain algorithm and it takes 100 secs for first run, 120 secs for second run, 110 for third run and so on. So, theta notations gives an average of running
  time of that algorithm.

- *Worst Case:* Big O(O) Notation
  
  • It is the formal way to express the upper bound of an algorithm's running time. Upper bound means for any given input this notation determines longest amount of time an algorithm can take to complete.
  • For example -
    If we say certain algorithm takes 100 secs as longest amount of time. So, 100 secs will be upper bound of that algorithm. The algorithm can take less than 100 secs but it will not take more than 100 secs.
    Rules of Big O(O) Notation:
  • It's a Single Processor
    It performs Sequential Execution of statements
  • Assignment operation takes 1 unit of time
  • Return statement takes in 1 unit of time
    Arithmetical operation takes 1 unit of time
  • Logical operation takes 1 unit of time
    Other small/single operations takes 1 unit of time
  • Drop lower order terms and constant multipliers
    T= n²+ 3n+1 ==> O(n²)

- Constant algorithm:
  
  <img width="978" alt="Screenshot 2024-04-23 at 10 28 42 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/dcf0d6c2-2b17-4089-b938-19a0b6757a92">

- Linear algorithm:
  i<=n: 3(n+1) (accessing n(1)+accessing i(1)+comparision operation(1))*comparision happens n number of time(n+1)
  
  ![image](https://github.com/Malobika8/GitDemo/assets/111234135/3666d0d8-15f7-459d-9716-de4bb0cdc0c7)


- Polynomial algorithm:
  
  ![image](https://github.com/Malobika8/GitDemo/assets/111234135/2fe37ee8-6a67-4335-b19d-c37d954e2446)


### Good to know info
1. Sum of n numbers: n(n+1)/2
   Better approach rather than looping and summing n number of times.
   
2. FYI:
   
   ![image](https://github.com/Malobika8/GitDemo/assets/111234135/71d19a61-82f9-40e5-b511-accb429205a8)


   
