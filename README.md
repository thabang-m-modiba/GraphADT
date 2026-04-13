# Graphs (source: Data Structures and Algorithms in Java 6th Edition, Micheal T. Goodrich, Roberto Tamassia, Micheal H. Goldwasser)
## Definition of a Graph.
Not your usual bar or line graph 😄.
* A Graph is a way of representing relationships that exists between pairs of Objects (Vertices or nodes).
* A Graph data structure consists of a finite <b>set of vertices</b> (also known as nodes or objects as defined above☝️), together with a <b>set of edges</b> (also called links) that connect these vertices together.
* A Graph can be formally defined as $G = (V, E)$, where $V$ is a set of vertices and $E$ is a set of edges.

## The two main categories of a Graph are:
1️⃣ <b>Directed Graphs</b> - in this case, edges are ordered pairs (u, v), meaning the connection between the vertices has a direction from u to v.<br>
2️⃣ <b>Undirected Graphs</b> - in this case, endges are unordered pairs {u, v}, meaning the connection between the vertices is bidirecional.

## Some important terminology in Graph structures.
* Two vertices joined by an edge are called the <b>end vertices</b> or <b>endpoints</b> of the edge.
* If an edge is directed, its first endpoint is called the <b>origin edge</b> and the other endpoint is called the <b>destination edge</b>.
* Two vertices $u$ and $v$ are said to be <b>adjacent</b> if there exists an edge with endpoints $u$ and $v$.
* An edge is said to be <b>incident</b> to a vertex if the vertex is one of the edge's endpoints.
* The <b>outgoing edges</b> of a vertex are the directed edges whose origin is that vertex.
* The <b>incoming edges</b> of a vertex are the directed edges whose destination is that vertex.
* <b>The degree</b> of a vertex $v$, denoted by <b>deg(v)</b>, is the number of incident edges of $v$.
* The <b>in-degree</b> and <b>out degree</b> of a vertex $v$ are the number of the incoming and outgoing edges of $v$, and are denoted by <b>indeg(v)</b> and <b>outged(v)</b>, respectively.

## Core Operations of a Graph ADT
* <code>adjacent(G, x, y)</code> - Tests whether there is an edge from vertex $x$ to vertex $y$.
* <code>neighbors(G, x)</code>
* <code>add_vertex(G, x)</code>
* <code>remove_vertex(G, x)</code>
* <code>add_edge(G, x, y)</code>
* <code>remove_edge(G, x, y)</code>
* <code>get_vertex_value(G, x)</code>
* <code>set_vertex_value(G, x, v)</code>
* <code>get_edge_value(G, x, y)</code>
* <code>set_edge_value(G, x, y, v)</code>

## The Graph ADT
* As defined, a graph is a collection of <b>vertices</b> and <b>edges</b>.
* We model the abstraction as a combination of three data types:
  1. Vertex
  2. Edge
  3. Graph
 
* A <b>vertex</b> is a lightweight object that stores an arbitrary element provided by user (e.g., an airport code).
* We assume the element can be retrieved with the <code>getElement()</code> method.
* An <b>edge</b> also stores an associated object (e.g., a flight number, travel distance, cost), which is returned by its <code>getElement()</code> method.
* The primary abstraction for a graph is the Graph ADT.
* As defined, we presume that a graph can be either <b>undirected</b> or <b>directed</b>, with the destination declared upon construction.
* A mixed graph can be represented as directed graph, modeling $edge{u, v}$ as a pair of directed edge $(u, v)$ and $(v, u)$.
* The Graph ADT includes  the following methods:
  - <code><b>numVertices()</b> // Returns the number of vertices of the graph</code>
  - <code><b>vertices()</b> // Returns an iteration of all the vertices of the graph</code>
  - <code><b>numEdge()</b> // Returns the number of Edges of the graph</code>
  - <code><b>edges()</b> // /returns an iteration of all edges of the graph</code>
  - <code><b>getEdge(u, v)</b> // Returns the edge from vertex u to vertex v, if one exists. Otherwise return null. For an undirected graph, there is no difference between getEdge(u, v) and getEdge(v, u)</code>
  - <code><b>endVertices(e)</b> // Returns an array containing the two endpoint vertices of edge e. If the graph is directed, the first vertex is the origin and the second vertex is the destination</code>
  - <code><b>opposite(v, e)</b> // For edge e incident to vertex v, returns the other vertex of the edge. An error occurs if e is not incident to v.</code>
  - <code><b>outDegree(v)</b> // Returns the number of outgoing edges to vertex v</code>
  - <code><b>inDegree(v)</b> // Returns the number of incoming edges to vertex v. For an undireected graph, this returns the same value as does outDegree(v)</code>
  - <code><b>outgoingEdges(v)</b> // Returns an iteration of all outgoing edges from vertex v</code>
  - <code><b>incomingEdges(v)</b> // Returns an iteration of all incoming edges to vertex v. For an undirected graph, this returns the same collection as does outgoingEdges(v)</code>
  - <code><b>insertVertex(x)</b> // Creates and returns a new Vertex storing element x</code>
  - <code><b>insertEdge(u, v, x)</b> // Creates and returns a new Edge from vertex u to vertex v, storing an element x. An error occurs if there already exists an edge from u to v.</code>
  - <code><b>removeVertex(v)</b> //Removes vertex v and all its incident edges from the graph. </code>
  - <code><b>removeEdge(e)</b> // Removes edge e from the graph</code>

