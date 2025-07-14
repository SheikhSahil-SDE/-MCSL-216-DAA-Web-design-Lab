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
  
      - Best Case
  
        Scenario: The graph is structured such that the shortest paths are found early
        (e.g., a linear graph where the source is at one end).
        Time Complexity: $ O(V^2) $.
        Explanation: The algorithm iterates $ V $ times to select the minimum distance
        vertex and checks all $ V $ vertices for updates, resulting in $ O(V^2) $ per iteration.
        The best case still requires checking all unvisited vertices.

      - Worst Case

        Scenario: The graph is complete (all $ V(V-1)/2 $ edges), requiring updates
        through all vertices.
        Time Complexity: $ O(V^2) $.
        Explanation: The outer loop runs $ V $ times, and the inner loop to find the minimum
        and update distances takes $ O(V) $ per iteration, leading to $ O(V^2) $ total.
        This is with an adjacency matrix; using a priority queue with an adjacency list can improve
        it to $ O((V + E) \log V) $.

* Additional Notes
  
      Space Complexity: $ O(V) $ for the distance and visited arrays.
      Assumption: All edge weights are non-negative. Negative weights invalidate the algorithm.
      Optimization: With a min-heap, complexity can be reduced to $ O((V + E) \log V) $,
      where $ E $ is the number of edges.
        
