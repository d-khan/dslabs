# Graphs

## Introduction

Many items in the world are connected, such as computers on a network connected by wires, cities connected by roads, or people connected by friendship.

A **graph** is a data structure for representing connections among items, and consists of vertices connected by edges.

- A **vertex** (or node) represents an item in a graph.
- An **edge** represents a connection between two vertices in a graph.

<img width="625" alt="image" src="https://user-images.githubusercontent.com/11669149/231191507-01a930c9-ff1d-4ded-9ad0-5ccb34522c8f.png">

1. Items in the world may have connections, like a computer network.
2. A graph's vertices represent items.
3. A graph's edges represent connections.
4. A graph can represent many different things, like friendships among people. Raj and Maya are friends, but Raj and Jen are not.

### Adjacency and paths

In a graph:

- Two vertices are **adjacent** if connected by an edge.
- A **path** is a sequence of edges leading from a source (starting) vertex to a destination (ending) vertex. The **path length** is the number of edges in the path.
- The **distance** between two vertices is the number of edges on the shortest path between those vertices.

<img width="637" alt="image" src="https://user-images.githubusercontent.com/11669149/231192056-e3422d47-82e1-4b06-8827-186250bec9d6.png">

1. Two vertices are adjacent if connected by an edge. PC1 and Server1 are adjacent. PC1 and Server3 are not adjacent.
2. A path is a sequence of edges from a source vertex to a destination vertex.
3. A path's length is the path's number of edges. Vertex distance is the shortest path length: Distance from PC1 to PC2 is 2.

### Graphs vs. Trees

You might have noticed that graphs look similar to trees, which we’ve dealt with in the past few chapters. Indeed, *trees are a type of graph.* Both data structures consist of nodes connected to each other.

So, what’s the difference between a graph and a tree?
 Here’s the deal: while all trees are graphs, not all graphs are trees.

Specifically, for a graph to be considered a tree, it cannot have *cycles,* and all nodes must be *connected.* Let’s see what that means.

A graph may have nodes that form what is known as a *cycle,* that is, nodes that reference each other circularly. In the example, Alice is friends with Diana, and Diana is connected to Bob, and Bob is connected...to Alice. These three nodes form a cycle.

Trees, on the other hand, are not “allowed” to have cycles. If a graph has a cycle, then it’s not a tree.

<img width="459" alt="image" src="https://user-images.githubusercontent.com/11669149/231199082-e6442358-6ee5-4d34-aad9-c85f753ff10c.png">

Another characteristic specific to trees is that every node is somehow connect- ed to every other node, even if the connections are indirect. However, it’s possible for a graph to not be fully connected.

See the following graph:

<img width="320" alt="image" src="https://user-images.githubusercontent.com/11669149/231199329-08f200ed-4003-45fb-9c40-ac6c2d4b4f06.png">

In this social network, we have two pairs of friends. However, no one from either pair are friends with anyone from the other pair. Additionally, we can see that Vicky has no friends yet, as perhaps she signed up for this social network just minutes ago. With trees, however, there’s never a node that’s disconnected from the rest of the tree.

## Applications of graph

### Geographic maps and navigation

Graphs are often used to represent a geographic map, which can contain information about places and travel routes. Ex: Vertices in a graph can represent airports, with edges representing available flights. Edge weights in such graphs often represent the length of a travel route, either in total distance or expected time taken to navigate the route. Ex: A map service with access to real-time traffic information can assign travel times to road segments.

<img width="705" alt="image" src="https://user-images.githubusercontent.com/11669149/231192913-2e360cb7-3a11-47b1-9529-de7de74b58c6.png">

1. A road map can be represented by a graph. Each intersection of roads is a vertex. Destinations like the beach or a house are also vertices.
2. Roads between vertices are edges. A map service with realtime traffic information can assign travel times as edge weights.
3. A shortest path finding algorithm can be used to find the shortest path starting at the house and ending at the beach.

### Product recommendations

A graph can be used to represent relationships between products. Vertices in the graph corresponding to a customer's purchased products have adjacent vertices representing products that can be recommended to the customer.

<img width="581" alt="image" src="https://user-images.githubusercontent.com/11669149/231194304-c357b5ae-782f-4d38-9dbf-4501fcd9951f.png">