## Data Structures for Graphs
* There are four data structures for representing a graph. Each data structure maintains a collection to store the vertices of a graph.
* These four data structures differ greatly in the way they organize the edges:
  - In an <b>edge list</b>, we maintain  an unordered list of all edges.
    * This minimally suffices, but there is no efficient way to locate a particular edge $(u, v)$, or the set of all edges incident to a vertex.
  - In an <b>adjacency list</b>, we additionally maintain, for each vertex, a separate list containing those edges that are incident to the vertex.
    * This organization allows us to more efficiently find all edges incident to a givem vertex.
  - An <b>adjacency map</b> is similar to an adjacency list, but the secondary container of all edges incident to a vertex is organized as a map, rather than as a list, with the adjacent vertex serving as a key.
    * This allows more efficient access to a specific edge $(u, v)$, for example, in $O(1)$ expected time with hashing.
  - An <b>adjacency matrix</b> provides worst-case $O(1)$ access to a specific edge $(u, v)$ by maintaining an $n by n$ matrix, for a graph with $n$ vertices.
    * Each slot is dedicated to storing a reference to the edge $(u, v)$ for a particular pair of vertices u and v.
    * If no such edge exists, the slot will store null.
* A summary for the performance of these structures is given below:
<img width="518" height="290" alt="GraphDataStructures" src="https://github.com/user-attachments/assets/28615bc4-825e-4048-929e-e1dbee1de11e" />

### Edge List Structure
* The edge list structure is possibly the sinplest, though not the most efficient, representation of graph G.
* All the vertex objects are stored in an unordered list V, and all the edge objects are stored in an unordered list E.

  <img width="452" height="258" alt="EdgeListStructure" src="https://github.com/user-attachments/assets/866a39e0-44fb-40f8-9766-11b35960540b" />

* To support the many methods of the Graph ADT, we assume the following additional features of an edge list representation.
* Collections V and E are represented with doubly linked list using <code>LinkedPositionalList</code> class.
  * Vertex Objects
    - The vertex object for a vertex $v$ storing element $x$ has instance variables for:
      * A reference to element $x$, to support the <code>getElement()</code> method.
      * A reference to the position of the vertex instance in the list $V$, thereby allowing $v$ to be efficiently removed from $V$ if it were removed from the graph
  * Edge Objects
    - The edge object for vertex $v$ storing element $x$ has instance variables for:
      * A reference to element $x$, to support the <code>getElement()</code> method.
      * A reference to the vertex objects associated with the endpoint vertices of $e$. These will allow for constant-time support for methods <code>endVertices(e)</code> and <code>opposite(v, e)</code>.
      * A reference to the position of the edge instance in list $E$, thereby allowing $e$ to be efficiently removed from $E$ if it were removed from the graph.

### Adjacency List Structure
* The adjacency list structure for a graph adds extra information to the edge list structure that supports direct access to the incident edges, and thus to the adjacent vertices, of each vertex.
* Specifically, for each vertex $v$, we maintain a collection $I(v)$, called the incidence collection of $v$, whose entries are edge incident to $v$.
* In the case of a directed graph, outgoing and incoming edges can be respectively stored in two separate collections.
* Traditionally, the incidence collection $I(v)$ for a vertex v is a list, which is why we call this way of representing a graph the adjacency list structure.
* We require that the primaty structure for an adjacency list maintain the collection V of vertices in a way so that we can locate the secondary structure $I(v)$ for a given vertex $v$ in $O(1)$ time.
* This could be done by using positional list to represent V, with each Vertex instance maintaining a direct reference to its $I(v)$ incident collecton.

   <img width="467" height="247" alt="AdjacencyListStructure" src="https://github.com/user-attachments/assets/3956926d-8c2b-4f86-83cc-08dadf7da935" />
