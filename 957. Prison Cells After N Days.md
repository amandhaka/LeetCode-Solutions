There are 8 prison cells in a row, and each cell is either occupied or vacant.

Each day, whether the cell is occupied or vacant changes according to the following rules:

If a cell has two adjacent neighbors that are both occupied or both vacant, then the cell becomes occupied.
Otherwise, it becomes vacant.
(Note that because the prison is a row, the first and the last cells in the row can't have two adjacent neighbors.)

We describe the current state of the prison in the following way: cells[i] == 1 if the i-th cell is occupied, else cells[i] == 0.

Given the initial state of the prison, return the state of the prison after N days (and N such changes described above.)

 
```
Example 1:

Input: cells = [0,1,0,1,1,0,0,1], N = 7
Output: [0,0,1,1,0,0,0,0]
Explanation: 
The following table summarizes the state of the prison on each day:
Day 0: [0, 1, 0, 1, 1, 0, 0, 1]
Day 1: [0, 1, 1, 0, 0, 0, 0, 0]
Day 2: [0, 0, 0, 0, 1, 1, 1, 0]
Day 3: [0, 1, 1, 0, 0, 1, 0, 0]
Day 4: [0, 0, 0, 0, 0, 1, 0, 0]
Day 5: [0, 1, 1, 1, 0, 1, 0, 0]
Day 6: [0, 0, 1, 0, 1, 1, 0, 0]
Day 7: [0, 0, 1, 1, 0, 0, 0, 0]

Example 2:

Input: cells = [1,0,0,1,0,0,1,0], N = 1000000000
Output: [0,0,1,1,1,1,1,0]
```

Note:

cells.length == 8
cells[i] is in {0, 1}
1 <= N <= 10^9

```java
class Solution {
    public int[] prisonAfterNDays(int[] cells, int N) {
        Map<String,Integer> map=new HashMap<>();
        while(N>0){
            int[] nextCells= new int[cells.length];
            map.put(Arrays.toString(cells),N--);
            for(int i=1;i<7;i++){
                nextCells[i]=(cells[i-1]==cells[i+1])?1:0;
            }
            cells=nextCells;
            if(map.containsKey(Arrays.toString(cells))){
                //so we are starting out loop from N so whenver we ecnounter a state which has occured before than we find the size of loop and modolu it with remaining number of iteration which will reduce N to cycles length . Lets say our map has 120 with some array and now the same state has occured at N value equal to 110 so cycle is repeating after every 10 iterations so we divide 110/10 we have 0 . so this don't need any iteration now
                N=N%(map.get(Arrays.toString(cells))-N); 
            }
        }
        return cells;
    }
}
/*
Since you only have 6 bits that are changing (first and last bit changes to 0 and stays 0). Total max possible distinct states are 2 ^ 6 = 64.

Let's take an example. Assume you are asked the state after 10 ^ 9 days.
You store the state in the map the first time you see a new state. Then when you see the same state again, you know that you have passed (lastSeen - currVal) state in between. So now you know your states repeat every (lastSeen - currVal) times. So finally you can mod the current N with that value to not repeat the same steps. Below is an example for 10^9 days.
[0,1,0,1,1,0,0,1]
1000000000

N -> N % (last_seen - curr_val) ==> result
999999985 -> 999999985 % (999999999 - 999999985) ==> 5
4 -> 4 % (999999998 - 4) ==> 4
3 -> 3 % (999999997 - 3) ==> 3
2 -> 2 % (999999996 - 2) ==> 2
1 -> 1 % (999999995 - 1) ==> 1
0 -> 0 % (999999994 - 0) ==> 0

seen.get(Arrays.toString(cells)) is the last time when the same cells appear, seen.get(Arrays.toString(cells))-N is the cycle length. %= cuts down the loop times.


*/
```
