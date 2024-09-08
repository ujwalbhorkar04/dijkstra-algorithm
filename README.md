# dijkstra-algorithm
Implementation of Dijkstra algorithm in C

#include <stdio.h>
#define MAX 100
#define INF 99999 // Infinite value for unreachable paths

int n; // Number of nodes
int adjMatrix[MAX][MAX]; // Graph adjacency matrix
int dist[MAX]; // Stores shortest distance from source to each node
int visited[MAX] = {0}; // Marks visited nodes

// Function to find the node with the smallest distance
int minDistance() {
    int min = INF, minIndex;

    for (int i = 0; i < n; i++) {
        if (!visited[i] && dist[i] < min) {
            min = dist[i];
            minIndex = i;
        }
    }
    return minIndex;
}

// Dijkstra's algorithm
void dijkstra(int startNode) {
    for (int i = 0; i < n; i++) {
        dist[i] = INF; // Initialize all distances as infinite
    }
    dist[startNode] = 0; // Distance from start node to itself is 0

    for (int count = 0; count < n - 1; count++) {
        int u = minDistance(); // Get the node with minimum distance
        visited[u] = 1; // Mark the node as visited

        for (int v = 0; v < n; v++) {
            // Update dist[v] if there's a shorter path through u
            if (!visited[v] && adjMatrix[u][v] && dist[u] != INF && dist[u] + adjMatrix[u][v] < dist[v]) {
                dist[v] = dist[u] + adjMatrix[u][v];
            }
        }
    }

    // Print the shortest distances
    printf("Node\tDistance from Source\n");
    for (int i = 0; i < n; i++) {
        printf("%d\t%d\n", i, dist[i]);
    }
}

int main() {
    int edges, u, v, weight, start;

    printf("Enter the number of nodes: ");
    scanf("%d", &n);

    printf("Enter the number of edges: ");
    scanf("%d", &edges);

    // Input graph connections (edges) and weights
    for (int i = 0; i < edges; i++) {
        printf("Enter edge (u v) and weight: ");
        scanf("%d %d %d", &u, &v, &weight);
        adjMatrix[u][v] = weight;
        adjMatrix[v][u] = weight; // For undirected graph
    }

    printf("Enter the start node for Dijkstra: ");
    scanf("%d", &start);

    dijkstra(start);

    return 0;
}