1. An online shopping service can represent relationships between products being sold using a graph.
2. Relationships may be based on the products alone. A game console requires a TV and games, so the game console vertex connects to TV and game products.
3. Vertices representing common kitchen products, such as a blender, dishwashing soap, kitchen towels, and oven mitts, are also connected.
4. Connections also represent common purchases that occur by chance. Several customers who purchase a Blu-ray player also purchase a blender.
5. A customer's purchases can be linked to the product vertices in the graph.
6. Adjacent vertices can then be used to provide a list of recommendations to the customer.

### Social and professional networks

A graph may use a vertex to represent a person. An edge in such a graph represents a relationship between 2 people. In a graph representing a social network, an edge commonly represents friendship. In a graph representing a professional network, an edge commonly represents business conducted between 2 people.

<img width="493" alt="image" src="https://user-images.githubusercontent.com/11669149/231197130-aa3256ad-b0b9-4251-abb7-10343c9eeb11.png">

1. In a graph representing a professional network, vertices represent people and edges represent a business connection.
2. Tuyet conducts business with Wilford, adding a new edge in the graph. Similarly, Manuel conducts business with Keira.
3. The graph can help professionals find new connections. Shayla connects with Octavio through a mutual contact, Manuel.

## Graph representations: Adjacency lists

Various approaches exist for representing a graph data structure. A common approach is an adjacency list. Recall that two vertices are **adjacent** if connected by an edge. In an **adjacency list** graph representation, each vertex has a list of adjacent vertices, each list item representing an edge.

<img width="123" alt="image" src="https://user-images.githubusercontent.com/11669149/231197675-479c152d-2aeb-4cfe-a1e2-594af213d192.png">

| Vertices | Adjacent vertices (egdes) |
| -------- | ------------------------- |
| A        | B C                       |
| B        | A C D                     |
| C        | A B                       |
| D        | B                         |

1. Each vertex has a list of adjacent vertices for edges. The edge connecting A and B appears in A's list and also in B's list.
2. Each edge appears in the lists of the edge's two vertices.

### Advantages of adjacency lists

A key advantage of an adjacency list graph representation is a size of O(V + E), because each vertex appears once, and each edge appears twice. V refers to the number of vertices, E the number of edges.

However, a disadvantage is that determining whether two vertices are adjacent is O(V), because one vertex's adjacency list must be traversed looking for the other vertex, and that list could have V items. However, in most applications, a vertex is only adjacent to a small fraction of the other vertices, yielding a sparse graph. A **sparse graph** has far fewer edges than the maximum possible. Many graphs are sparse, like those representing a computer network, flights between cities, or friendships among people (every person isn't friends with every other person). Thus, the adjacency list graph representation is very common.

## Graph representations: Adjacency matrices

Various approaches exist for representing a graph data structure. One approach is an adjacency matrix. Recall that two vertices are **adjacent** if connected by an edge. In an **adjacency matrix** graph representation, each vertex is assigned to a matrix row and column, and a matrix element is 1 if the corresponding two vertices have an edge or is 0 otherwise.

<img width="386" alt="image" src="https://user-images.githubusercontent.com/11669149/231199987-89b4e8c7-be50-42bf-bf50-97deca30a924.png">

1. Each vertex is assigned to a row and column.
2. An edge connecting A and B is a 1 in A's row and B's column.
3. Similarly, that same edge is a 1 in B's row and A's column. (The matrix will thus be symmetric.)
4. Each edge similarly has two 1's in the matrix. Other matrix elements are 0's (not shown).

### Analysis of adjacency matrices

Assuming the common implementation as a two-dimensional array whose elements are accessible in $O(1)$, then an adjacency matrix's key benefit is $O(1)$ determination of whether two vertices are adjacent: The corresponding element is just checked for 0 or 1.

A key drawback is $O(N^2)$ size. Ex: A graph with 1000 vertices would require a 1000 x 1000 matrix, meaning 1,000,000 elements. An adjacency matrix's large size is inefficient for a sparse graph, in which most elements would be 0's.

An adjacency matrix only represents edges among vertices; if each vertex has data, like a person's name and address, then a separate list of vertices is needed.

## Breadth-first search

### Graph traversal and breadth-first search

