<h1>ExpNo 4 : Implement A* search algorithm for a Graph</h1>

<h3>Name: Bhuvaneshwaran TU     </h3>
<h3>Register Number: 212224040049           </h3>

<h3>Aim:</h3>
<p>To Implement A* Search algorithm for a Graph using Python 3.</p>

<h3>Algorithm:</h3>

<pre>
1. Initialize the OPEN list.
2. Initialize the CLOSED list.
3. Add the starting node to the OPEN list.
4. While the OPEN list is not empty:
   a) Select the node with the lowest f value.
   b) Remove the node from the OPEN list.
   c) If the node is the goal, display the path.
   d) Otherwise, examine its neighboring nodes.
   e) Calculate g, h and f values.
      f(n) = g(n) + h(n)
   f) Update the parent and cost if a better path is found.
   g) Add the expanded node to the CLOSED list.
5. Repeat until the goal is found or OPEN is empty.
</pre>

<hr>

<h2>Python Program</h2>

<hr>

<pre><code>
import heapq

def astar(graph, heuristic, start, goal):
    open_list = []
    heapq.heappush(open_list, (heuristic[start], 0, start))

    g_cost = {start: 0}
    parent = {start: None}
    closed = set()

    while open_list:
        f, cost, node = heapq.heappop(open_list)

        if node in closed:
            continue

        if node == goal:
            path = []
            current = node

            while current is not None:
                path.append(current)
                current = parent[current]

            path.reverse()
            print("Path found:", path)
            return path

        closed.add(node)

        for neighbor, weight in graph[node]:
            new_cost = g_cost[node] + weight

            if new_cost < g_cost.get(neighbor, float("inf")):
                g_cost[neighbor] = new_cost
                parent[neighbor] = node

                if neighbor in closed:
                    closed.remove(neighbor)

                heapq.heappush(
                    open_list,
                    (
                        new_cost + heuristic[neighbor],
                        new_cost,
                        neighbor
                    )
                )

    print("Path not found")
    return None


n, m = map(int, input().split())

graph = {}

for _ in range(m):
    u, v, w = input().split()
    w = int(w)

    graph.setdefault(u, []).append((v, w))
    graph.setdefault(v, []).append((u, w))

heuristic = {}

for _ in range(n):
    node, h = input().split()
    heuristic[node] = int(h)
    graph.setdefault(node, [])

start = input().strip()
goal = input().strip()

astar(graph, heuristic, start, goal)
</code></pre>

<hr>

<h2>Sample Graph I</h2>

<hr>

![Sample Graph I](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/b1377c3f-011a-4c0f-a843-516842ae056a)

<hr>

<h2>Sample Input</h2>

<hr>

<pre>
10 14
A B 6
A F 3
B D 2
B C 3
C D 1
C E 5
D E 8
E I 5
E J 5
F G 1
G I 3
I J 3
F H 7
I H 2
A 10
B 8
C 5
D 7
E 3
F 6
G 5
H 3
I 1
J 0
A
J
</pre>

<hr>

<h2>Sample Output</h2>

<hr>

<pre>
Path found: ['A', 'F', 'G', 'I', 'J']
</pre>

<hr>

<h2>Sample Graph II</h2>

<hr>

![Sample Graph II](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/acbb09cb-ed39-48e5-a59b-2f8d61b978a3)

<hr>

<h2>Sample Input</h2>

<hr>

<pre>
6 6
A B 2
B C 1
A E 3
B G 9
E D 6
D G 1
A 11
B 6
C 99
E 7
D 1
G 0
A
G
</pre>

<hr>

<h2>Sample Output</h2>

<hr>

<pre>
Path found: ['A', 'E', 'D', 'G']
</pre>

<hr>

<h2>Result</h2>

<p>Thus, the A* Search Algorithm was successfully implemented in Python 3 to find a path from the starting node to the goal node using edge costs and heuristic values.</p>
