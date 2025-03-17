# Pattern

## 1. Fixed window size: 

   - Construct the initial window by incrementing the j pointer until the window size k is reached. Once the window size is reached,      
     compute the sum, check if it’s the maximum, and then slide the window by incrementing both i and j.
   - Window size is given
   - ### Algo:
     - Reach the window size
     - Move the window by increasing i and j by 1
     - Pattern

       ```
         while(j<arr.length){
             calculations;

             if(j-i+1 < k){
                j++;
             }
             else if(j-i+1 == k){
                ans

                slide (i++, j++)
             }
          }
       ```
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
   - Pattern

       ```
         while(j<arr.length){
             calculations;

             if(count < k){
                j++;
             }
             else if(count == k){
                find max/min; //whatever is given
                j++;
             }
             else{
                calculations;
                slide;
             }
          }
       ```
       
   - Sample code:
     
      ```
       public int longestkSubstr(String s, int k) {
        Map<Character,Integer> map = new HashMap<>();
        int i=0;
        int j=0;
        int count=0;
        int max=-1;
        
        while(j<s.length()){
            if(map.containsKey(s.charAt(j))){
                map.put(s.charAt(j), map.get(s.charAt(j))+1);
            }
            else{
                map.put(s.charAt(j), 1);
                count++;
            }
            
            if(count < k){
                j++;
            }
            else if(count == k){
                max = Math.max(max, j-i+1);
                j++;
            }
            else{
                while(count>k){
                    map.put(s.charAt(i), map.get(s.charAt(i))-1);
                    if(map.get(s.charAt(i))==0){
                        map.remove(s.charAt(i));
                        count--;
                    }
                    i++;
                }
                j++;
            }
        }
        return max;
       }
    
      ```