* If vertices can be uniquely numbered from 0 to $n - 1$, we could instead use a primary array-based structure to access the appropriate seconday list.
* The primary benefit of an adjacency list is that the collection $I(v)$ contains exactly those edges that should be reported by the method <code>outgoingEdges(v)</code> ($I(v)out$).
* Therefore, we can implement this method by iterating the edges of $I(v)& in $O(deg(v))$ time, where $deg(v)$ is the degree of vertex $v$.
* This is the best possible outcome for any graph representation, because there are $deg(v)$ edges to be reported.

### Adjacency Map Structure
* In the adjacency list structure, we assemu that the secondary incidence collections are implemented as unordered linked lists.
* Such a collection $I(v)$ uses space proportional to $O(deg(v))$, allows an edge to be added or removed in $O(1)$ time, and allows an iteration of all edges incident to vertex $v$ in #O(deg(v))$ time.
* However, the best implementation of <code>getEdge(u, v)</code> requires $O(min(deg(u), deg(v)))$ time, because we must search through either $I(u)$ ir $I(v)$.
* We can improve the performance by using a hash-based map to implement $I(v)$ for each vertex $v$.
* Specifically, we let the opposite endpoint of each incident edge serve as a key in the map, with the edge structure serving as the value.
* We call such a graph representation an adjacency map.

  <img width="463" height="275" alt="AdjacencyMap" src="https://github.com/user-attachments/assets/7ca6e63b-8bf5-4676-9a26-fa757e749ca3" />

* The space usage for an adjacency map remains $O(n + m)$, because $I(v)$ uses $O(deg(v))$ space for each vertex $v$, as with the adjacency list.
* The advantage of the adjacency map, relative to an adjacency list, is that the <code>getEdge(u, v)</code> method can be implemented in expected $O(1)$ tme by searching for vertex u as a key in $I(v)$, or vice versa.
* This provides a likely improvement over the adjacency list, while retaining the worst-case bound of $O(min(deg(u), deg(v)))$.

### Adjacency Matrix Structure
* The adjacency matrix structure for a graph G augments the edge list structure with a matrix A, which allows us to locate an edge between a given pair of vertices in worst-case constant time.
* In the adjacency matrix representation, we think of the vertices as being integers in the set ${0, 1, ..., n - 1}$ and the edges as being pairs of such integers.
* this allows us to store references to edges in the cells of a two-dimensional $n by n$ array A.
* Specifically, the cell $A[i][j]$ holds a reference to the edge $(u, v)$, if it exists, where $u$ is the vertex with index $i$ and $v$ is the vertex with index $j$.
* If there is no such edge, then $A[i][j] = null$.
* We note that array A is symmetric if graph G is undirected, as $A[i][j] = A[j][i]$ for all pairs $i$ and $j$.
* The most significant advantage of an adjacency matrix is that any edge $(u, v)$ can be accessed in worst-case $O(1)$ time.
* However, several opeations are less efficient with an adjacency matrix.
<img width="453" height="154" alt="AdjacencyMatrix" src="https://github.com/user-attachments/assets/106a552f-9576-4070-bc89-442851d98bc2" />

## Java Implementation: 💻 Graph ADT based on the adjacency map
* We use positional list to represent each of the primary list $V$ and $E$.
* Additionally, for each vertex $v$, we use a hash-based mao to represent the secondary incident map $I(v)$.
* To support both undirected and directed graphs, each vertex maintains two different map references, outgoing and incoming.
* In the directed case, these are initialized to two distinct map instances, representing $I(v) out$ and $I(v) in$, respectively.
* In the case of an undirected graph, we assign both outgoing and incoming as aliases to a single map instance.
* Our implementation is as follows:
  * We assume Vertex, Edge, and Graph interfaces.
  * We then define a concrete <code>AdjacencyMapGraph</code> class, with nested classes <code>InnerVertex</code> and <code>InnerEdge</code> to implement the vertex and edge abstractions.
  * these classes use generic parameters V and E to designate the element type stored respectively at vertices and edges.
 
