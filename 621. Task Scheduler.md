You are given a char array representing tasks CPU need to do. It contains capital letters A to Z where each letter represents a different task. Tasks could be done without the original order of the array. Each task is done in one unit of time. For each unit of time, the CPU could complete either one task or just be idle.

However, there is a non-negative integer n that represents the cooldown period between two same tasks (the same letter in the array), that is that there must be at least n units of time between any two same tasks.

You need to return the least number of units of times that the CPU will take to finish all the given tasks.

Example 1:
```
Input: tasks = ["A","A","A","B","B","B"], n = 2
Output: 8
Explanation: 
A -> B -> idle -> A -> B -> idle -> A -> B
There is at least 2 units of time between any two same tasks.
```
Example 2:
```
Input: tasks = ["A","A","A","B","B","B"], n = 0
Output: 6
Explanation: On this case any permutation of size 6 would work since n = 0.
["A","A","A","B","B","B"]
["A","B","A","B","A","B"]
["B","B","B","A","A","A"]
...
And so on.
```
Example 3:
```
Input: tasks = ["A","A","A","A","A","A","B","C","D","E","F","G"], n = 2
Output: 16
Explanation: 
One possible solution is
A -> B -> C -> A -> D -> E -> A -> F -> G -> A -> idle -> idle -> A -> idle -> idle -> A
```

Constraints:
```
The number of tasks is in the range [1, 10000].
The integer n is in the range [0, 100].
```
```java

class Solution {
    public int leastInterval(char[] tasks, int n) {
        Map<Character,Integer> map=new HashMap<>();
        for(char ch:tasks) map.put(ch,map.getOrDefault(ch,0)+1);
        
        PriorityQueue<Integer> pq=new PriorityQueue<>((a,b)->b-a);
        pq.addAll(map.values());
        int time=0;
        while(!pq.isEmpty()){
            List<Integer> list=new ArrayList<>();
            // Reason for n+1 is we are running tasks until cooldown period . lets say we have A A B B C C and n=2 
            // so we running A B C in first iteration and we will increase 3 in cycle also and lets say if we had
            // A A A B B B so now we can only run A B and then we will have to stay idle for 1 unit of time so that will be added
            // with n+1
            //Basically Baat ye hai hmko total idle leke chlana. Ki sbhi idle hai . lets say n=2 so _ _ _ so After one process I 
            // will have to wait for 2 unit time But I have different process like A A B B C C So i put A B C in all those blanks
            // and add 3 to my total time and lets say  I have A A A then I can only will A  _ _ and rest two will remain idle and 
            // that will also add 3 to total time unit;
            for(int i=0;i<n+1;i++){
                if(!pq.isEmpty()) list.add(pq.remove());
            }
            for(int i:list){
                if(--i>0){
                    pq.add(i);
                }
            }
            time+=pq.isEmpty()?list.size():n+1;
        }
        return time;
    }
}

```
