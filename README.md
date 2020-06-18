# REII211-PRACTICAL-2
#include <stdio.h> 
#include <limits.h> 
#define V 8 

// function to find the minimum value, from the set of vertices not yet included in shortest 
// path tree 
int minDistance(int dist[], 
				bool sptSet[]) 
{ 
	

	int min = INT_MAX, min_index; 

	for (int v = 0; v < V; v++) 
		if (sptSet[v] == false && 
				dist[v] <= min) 
			min = dist[v], min_index = v; 

	return min_index; 
} 

// Function to print shortest path from source to j using parent array 
void printPath(int parent[], int j) 
{ 
	
	if (parent[j] == - 1) 
		return; 

	printPath(parent, parent[j]); 

	printf("%d ", j); 
} 

// function to print the constructed distance array 
int printSolution(int dist[], int n, 
					int parent[]) 
{ 
	int src = 0; 
	printf("Vertex\t Distance\tPath"); 
	for (int i = 1; i < V; i++) 
	{ 
		printf("\n%d -> %d \t\t %d\t\t%d ", 
					src, i, dist[i], src); 
		printPath(parent, i); 
	} 
} 


void dijkstra(int graph[V][V], int src) 
{ 
	

	int dist[V]; 

	bool sptSet[V]; 

	
	int parent[V]; 

	// Initialize all distances

	for (int i = 0; i < V; i++) 
	{ 
		parent[0] = -1; 
		dist[i] = INT_MAX; 
		sptSet[i] = false; 
	} 

	dist[src] = 0; 

	// Find shortest path 
	 
	for (int count = 0; count < V - 1; count++) 
	{ 
		 
		int u = minDistance(dist, sptSet); 

		 
		sptSet[u] = true; 

	
		for (int v = 0; v < V; v++) 

			 
			if (!sptSet[v] && graph[u][v] && 
				dist[u] + graph[u][v] < dist[v]) 
			{ 
				parent[v] = u; 
				dist[v] = dist[u] + graph[u][v]; 
			} 
	} 

	
	printSolution(dist, V, parent); 
} 


int main() 
{ 
	int graph[V][V] ={ { 0, 10, 9, 0, 0, 0, 0, 0 }, 
						{ 10, 0, 9, 3, 1, 0, 0, 0 }, 
						{ 9, 9, 0, 6, 5, 0, 0, 0 }, 
						{ 0, 3, 6, 0, 4, 2, 5, 0 }, 
						{ 0, 1, 5, 4, 0, 2, 1, 0 }, 
						{ 0, 0, 0, 2, 2, 0, 6, 5 }, 
						{ 0, 0, 0, 5, 1, 6, 0, 7 }, 
						{ 0, 0, 0, 0, 0, 5, 7, 0 }, 
					}; 

	dijkstra(graph, 0); 
	return 0; 
} 