An algorithm commonly must visit every vertex in a graph in some order, known as a **graph traversal**. A **breadth-first search** (BFS) is a traversal that visits a starting vertex, then all vertices of distance 1 from that vertex, then of distance 2, and so on, **without revisiting a vertex.**

<img width="561" alt="image" src="https://user-images.githubusercontent.com/11669149/231230121-5ebf25f3-6a91-40b0-b5bb-d56a1336575e.png">

1. Breadth-first search starting at A visits vertices based on distance from A. B and D are distance 1.
2. E and F are distance 2 from A. Note: A path of length 3 also exists to F, but **distance metric uses the shortest path**.
3. C is distance 3 from A. C is also distance 4 from A, but this is not the shortest path.
4. Breadth-first search from A visits A, then vertices of distance 1, then 2, then 3. Note: Visiting order of same-distance vertices doesn't matter.

> **Note:** Sometimes, I use the word 'hop' instead of distance. For example, D is one hop away from A, E is two hops away from B, and so on.

### **Example**: Social networking connection recommender

Social networking sites like Facebook and LinkedIn use graphs to represent connections among people. For a particular user, a site may wish to recommend new connections. One approach does a breadth-first search starting from the user, recommending new connections starting at distance 2 (distance 1 people are already connected with the user).

<img width="519" alt="image" src="https://user-images.githubusercontent.com/11669149/231232200-28bed542-0cf8-4480-b528-0308ac4300b5.png">

### Example: Find closest item in a peer-to-peer network

In a **peer-to-peer network**, computers are connected via a network and may seek and download file copies (such as songs or movies) via intermediary computers or routers. For example, one computer may seek the movie "The Wizard of Oz", which may exist on 10 computers in a network consisting of 100,000 computers. Finding the closest computer (having the fewest intermediaries) yields a faster download. A BFS traversal of the network graph can find the closest computer with that movie. The BFS traversal can be set to immediately return if the item sought is found during a vertex visit. Below, visiting vertex G finds the movie; BFS terminates, and a download process can begin, involving a path length of 2 (so only 1 intermediary). Vertex H also has the movie, but is further from B so wasn't visited yet during BFS. (Note: Distances of vertices visited during the BFS from B are shown below for convenience).

<img width="644" alt="image" src="https://user-images.githubusercontent.com/11669149/231232972-0fe2173d-93f1-48cc-a926-41a07fdc6f4d.png">

### Breadth-first search algorithm

An algorithm for breadth-first search enqueues the starting vertex in a queue. While the queue is not empty, the algorithm dequeues a vertex from the queue, visits the dequeued vertex, enqueues that vertex's adjacent vertices (if not already discovered), and repeats. [See BFS algorithm in action](https://youtu.be/WD49JkVEmVw).

```
BFS(startV) {
   Enqueue startV in frontierQueue
   Add startV to discoveredSet

   while ( frontierQueue is not empty ) {
      currentV = Dequeue from frontierQueue
      "Visit" currentV
      for each vertex adjV adjacent to currentV {
         if ( adjV is not in discoveredSet ) {
            Enqueue adjV in frontierQueue
            Add adjV to discoveredSet
         }
      }
   }
}
```

1. BFS enqueues the start vertex (in this case A) in frontierQueue, and adds A to discoveredSet.
2. Vertex A is dequeued from frontierQueue and visited.
3. Undiscovered vertices adjacent to A are enqueued in frontierQueue and added to discoveredSet.
4. Vertex A's visit is complete. The process continues on to next vertices in the frontierQueue, D and B.
5. E is visited. Vertices B and F are adjacent to E, but are already in discoveredSet. So B and F are not again added to frontierQueue or discoveredSet.
6. The process continues until frontierQueue is empty. discoveredSet shows the visit order. Note that each vertex's distance from start is shown on the graph.

When the BFS algorithm first encounters a vertex, that vertex is said to have been **discovered**. In the BFS algorithm, the vertices in the queue are called the **frontier**, being vertices thus far discovered but not yet visited. Because each vertex is visited at most once, an already-discovered vertex is not enqueued again.

A "visit" may mean to print the vertex, append the vertex to a list, compare vertex data to a value and return the vertex if found, etc.

## Depth-first search

### Graph traversal and depth-first search

An algorithm commonly must visit every vertex in a graph in some order, known as a **graph traversal**. A **depth-first search** (DFS) is a traversal that visits a starting vertex, then visits every vertex along each path starting from that vertex to the path's end before backtracking. [See DFS algorithm in action](https://youtu.be/nqgLaTt6ZE8).

