# Pattern

## 1. Fixed window size: 

   - Construct the initial window by incrementing the j pointer until the window size k is reached. Once the window size is reached,      
     compute the sum, check if it’s the maximum, and then slide the window by incrementing both i and j.
   - Window size is given
   - ### Algo:
     - Reach the window size
     - Move the window by increasing i and j by 1
     - Sample:
      
       ```
       public static List<Integer> FirstNegativeInteger(int arr[], int k) {
        List<Integer> list = new LinkedList<>();
        List<Integer> negative = new LinkedList<>();
        int i=0;
        int j=0;
        
        while(j<arr.length){
            if(arr[j]<0){
                negative.add(arr[j]);
            }
            if(j-i+1 < k){
                j++;
            }
            else if(j-i+1 == k){
                if(negative.isEmpty()){
                    list.add(0);
                }
                else{
                    list.add(negative.get(0));
                }
                if(!negative.isEmpty() && arr[i] == negative.get(0)){
                    negative.remove(0);
                }
                i++;
                j++;
            }
         }
        
         return list;
         }
     ```
     
## 3. Variable window size
   - Window is of variable length
   - Find max or min as given in the question
   - Sample code:
     
     
      ```
       while(j<s.length()){
            if(map.containsKey(s.charAt(j))){
                if(map.get(s.charAt(j)) > 0)
                    count--;
                map.put(s.charAt(j), map.get(s.charAt(j))-1);
            }
       
            if(count > 0){
                j++;
            }
            else if(count == 0){
                if(min > j-i+1){
                    min = j-i+1;
                    minString = s.substring(i,j+1);
                }
                while(count<=0){
                    if(map.containsKey(s.charAt(i))){
                        map.put(s.charAt(i), map.get(s.charAt(i))+1);
                        if(map.get(s.charAt(i)) > 0)
                            count++;
                    }
                    if(min > j-i+1){
                        min = j-i+1;
                        minString = s.substring(i,j+1);
                    }
                    i++;
                }

                if(i>j)
                    break;
                while(!map.containsKey(s.charAt(i)))
                    i++;
                j++;
            }
        }
       ```