## Graph Traversals
* Graph traversal is a systematic procedure for exploring a graph by examining all of its vertices and edges..
* A traversal is efficient if it visits all the vertcies and edges in time proportional to their number.
* Graph traversal algorithms are key in determining how to travel from one vertex to another while following paths of a graph.
* Some problems that deal with reachability in an undirected graph $G$ include the following:
  - Computing a path from vertex $u$ to vertex $v$, or reporting that no such path exists.
  - Given a start vertex $s$ of $G$, computing , for every vertex $v$ of $G$, a path with the minimum number of edges between $s$ and $v$, or reporting that no such path exists.
  - Testing whether $G$ is connected
  - Computing a spanning tree of $G$, if $G$ is connected
  - Computing the connected componets of $G$
  - Identifying a cycle in $G$, or reporting that $G$ has no cycles
 
* Some problems that deal with reachability in a directed graph $G$ include the following:
  - Computing a directed path from vertex $u$ to vertex $v$, or reporting that no such path exists.
  - Finding all the vertices of $G$ that are reachable from a given vertex $s$.
  - Determine whether $G$ is acyclic.
  - Determine  whether $G$ is strongly connected.
 
  * The two efficient graph traversals are:
    1. Depth-First search
    2. Breath-First search

### Depth-First Search
* This algorithm is useful for testing a number of properties of graphs including whether there is a path from one vertex to another and whether or not a graph is connected.
* DFS is analogous to wandering in a 'maze' with a string and a can of paint without getting lost.
* We begin at a starting point vertex $s$ in $G$, which we initialize by fixing one end of our string to $s$ and painting $s$ as visited.
* The vertex $s$ is now our current vertex.
* In general, if we call our current vertex $u$, we traverse $G$ by considering an arbitrary edge $(u, v)$ incident to the current vertex $u$.
* If the edge $(u, v)$ leads us to a vertex $v$ that is already visited, we ignore that edge.
* If, on the other hand, $(u, v)$ leads to an unvisited vertex $v$, then we unroll out string, and go to $v$.
* We then paint $v$ as visited, and make it the current vertex, repeating the computation.
* Eventually, we will get to a vertex $v$ such that all the edges incident to $v$ lead to vertices already visited.
* To get out of this impasse, we roll our string back up, backtracking along the edge that brought us to $v$, going back to a previously visited vertex $u$.
* We then ,ake $u$ our current vertex and repeat the compuatation above for any edges incident to $u$ that we have not yet considered.
* If all of $u$'s incident edges lead to vissited vertices, then we again roll up our string and backtrack to the vertex we came from to get to $u$, and repeat the procedure at that vertex.
* Thus, we continue to backtrack along the path that we have traced so far until we find a vertex that has yet unexplored edges, take one such edge, and continue the traversa.
* The process terminates when our backtracking leads us back to the start vertex $s$, and there are no more unexpected edges incident to $s$.

#### Classifying Graph Edges with DFS
* An execution of DFS can be used to analyze the structure of a graph, based upon the way in which edges are explored during the traversal.
* The DFS process naturally identifies what is known as the <b>Depth-First Search Tree</b> rooted at a starting vertex $s$.
* whenever an edge $e = (u, v)$ is used to discover a new vertex $v$ suring the DFS, that edge is know as a <b>discovery edge</b> or <b>tree edge</b>, as oriented from $u$ to $v$.
* All other edges that are considered suring the execution of DFS are known as <b>nontree edges</b>, which take us to a previously visited vertex.
* In the case of an undirected graph, we will find that all nontree edges that are explored connect the current vertex to one that is an ancestor of it in the DFS tree.
* We will call such an edge a <b>back edge</b>.
* When performing a DFS on a directed graph, there are three possible kinds of nontree edges:
  - Back edges - Edges which connect a vertex to an ancestor in the DFS tree.
  - Forward edges - Edges which connect a vertex to a descendant in the DFS tree.
  - Cross edges - Edges which connect a vertex to a vertex that is neither its ancesto nor its descendant.
 
#### Properties of a DFS
* Let $G$ be an undirected graph on which a DFS traversal starting at a vertex $s$ has been performed.
  * Then the traversal visits all vertices in the connected component of $s$, and the discovery edges form a spanning tree of the connected component of $s$.