### Depth-first search algorithm

```
DFS(startV) {
   Push startV to stack

   while ( stack is not empty ) {
      currentV = Pop stack
      if ( currentV is not in visitedSet ) {
         "Visit" currentV
         Add currentV to visitedSet
         for each vertex adjV adjacent to currentV
            Push adjV to stack
      }
   }
}
```

1. A depth-first search at vertex A first pushes vertex A onto the stack. The first loop iteration then pops vertex A off the stack and assigns currentV with that vertex.
2. Vertex A is visited and added to the visited set. Each vertex adjacent to A is pushed onto the stack.
3. Vertex B is popped off the stack and processed as the next currentV.
4. Vertices F and E are processed similarly.
5. Vertices F and B are in the visited set and are skipped after being popped off the stack.
6. Vertex C is popped off the stack and visited. All remaining vertices except D are in the visited set.
7. Vertex D is the last vertex visited.

## Directed graphs

A **directed graph**, or **digraph**, consists of vertices connected by directed edges. A **directed edge** is a connection between a starting vertex and a terminating vertex. In a directed graph, a vertex Y is **adjacent** to a vertex X, if there is an edge from X to Y.

Many graphs are directed, like those representing links between web pages, maps for navigation, or college course prerequisites.

<img width="599" alt="image" src="https://user-images.githubusercontent.com/11669149/231902240-b7d9325f-8561-4ed8-b937-c5787af1e939.png">



1. Items in the world may have directed connections, like links on a website.
2. directed graph's vertices represent items.
3. Vertices are connected by directed edges.
4. A directed edge represents a connection from a starting vertex to a terminating vertex; the terminating vertex is adjacent to the starting vertex. B is adjacent to A, but A is not adjacent to B.
5. A directed graph can represent many things, like airline connections between cities. A flight is available from Los Angeles to Tucson, but not Tucson to Los Angeles.

### Path and cycles

In a directed graph:

- A **path** is a sequence of directed edges leading from a source (starting) vertex to a destination (ending) vertex.
- A **cycle** is a path that starts and ends at the same vertex. A directed graph is **cyclic** if the graph contains a cycle, and **acyclic** if the graph does not contain a cycle.

<img width="504" alt="image" src="https://user-images.githubusercontent.com/11669149/231904856-b1e731b9-1323-42a9-ba66-f5e77d7b0695.png">

1. A path is a sequence of directed edges leading from a source (starting) vertex to a destination (ending) vertex.
2. A cycle is a path that starts and ends at the same vertex. A graph can have more than one cycle.
3. A cyclic graph contains a cycle. An acyclic graph contains no cycles.

### Example - Cycles in directed graphs: Kidney transplants

