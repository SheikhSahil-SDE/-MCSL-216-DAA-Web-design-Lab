# Dijkstra's Algorithm
    Dijkstra's algorithm is a greedy algorithm used to find the shortest path from a single source 
    vertex to all other vertices in a weighted, directed graph with non-negative edge weights.

* Pseudocode:
  ```
  Algorithm Dijkstra(graph, src, V)
    Input: graph (V x V adjacency matrix where graph[i][j] is the weight of edge (i,j), ∞ if no edge), 
           src (source vertex), V (number of vertices)
    Output: distance[] (array of shortest distances from src)
    
    // Initialize
    distance[0 to V-1] = ∞
    distance[src] = 0
    visited[0 to V-1] = {false}    // Track visited vertices
    
    // Find shortest path for all vertices
    for count = 0 to V - 1 do
        // Find the unvisited vertex with minimum distance
        min = ∞
        u = -1
        for i = 0 to V - 1 do
            if visited[i] = false AND distance[i] < min then
                min = distance[i]
                u = i
            end if
        end for
        
        // Mark the selected vertex as visited
        if u ≠ -1 then
            visited[u] = true
            
            // Update distances to adjacent vertices
            for v = 0 to V - 1 do
                if visited[v] = false AND graph[u][v] ≠ ∞ AND 
                   distance[u] ≠ ∞ AND distance[u] + graph[u][v] < distance[v] then
                    distance[v] = distance[u] + graph[u][v]
                end if
            end for
        end if
    end for
    
    return distance
  ```
* Analysis
  
  - Best Case <br>
    Scenario: The graph is structured such that the shortest paths are found early<br>
    (e.g., a linear graph where the source is at one end).<br><br>
    Time Complexity: $ O(V^2) $.<br><br>
    Explanation: The algorithm iterates $ V $ times to select the minimum distance<br>
    vertex and checks all $ V $ vertices for updates, resulting in $ O(V^2) $ per iteration.<br>
    The best case still requires checking all unvisited vertices.<br><br>

  - Worst Case<br>
    Scenario: The graph is complete (all $ V(V-1)/2 $ edges), requiring updates<br>
    through all vertices.<br><br>
    Time Complexity: $ O(V^2) $.<br><br>
    Explanation: The outer loop runs $ V $ times, and the inner loop to find the minimum<br>
    and update distances takes $ O(V) $ per iteration, leading to $ O(V^2) $ total.<br>
    This is with an adjacency matrix; using a priority queue with an adjacency list can improve<br>
    it to $ O((V + E) \log V) $.<br>

* Additional Notes
  
      Space Complexity: $ O(V) $ for the distance and visited arrays.
      Assumption: All edge weights are non-negative. Negative weights invalidate the algorithm.
      Optimization: With a min-heap, complexity can be reduced to $ O((V + E) \log V) $,
      where $ E $ is the number of edges.
        
# Prim's Algorithm
        Prim's algorithm is a greedy algorithm used to find the Minimum Spanning Tree (MST) of a connected,
        undirected, weighted graph. It starts from an arbitrary vertex and grows the MST by adding the minimum-weight 
        edge that connects a new vertex to the existing tree, ensuring no cycles are formed.


*Pseudocode:
```
Algorithm Prim(graph, V)
    Input: graph (V x V adjacency matrix where graph[i][j] is the weight of edge (i,j), ∞ if no edge), V (number of vertices)
    Output: MST (set of edges forming the Minimum Spanning Tree)
    
    // Initialize
    minCost = 0
    visited[0 to V-1] = {false}    // Track visited vertices
    visited[0] = true             // Start from vertex 0
    edgeCount = 0                  // Count of edges in MST
    MST = empty set               // Store MST edges
    
    // Continue until V-1 edges are added (MST has V-1 edges)
    while edgeCount < V - 1 do
        min = ∞
        a = -1
        b = -1
        
        // Find the minimum weight edge from visited to unvisited
        for i = 0 to V - 1 do
            if visited[i] = true then
                for j = 0 to V - 1 do
                    if visited[j] = false AND graph[i][j] ≠ ∞ AND graph[i][j] < min then
                        min = graph[i][j]
                        a = i
                        b = j
                    end if
                end for
            end if
        end for
        
        // Add the edge to MST
        if a ≠ -1 AND b ≠ -1 then
            visited[b] = true
            MST = MST ∪ {(a, b)}
            minCost = minCost + min
            edgeCount = edgeCount + 1
        end if
    end while
    
    return MST, minCost
```

* Analysis

    - Best Case<br>
        Scenario: The graph is already structured such that the minimum edges are found early (e.g.,<br>
        a star graph with the center as the starting vertex).<br><br>
        Time Complexity: $ O(V^2) $.<br><br>
        Explanation: The algorithm uses two nested loops over $ V $ vertices to find the minimum edge, resulting in $ O(V^2)<br>
      $ operations per iteration. With $ V-1 $ iterations, the total is $ O(V^2) $. The best case still requires checking all unvisited vertices.<br><br>
        
    - Worst Case<br>
    Scenario: The graph is complete (all $ V(V-1)/2 $ edges), requiring exhaustive checks.<br><br>
    Time Complexity: $ O(V^2) $.<br><br>
    Explanation: The outer loop runs $ V-1 $ times, and the inner loops scan all $ V $ vertices to find the minimum edge,
leading to $ O(V^2) $ per iteration. Total complexity remains $ O(V^2) $ with an adjacency matrix representation.<br><br>

* Additional Notes
  
        Space Complexity: $ O(V) $ for the visited array.
        Optimization: Using a priority queue (e.g., min-heap) with an adjacency list can reduce complexity to $ O(E \log V)
        $ where $ E $ is the number of edges, but the basic version uses $ O(V^2) $.
        Assumption: The graph is connected and has no negative weights (though the algorithm works with non-negative weights).

