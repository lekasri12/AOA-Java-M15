
# EX 5E Minimum Spanning Tree -Boruvka's Algorithm
## DATE: 15.11.2025
## AIM:
To write a Java program to for given constraints.
Boruvka's Algorithm - Minimum Spanning Tree

Find the MST using Boruvka's Algorithm for a weighted undirected graph.
<img width="292" height="235" alt="image" src="https://github.com/user-attachments/assets/06246b27-37a9-40a8-bd7a-37a1d5187cd1" />

## Algorithm
1.Start and read the number of vertices V and edges E of the graph.

2.Initialize each vertex as a separate component (Disjoint Set / Union-Find).

3.For every component, find its cheapest outgoing edge connecting it to another component.

4.Add all such cheapest edges to the MST and merge (union) the connected components.

5.Repeat until all vertices belong to a single component, then print the total MST weight.
   

## Program:
```
/*
Developed by: LEKASRI G
RegisterNumber:  212223100025
*/
import java.util.*;

public class BoruvkaMST {
    static int[] parent;

    static int find(int i) {
        if (parent[i] != i)
            parent[i] = find(parent[i]);
        return parent[i];
    }

    static void union(int x, int y) {
        parent[find(x)] = find(y);
    }

    
    static int boruvkaMST(int V, List<Edge> edges) {
        parent = new int[V];
        for (int i = 0; i < V; i++) parent[i] = i;

        int components = V;
        int mstWeight = 0;

        while (components > 1) {
            Edge[] cheapest = new Edge[V];

            // Find cheapest edge for each component
            for (Edge e : edges) {
                int set1 = find(e.src), set2 = find(e.dest);
                if (set1 == set2) continue;

                if (cheapest[set1] == null || cheapest[set1].weight > e.weight)
                    cheapest[set1] = e;

                if (cheapest[set2] == null || cheapest[set2].weight > e.weight)
                    cheapest[set2] = e;
            }

            // Add cheapest edges to MST and union the components
            for (int i = 0; i < V; i++) {
                Edge e = cheapest[i];
                if (e != null && find(e.src) != find(e.dest)) {
                    mstWeight += e.weight;
                    union(e.src, e.dest);
                    components--;
                    System.out.println("Edge: " + e.src + "-" + e.dest + " Weight: " + e.weight);
                }
            }
        }
        return mstWeight;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int V = sc.nextInt();
        int E = sc.nextInt();

        List<Edge> edges = new ArrayList<>();
        for (int i = 0; i < E; i++) {
            edges.add(new Edge(sc.nextInt(), sc.nextInt(), sc.nextInt()));
        }

        int totalWeight = boruvkaMST(V, edges);
        System.out.println("Total Weight of MST: " + totalWeight);

        sc.close();
    }
}

class Edge {
    int src, dest, weight;
    Edge(int s, int d, int w) {
        src = s; dest = d; weight = w;
    }
}

```

## Output:

<img width="624" height="470" alt="image" src="https://github.com/user-attachments/assets/7f428f33-8068-4a89-98a6-6be1f413cc92" />


## Result:
The program successfully implemented and the expected output is verified.
