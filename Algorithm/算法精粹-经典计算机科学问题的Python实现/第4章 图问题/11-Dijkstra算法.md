### Dijkstra算法

Dijkstra算法能解决单源最短路径问题。只要给定一个起始顶点，它就会返回抵达加权图中其他任一顶点的最小权重路径，同时它还会返回从起始顶点到其他每一个顶点的最小总权重。Dijkstra算法从单源顶点开始，不断探索距离起始顶点最近的顶点，因此，与Jarník算法类似，Dijkstra算法也是一种贪婪算法。当Dijkstra算法遇到新顶点时，将会记录新顶点与起始顶点之间的距离，并在找到更短路径时更新该距离值。Dijkstra算法还会把到达每个顶点的边都记录下来，就像广度优先搜索一样。

下面是Dijkstra算法的全部步骤。

（1）将起始顶点加入优先队列。

（2）从优先队列中弹出距离最近的顶点（一开始即为起始顶点），我们称之为当前顶点。

（3）逐个查看连接到当前顶点的所有邻居。如果之前这些顶点尚未被记录过，或者到这些顶点的边给出了新的最短路径，就逐个记录它们与起点之间的距离以及产生该距离的边，并把新顶点加入优先队列。

（4）重复第2步和第3步，直至优先队列为空为止。

（5）返回起始顶点与每个顶点之间的最短距离和路径。

Dijkstra算法的代码中包含一个简单的数据结构 `DijkstraNode` ，用于记录目前已探索的每个顶点相关的成本，以便用于比较。这类似于第2章的 `Node` 类。它还包含几个实用函数，涉及将返回的距离数组转换为更易于按顶点查找的结构，以及用 `dijkstra()` 返回的路径字典计算出到指定目标顶点的最短路径。

言归正传，下面给出Dijkstra算法的代码，如代码清单4-13所示。后面将会逐行过一遍这段代码。

代码清单4-13　dijkstra.py

```c
from __future__ import annotations
from typing import TypeVar, List, Optional, Tuple, Dict
from dataclasses import dataclass
from mst import WeightedPath, print_weighted_path
from weighted_graph import WeightedGraph
from weighted_edge import WeightedEdge
from priority_queue import PriorityQueue
V = TypeVar('V') # type of the vertices in the graph
@dataclass
class DijkstraNode:
    vertex: int
    distance: float
    def __lt__(self, other: DijkstraNode) -> bool:
        return self.distance < other.distance
    def __eq__(self, other: DijkstraNode) -> bool:
        return self.distance == other.distance
def dijkstra(wg: WeightedGraph[V], root: V) -> Tuple[List[Optional[float]], Dict[int,
     WeightedEdge]]:
    first: int = wg.index_of(root) # find starting index
    # distances are unknown at first
    distances: List[Optional[float]] = [None] * wg.vertex_count
    distances[first] = 0 # the root is 0 away from the root
    path_dict: Dict[int, WeightedEdge] = {} # how we got to each vertex
    pq: PriorityQueue[DijkstraNode] = PriorityQueue()
    pq.push(DijkstraNode(first, 0))
    while not pq.empty:
        u: int = pq.pop().vertex # explore the next closest vertex
        dist_u: float = distances[u] # should already have seen it
        # look at every edge/vertex from the vertex in question
        for we in wg.edges_for_index(u): 
            # the old distance to this vertex
            dist_v: float = distances[we.v] 
            # no old distance or found shorter path
            if dist_v is None or dist_v > we.weight + dist_u: 
                # update distance to this vertex
                distances[we.v] = we.weight + dist_u
                # update the edge on the shortest path to this vertex
                path_dict[we.v] = we 
                # explore it soon
                pq.push(DijkstraNode(we.v, we.weight + dist_u)) 
    return distances, path_dict
# Helper function to get easier access to dijkstra results
def distance_array_to_vertex_dict(wg: WeightedGraph[V], distances: List[Optional[float]])
     -> Dict[V, Optional[float]]:
    distance_dict: Dict[V, Optional[float]] = {}
    for i in range(len(distances)):
        distance_dict[wg.vertex_at(i)] = distances[i]
    return distance_dict
# Takes a dictionary of edges to reach each node and returns a list of
# edges that goes from `start` to `end`
def path_dict_to_path(start: int, end: int, path_dict: Dict[int, WeightedEdge]) ->
    WeightedPath:
    if len(path_dict) == 0:
        return []
    edge_path: WeightedPath = []
    e: WeightedEdge = path_dict[end]
    edge_path.append(e)
    while e.u != start:
        e = path_dict[e.u]
        edge_path.append(e)
    return list(reversed(edge_path))

```

