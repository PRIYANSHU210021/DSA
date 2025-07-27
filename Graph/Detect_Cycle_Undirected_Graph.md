

## 🧠 **Version 1: DFS Approach**

### ✅ Purpose:

Detect a **cycle in an undirected graph** using **Depth-First Search (DFS)**.

### 🔍 Code:

```cpp
class Solution {
  public:
  
    // DFS helper function
    bool solve(int node, int parent, vector<int>& vis, vector<int> adj[]) {
        vis[node] = 1;  // Mark node as visited
        
        for (auto it : adj[node]) {
            if (!vis[it]) {
                if (solve(it, node, vis, adj))  // Recurse into neighbors
                    return true;  // Cycle found
            } 
            else if (parent != it) {
                return true;  // Cycle detected via back edge
            }
        }
        return false;  // No cycle from this path
    }
  
    // Main function to check for cycle
    bool isCycle(int V, vector<vector<int>>& edges) {
        vector<int> adj[V];         // Adjacency list
        vector<int> vis(V, 0);      // Visited array
        
        // Build adjacency list
        for (auto it : edges) {
            int u = it[0];
            int v = it[1];
            adj[u].push_back(v);
            adj[v].push_back(u);
        }
        
        // Check all components (disconnected graphs too)
        for (int i = 0; i < V; i++) {
            vector<int> vis(V);  // ❌ Issue: Re-declaring `vis` inside loop resets it every time
            if (solve(i, -1, vis, adj))
                return true;
        }
        
        return false;  // No cycle found
    }
};
```

### ⚠️ Issue:

* **`vector<int> vis(V)` inside the loop** reinitializes the visited array every time — defeats the purpose of checking already visited nodes.
* Fix: Declare `vis` **once** outside the loop, and reuse it.

---

## ✅ **Version 2: BFS Approach (Correct and Efficient)**

### 🔄 Uses Breadth-First Search (BFS) with a queue

### 🔍 Code:

```cpp
class Solution {
  public:
    bool isCycle(int V, vector<vector<int>>& edges) {
        vector<vector<int>> adj(V);  // Adjacency list
        vector<int> vis(V, 0);       // Visited array

        // Build the adjacency list from edge list
        for (auto it : edges) {
            int u = it[0];
            int v = it[1];
            adj[u].push_back(v);
            adj[v].push_back(u);  // Undirected graph
        }

        // Traverse all components
        for (int i = 0; i < V; i++) {
            if (!vis[i]) {
                queue<pair<int, int>> q;
                q.push({i, -1});   // Start BFS from node i, parent = -1
                vis[i] = 1;

                while (!q.empty()) {
                    int node = q.front().first;
                    int parent = q.front().second;
                    q.pop();

                    for (auto it : adj[node]) {
                        if (!vis[it]) {
                            vis[it] = 1;
                            q.push({it, node});
                        } 
                        else if (parent != it) {
                            return true;  // Cycle found
                        }
                    }
                }
            }
        }

        return false;  // No cycle found
    }
};
```

---

## 📝 Summary Notes:

| Feature                    | DFS Version                          | BFS Version                        |
| -------------------------- | ------------------------------------ | ---------------------------------- |
| Approach                   | Depth-First Search (Recursive)       | Breadth-First Search (Queue-based) |
| Cycle Check                | Back edge to non-parent node         | Same logic                         |
| Handles disconnected graph | ✅ Yes                                | ✅ Yes                              |
| Error in version?          | ❌ Yes (redeclared `vis` inside loop) | ✅ Correct                          |
| Efficiency                 | O(V + E)                             | O(V + E)                           |
| Space Complexity           | O(V) recursion stack + visited array | O(V) queue + visited array         |

---
