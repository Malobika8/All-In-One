# Backtracking

Used to find all possible solutions. It lies on top of recursion.
         
### Approach:

          func(){
             // Step1: Solution
                    if(solution){
                       print it
                    }
             // Step2: Choices
                    choice
                    func()
                    choice
                    func()
                }
         
*Note:*
1. If there's a blockage/no more options left, go back
2. If we are outside(valid)/found a solution, go back
3. Repeat above till we reach the entry

* **Calculate number of ways to exit maze.**
  
<img width="813" alt="Screenshot 2024-04-24 at 9 39 40 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/797a0f99-0be1-40f0-b3e3-7bed794fd5f3">

* **Given N print N digit number formed only by 1,2.**
  
<img width="833" alt="Screenshot 2024-04-24 at 9 40 23 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/e3555362-544d-4d83-9e6c-1672fbd5d659">
<img width="824" alt="Screenshot 2024-04-24 at 9 40 44 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/16c21fd6-2216-49d3-b55e-2ce3eb351529">
<img width="825" alt="Screenshot 2024-04-24 at 9 41 12 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/325b278b-22e7-4e11-aecd-f2d70538c956">
<img width="829" alt="Screenshot 2024-04-24 at 9 41 43 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/3f92b7d1-5ed0-4a37-aa8a-9ca4314ea653">

*Code:*

    public class PossibleCombination {
      public static void main(String[] args) {

        //Given N print N digit number formed only by 1,2
        int n=3;
        int arr[]=new int[n];
        possibleCombination(arr,n,0);
    }

    public static void possibleCombination(int arr[], int len, int index){
        if(index==len){
            for(int i=0;i<len;i++)
                System.out.print(arr[i]);

            System.out.println();
            return;
        }
        arr[index]=1;
        possibleCombination(arr,len,index+1);
        arr[index]=2;
        possibleCombination(arr,len,index+1);
     }
    }

* **NQueens problems**
  
<img width="840" alt="Screenshot 2024-04-24 at 9 42 41 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/e91b2410-acc8-43f1-afd0-1ca7421d91f7">
<img width="823" alt="Screenshot 2024-04-24 at 9 42 57 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/5c177172-c52d-41cf-b43d-0d13e2a83c76">
<img width="821" alt="Screenshot 2024-04-24 at 9 43 15 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/b89f23b9-ee7b-4727-94af-7813d93a5260">
<img width="821" alt="Screenshot 2024-04-24 at 9 43 37 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/584efe3c-b237-41e5-874a-4cc98d37de9b">
<img width="832" alt="Screenshot 2024-04-24 at 9 43 45 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/b42301bd-736b-4252-9bc9-fd935186c445">
<img width="829" alt="Screenshot 2024-04-24 at 9 44 12 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/c8e274f0-9d65-485b-8db7-972b6c0692af">
<img width="829" alt="Screenshot 2024-04-24 at 9 44 22 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/b5c06817-c7d2-4d96-9a6d-f710cd630d27">

Code for nQueens problem:
          
    public class Main {
      public static boolean valid(int mat[][], int i, int j){
      int r,c,N;
      N = mat.length;
      r = i;
      c = j;
      // validate column
      while(r>=0){
          if(mat[r][c] == 1){
              return false;
          }
          r--;
      }
      r = i;
      c = j;
      // validate left diagonal
      while((r>=0) && (c>=0)){
          if(mat[r][c] == 1){
              return false;
          }
          r--;
          c--;
      }
      r = i;
      c = j;
      // validate right diagonal
      while((r>=0) && (c<N)){
          if(mat[r][c] == 1){
              return false;
          }
          r--;
          c++;
      }
      return true;
    }
    public static void Nqueen(int mat[][], int i, int N){
      if(i==N){ // Blocked State
          for(int r=0;r<N;r++){
              for(int c=0;c<N;c++){
                  if(mat[r][c] == 1){
                      System.out.print("Q ");
                  }
                  else{
                      System.out.print("_ ");
                  }
              }
              System.out.println();
          }
          System.out.println();
          return; // BackTrack
      }
      // Make choices at ith row
      for(int j=0;j<N;j++){
          // Place cell at [i,j] --> Valid and check
          if(valid(mat,i,j)){
              mat[i][j] = 1; // Place queen
              Nqueen(mat,i+1,N);
              mat[i][j] = 0; // delete queen
          }
      }
      return;
    }
    public static void main(String[] args) {
      int N = 7;
      int mat[][] = new int[N][N];
      for(int i=0;i<N;i++){
        for(int j=0;j<N;j++){
          mat[i][j] = 0;
        }
      }
      Nqueen(mat,0,N);
     }
    }