`dijkstra()` 的前几行用到了我们熟悉的数据结构，但 `distances` 除外，它是从 `root` 到图中每个顶点的距离的占位符。最初所有这些距离都是 `None` ，因为我们尚不知道这些距离有多长，这正是要用Dijkstra算法来弄清楚的事情！

```c
def dijkstra(wg: WeightedGraph[V], root: V) ->Tuple[List[Optional[float]], Dict[int, 
     WeightedEdge]]:
    first: int = wg.index_of(root) # find starting index
    # distances are unknown at first
    distances: List[Optional[float]] = [None] * wg.vertex_count
    distances[first] = 0 # the root is 0 away from the root
    path_dict: Dict[int, WeightedEdge] = {} # how we got to each vertex
    pq: PriorityQueue[DijkstraNode] = PriorityQueue()
    pq.push(DijkstraNode(first, 0))

```

第一个压入优先队列的节点包括根顶点。

```c
while not pq.empty:
    u: int = pq.pop().vertex # explore the next closest vertex
    dist_u: float = distances[u] # should already have seen it

```

Dijkstra算法将持续运行，直至优先级队列变空为止。 `u` 是我们正要搜索的当前顶点， `dist_u` 是已记录下来的沿着已知路径到达 `u` 的距离。当前探索过的每个顶点都是已找到的，因此它们必须带有已知的距离。

```c
# look at every edge/vertex from here
for we in wg.edges_for_index(u): 
    # the old distance to this
    dist_v: float = distances[we.v]

```

接下来，对连接到 `u` 的每条边进行探索。 `dist_v` 是指从 `u` 到任何已知与 `u` 有边相连的顶点的距离。

```c
# no old distance or found shorter path
if dist_v is None or dist_v > we.weight + dist_u:
    # update distance to this vertex
    distances[we.v] = we.weight + dist_u
    # update the edge on the shortest path
    path_dict[we.v] = we 
    # explore it soon
    pq.push(DijkstraNode(we.v, we.weight + dist_u))

```

如果我们发现一个尚未被探索过（ `dist_v` 为 `None` ）的顶点，或者找到一条新的、更短的路径能到达它，就会记录到达 `v` 的新的最短距离和到达那里的边。最后，我们把新发现路径到达的顶点全都压入优先队列。

```c
return distances, path_dict

```

`dijkstra()` 返回从根顶点到加权图中每个顶点的距离，以及能够揭示到达这些顶点的最短路径的 `path_dict` 。

现在我们可以放心运行Dijkstra算法了。我们先从Los Angeles开始测算到达图中其他所有MSA的距离，然后就会找到Los Angeles和Boston之间的最短路径，最后，将用 `print_weighted_path()` 美观打印出结果。具体代码如代码清单4-14所示。

代码清单4-14　dijkstra.py（续）