A patient needing a kidney transplant may have a family member willing to donate a kidney but is incompatible. That family member is willing to donate a kidney to someone else, as long as their family member also receives a kidney donation. Suppose Gregory needs a kidney. Gregory's wife, Eleanor, is willing to donate a kidney but is not compatible with Gregory. However, Eleanor is compatible with another patient Joanna, and Joanna's husband Darrell is compatible with Gregory. So, Eleanor donates a kidney to Joanna, and Darrell donates a kidney to Gregory, which is an example of a 2-way kidney transplant. In 2015, a 9-way kidney transplant involving 18 patients was performed within 36 hours (Source: [SF Gate](http://www.sfgate.com/health/article/9-way-kidney-swap-involving-18-surgeries-at-2-6307975.php)). Multiple-patient kidney transplants can be represented as cycles within a directed graph.

<img width="643" alt="image" src="https://user-images.githubusercontent.com/11669149/231905100-4d281911-cf98-4ead-b0da-cc489ba384b2.png">

In this graph, vertices represent patients, and edges represent compatibility between a patient's family member (shown in parentheses) and another patient. An N-way kidney transplant is represented as a cycle with N edges. Due to the complexity of coordinating multiple simultaneous surgeries, hospitals and doctors typically try to find the shortest possible cycle.

## Weighted graphs

A **weighted graph** associates a weight with each edge. A graph edge's **weight**, or **cost**, represents some numerical value between vertex items, such as flight cost between airports, connection speed between computers, or travel time between cities. A weighted graph may be directed or undirected.

<img width="299" alt="image" src="https://user-images.githubusercontent.com/11669149/231905486-22524ec6-ceda-407e-8b96-9ec9aab179e4.png">

Weighted graphs can be directed.  Ex: Edge weights may indicate travel time (hours) between cities; travel times may vary by direction. 

1. A weighted graph associates a numerical weight, or cost, with each edge. Ex: Edge weights may indicate connection speed (Mbps) between computers.
2. Weighted graphs can be directed. Ex: Edge weights may indicate travel time (hours) between cities; travel times may vary by direction.

### Path length in weighted graphs

In a weighted graph, the **path length** is the sum of the edge weights in the path.

<img width="562" alt="image" src="https://user-images.githubusercontent.com/11669149/231905672-d2cad29a-0218-4af4-b0ec-19413c75965f.png">

1. A path is a sequence of edges from a source vertex to a destination vertex.
2. The path length is the sum of the edge weights in the path.
3. The shortest path is the path yielding the lowest sum of edge weights. Ex: The shortest path from Paris to Marseille is 6.

### Negative edge weight cycles

The **cycle length** is the sum of the edge weights in a cycle. A **negative edge weight cycle** has a cycle length less than 0. A shortest path does not exist in a graph with a negative edge weight cycle, because each loop around the negative edge weight cycle further decreases the cycle length, so no minimum exists.

<img width="681" alt="image" src="https://user-images.githubusercontent.com/11669149/232980652-0c23b4a8-bacf-4631-bd15-70ca4a298a25.png">

## Dijkstra's shortest path

Finding the shortest path between vertices in a graph has many applications. Ex: Finding the shortest driving route between two intersections can be solved by finding the shortest path in a directed graph where vertices are intersections and edge weights are distances. If edge weights instead are expected travel times (possibly based on real-time traffic data), finding the shortest path will provide the fastest driving route.

Dijkstra's algorithm initializes all vertices' distances to infinity (∞), initializes all vertices' predecessors to null, and enqueues all vertices into a queue of unvisited vertices. The algorithm then assigns the start vertex's distance with 0. While the queue is not empty, the algorithm dequeues the vertex with the shortest distance. For each adjacent vertex, the algorithm computes the distance of the path from the start vertex to the current vertex and continuing on to the adjacent vertex. If that path's distance is shorter than the adjacent vertex's current distance, a shorter path has been found. The adjacent vertex's current distance is updated to the distance of the newly found shorter path's distance, and vertex's predecessor pointer is pointed to the current vertex. [See Dijkstra's shortest path algorithm in action](https://youtu.be/7MLD33ubQzE).

### Dijkstra's algorithm

```
DijkstraShortestPath(startV) {
   for each vertex currentV in graph {
      currentV⇢distance = Infinity
      currentV⇢predV = 0
      Enqueue currentV in unvisitedQueue
   }

   // startV has a distance of 0 from itself
   startV⇢distance = 0

   while (unvisitedQueue is not empty) {
      // Visit vertex with minimum distance from startV
      currentV = DequeueMin unvisitedQueue

      for each vertex adjV adjacent to currentV {
         edgeWeight = weight of edge from currentV to adjV
         alternativePathDistance = currentV⇢distance + edgeWeight
            
         // If shorter path from startV to adjV is found,
         // update adjV's distance and predecessor
         if (alternativePathDistance < adjV⇢distance) {
            adjV⇢distance = alternativePathDistance
            adjV⇢predV = currentV
         }
      }
   }
}
```

1. Each vertex is initialized with distance set to Infinity and the predecessor pointer set to null. Each vertex is enqueued into unvisitedQueue.
2. The start vertex's distance is 0. The algorithm visits the start vertex first.
3. For each adjacent vertex, if a shorter path from the start vertex to the adjacent vertex is found, the vertex's distance and predecessor pointer are updated.
4. B has the shortest path distance, and is dequeued from the queue. The path through B to C is not shorter, so no update occurs. The path through B to D is shorter, so D's distance and predecessor are updated.
5. D is then dequeued. The path through D to C is shorter, so C's distance and predecessor pointer are updated.
6. C is then dequeued. The path through C to D is not shorter, so no update occurs.
7. The algorithm terminates when all vertices are visited. Each vertex's distance is the shortest path distance from the start vertex. The vertex's predecessor pointer points to the previous vertex in the shortest path.

### Finding shortest path from start vertex to destination vertex

After running Dijkstra's algorithm, the shortest path from the start vertex to a destination vertex can be determined using the vertices' predecessor pointers. If the destination vertex's predecessor pointer is not 0, the shortest path is traversed in reverse by following the predecessor pointers until the start vertex is reached. If the destination vertex's predecessor pointer is null, then a path from the start vertex to the destination vertex does not exist.

<img width="405" alt="image" src="https://user-images.githubusercontent.com/11669149/232973246-69524340-5e6a-4a70-9163-c2bea9c164df.png">

1. The vertex's predecessor pointer points to the previous vertex in the shortest path.
2. Starting with the destination vertex, the predecessor pointer is followed until the start vertex is reached.
3. The vertex's distance is the shortest path distance from the start vertex.

### Algorithm efficiency

If the unvisited vertex queue is implemented using a list, the runtime for Dijkstra's shortest path algorithm is O(V2). The outer loop executes V times to visit all vertices. In each outer loop execution, dequeuing the vertex from the queue requires searching all vertices in the list, which has a runtime of O(V). For each vertex, the algorithm follows the subset of edges to adjacent vertices; following a total of E edges across all loop executions. Given E < V2, the runtime is O(V*V + E) = O(V2 + E) = O(V2). Implementing the unvisited vertex queue using a standard binary heap reduces the runtime to O((E + V) log V), and using a Fibonacci heap data structure (not discussed in this material) reduces the runtime to O(E + V log V).

> Dijkstra's shortest path algorithm can be used for unweighted graphs (using a uniform edge weight of 1) and weighted graphs with non-negative edges weights. For a directed graph with negative edge weights, Dijkstra's algorithm may not find the shortest path for some vertices, so the algorithm should not be used if a negative edge weight exists.

### Applications

1. Dijkstra’s algorithm is used as a routing protocol required by the routers to update their forwarding table.
2. It is used to find the shortest distance between two locations along the path on google maps.
3. It is used in telephone networking to find the shortest path for the nearest transmission switching station.
4. Dijkstra’s algorithm finds the shortest path between users measured through handshakes or connections among them.
5. Dijkstra’s algorithm minimizes the number of hops in computer networks.

### Dijkistra's algoritm implementation in C++

``` c++
#include <iostream>
using namespace std;

int miniDist(int distance[], bool Tset[]) // finding minimum distance
{
    int minimum=INT_MAX,ind;
              
    for(int k=0;k<6;k++) 
    {
        if(Tset[k]==false && distance[k]<=minimum)      
        {
            minimum=distance[k];
            ind=k;
        }
    }
    return ind;
}

void DijkstraAlgo(int graph[6][6],int src) // adjacency matrix 
{
    int distance[6]; // // array to calculate the minimum distance for each node                             
    bool Tset[6];// boolean array to mark visited and unvisited for each node
    
     
    for(int k = 0; k<6; k++)
    {
        distance[k] = INT_MAX;
        Tset[k] = false;    
    }
    
    distance[src] = 0;   // Source vertex distance is set 0               
    
    for(int k = 0; k<6; k++)                           
    {
        int m=miniDist(distance,Tset); 
        Tset[m]=true;
        for(int k = 0; k<6; k++)                  
        {
            // updating the distance of neighbouring vertex
            if(!Tset[k] && graph[m][k] && distance[m]!=INT_MAX && distance[m]+graph[m][k]<distance[k])
                distance[k]=distance[m]+graph[m][k];
        }
    }
    cout<<"Vertex\t\tDistance from source vertex"<<endl;
    for(int k = 0; k<6; k++)                      
    { 
        char str=65+k; 
        cout<<str<<"\t\t\t"<<distance[k]<<endl;
    }
}

int main()
{
    int graph[6][6]={
        {0, 1, 2, 0, 0, 0},
        {1, 0, 0, 5, 1, 0},
        {2, 0, 0, 2, 3, 0},
        {0, 5, 2, 0, 2, 2},
        {0, 1, 3, 2, 0, 1},
        {0, 0, 0, 2, 1, 0}};
    DijkstraAlgo(graph,0);
    return 0;                           
}
```

