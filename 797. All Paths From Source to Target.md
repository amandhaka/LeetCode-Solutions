Given a directed, acyclic graph of N nodes.  Find all possible paths from node 0 to node N-1, and return them in any order.

The graph is given as follows:  the nodes are 0, 1, ..., graph.length - 1.  graph[i] is a list of all nodes j for which the edge (i, j) exists.

Example:
```
Input: [[1,2], [3], [3], []] 
Output: [[0,1,3],[0,2,3]] 
Explanation: The graph looks like this:
0--->1
|    |
v    v
2--->3
There are two paths: 0 -> 1 -> 3 and 0 -> 2 -> 3.
```
Note:
```
The number of nodes in the graph will be in the range [2, 15].
You can print different paths in any order, but you should keep the order of nodes inside one path.
```
```java

class Solution {
    public List<List<Integer>> allPathsSourceTarget(int[][] graph) {
        ArrayList<Integer>[] g=new ArrayList[graph.length];
        for(int i=0;i<graph.length;i++){
            g[i]=new ArrayList<>();
            for(int j=0;j<graph[i].length;j++){
                g[i].add(graph[i][j]);
            }
        }
        List<List<Integer>> res= new ArrayList<>();
        dfs(res,g,0,graph.length-1,new ArrayList<>());
        return res;
    }
    private static void dfs(List<List<Integer>> res, ArrayList<Integer>[] g, int curr, int target,ArrayList<Integer> list){
        if(curr==target){
            list.add(curr);
            res.add(new ArrayList<>(list));
            list.remove(list.size()-1);
            return;
        }
        list.add(curr);
        for(int adj:g[curr]){
            dfs(res,g,adj,target,list);
        }
        list.remove(list.size()-1);
    }
}
```