```c
if __name__ == "__main__":
    city_graph2: WeightedGraph[str] = WeightedGraph(["Seattle", "San Francisco", "Los 
     Angeles", "Riverside", "Phoenix", "Chicago", "Boston", "New York", "Atlanta",
     "Miami",  "Dallas", "Houston", "Detroit", "Philadelphia", "Washington"])
    city_graph2.add_edge_by_vertices("Seattle", "Chicago", 1737)
    city_graph2.add_edge_by_vertices("Seattle", "San Francisco", 678)
    city_graph2.add_edge_by_vertices("San Francisco", "Riverside", 386)
    city_graph2.add_edge_by_vertices("San Francisco", "Los Angeles", 348)
    city_graph2.add_edge_by_vertices("Los Angeles", "Riverside", 50)
    city_graph2.add_edge_by_vertices("Los Angeles", "Phoenix", 357)
    city_graph2.add_edge_by_vertices("Riverside", "Phoenix", 307)
    city_graph2.add_edge_by_vertices("Riverside", "Chicago", 1704)
    city_graph2.add_edge_by_vertices("Phoenix", "Dallas", 887)
    city_graph2.add_edge_by_vertices("Phoenix", "Houston", 1015)
    city_graph2.add_edge_by_vertices("Dallas", "Chicago", 805)
    city_graph2.add_edge_by_vertices("Dallas", "Atlanta", 721)
    city_graph2.add_edge_by_vertices("Dallas", "Houston", 225)
    city_graph2.add_edge_by_vertices("Houston", "Atlanta", 702)
    city_graph2.add_edge_by_vertices("Houston", "Miami", 968)
    city_graph2.add_edge_by_vertices("Atlanta", "Chicago", 588)
    city_graph2.add_edge_by_vertices("Atlanta", "Washington", 543)
    city_graph2.add_edge_by_vertices("Atlanta", "Miami", 604)
    city_graph2.add_edge_by_vertices("Miami", "Washington", 923)
    city_graph2.add_edge_by_vertices("Chicago", "Detroit", 238)
    city_graph2.add_edge_by_vertices("Detroit", "Boston", 613)
    city_graph2.add_edge_by_vertices("Detroit", "Washington", 396)
    city_graph2.add_edge_by_vertices("Detroit", "New York", 482)
    city_graph2.add_edge_by_vertices("Boston", "New York", 190)
    city_graph2.add_edge_by_vertices("New York", "Philadelphia", 81)
    city_graph2.add_edge_by_vertices("Philadelphia", "Washington", 123)
    distances, path_dict = dijkstra(city_graph2, "Los Angeles")
    name_distance: Dict[str, Optional[int]] = distance_array_to_vertex_dict(city_graph2,
    distances)
    print("Distances from Los Angeles:")
    for key, value in name_distance.items():
        print(f"{key} : {value}")
    print("") # blank line
    print("Shortest path from Los Angeles to Boston:")
    path: WeightedPath = path_dict_to_path(city_graph2.index_of("Los Angeles"), city_
     graph2.index_of("Boston"), path_dict)
    print_weighted_path(city_graph2, path)

```

输出应该会如下所示：

```c
Distances from Los Angeles:
Seattle : 1026
San Francisco : 348
Los Angeles : 0
Riverside : 50 
Phoenix : 357
Chicago : 1754
Boston : 2605
New York : 2474
Atlanta : 1965
Miami : 2340
Dallas : 1244
Houston : 1372
Detroit : 1992
Philadelphia : 2511
Washington : 2388
Shortest path from Los Angeles to Boston:
Los Angeles 50> Riverside
Riverside 1704> Chicago
Chicago 238> Detroit
Detroit 613> Boston
Total Weight: 2605
```

或许大家已经注意到了，Dijkstra算法与Jarník算法有一些相似之处。它们都是贪婪算法，如果有人动力十足，完全可以用相当类似的代码去实现它们。另一个与Dijkstra类似的算法是第2章中讲过的A*算法。A*算法可以被认为是对Dijkstra算法的改进。这两种算法都一样，加入启发式信息并将Dijkstra算法限定为查找单个目标。



**注意** 　Dijkstra算法是为具有正权重的图设计的。对Dijkstra算法而言，边的权重为负数的图是一个挑战，因此需要做出相应修改或换用别的算法。



