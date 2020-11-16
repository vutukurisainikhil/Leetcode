```cpp Question
A tree is an undirected graph in which any two vertices are connected by exactly one path. In other words, any connected graph without simple cycles is a tree.

Given a tree of n nodes labelled from 0 to n - 1, and an array of n - 1 edges where edges[i] = [ai, bi] indicates that there is an undirected edge between the two nodes ai and bi in the tree, you can choose any node of the tree as the root. When you select a node x as the root, the result tree has height h. Among all possible rooted trees, those with minimum height (i.e. min(h))  are called minimum height trees (MHTs).

Return a list of all MHTs' root labels. You can return the answer in any order.

The height of a rooted tree is the number of edges on the longest downward path between the root and a leaf.

 

Example 1:


Input: n = 4, edges = [[1,0],[1,2],[1,3]]
Output: [1]
Explanation: As shown, the height of the tree is 1 when the root is the node with label 1 which is the only MHT.
Example 2:


Input: n = 6, edges = [[3,0],[3,1],[3,2],[3,4],[5,4]]
Output: [3,4]
Example 3:

Input: n = 1, edges = []
Output: [0]
Example 4:

Input: n = 2, edges = [[0,1]]
Output: [0,1]
 

Constraints:

1 <= n <= 2 * 104
edges.length == n - 1
0 <= ai, bi < n
ai != bi
All the pairs (ai, bi) are distinct.
The given input is guaranteed to be a tree and there will be no repeated edges.
```
 
#**CPP CODE**
# Bruteforce Approach (timelimit exceeded
```cpp
class Solution {
public:
    int min_level=INT_MAX;
    vector<int> findMinHeightTrees(int n, vector<vector<int>>& edges) {
        ios_base::sync_with_stdio(false);
        cin.tie(NULL);
        if(n <= 1)
            return n == 0 ? vector<int>{} : vector<int>{0};
        vector<int> adj[n];
        for(int i=0;i<edges.size();i++){
            adj[edges[i][0]].push_back(edges[i][1]);
            adj[edges[i][1]].push_back(edges[i][0]); 
        }
        vector<int> v(n,-1);
        for(int i=0;i<n;i++){
            dfs(n, i, adj, v);
        }
        vector<int> res;
        for(int i=0;i<n;i++){
            if(v[i]==min_level){
                res.push_back(i);
            }
        }
        return res;
    }
    
    void dfs(int n, int key, vector<int> adj[], vector<int> &v){
        int max_level=0;
        priority_queue<pair<int,int>> pq;
        vector<bool> visited(n,false);
        pq.push(make_pair(key,0)); // pushing level=0, then adding +1 to it, to find total depth 
        while(!pq.empty()){
            pair<int,int> k = pq.top();
            int u = k.first;
            int level = k.second;
             // to find max of depth
            (level >= max_level)? max_level = level: max_level=max_level;
            pq.pop();
            visited[u] = true;
            for(int i=0;i<adj[u].size();i++){
                if(!visited[adj[u][i]] and i<n){
                    pq.push(make_pair(adj[u][i],level+1));
                }
            }
        }
        int check=1;
        for(int i=0;i<n;i++){
            if(!visited[i]){
                return;
                //check = 0;
            }
        }
        // adding max level in each iteration
        v[key]=max_level;
        if(min_level>max_level){
            min_level = max_level;
        }
        return;
    }
};
```
