#include <iostream>
#include <vector>
#include <queue>
#include <stack>
#include <chrono>

using namespace std;
using namespace chrono;

class Graph {
    int V;
    vector<vector<int>> adjMatrix;   // adjacency matrix representation

public:
    Graph(int v) {
        V = v;
        adjMatrix.assign(V, vector<int>(V, 0));
    }

    void addEdge(int u, int v) {
        adjMatrix[u][v] = 1;
        adjMatrix[v][u] = 1;
    }

    // Iterative DFS using an explicit stack
    void DFS(int start) {
        vector<bool> visited(V, false);
        stack<int> st;

        st.push(start);

        while (!st.empty()) {
            int node = st.top();
            st.pop();

            if (!visited[node]) {
                visited[node] = true;
                cout << node << " ";
            }

            // push neighbours in reverse order so traversal order
            // matches the natural (ascending) order like the recursive version
            for (int next = V - 1; next >= 0; next--) {
                if (adjMatrix[node][next] == 1 && !visited[next]) {
                    st.push(next);
                }
            }
        }
    }

    void BFS(int start) {
        vector<bool> visited(V, false);
        queue<int> q;

        visited[start] = true;
        q.push(start);

        while (!q.empty()) {
            int node = q.front();
            q.pop();

            cout << node << " ";

            for (int next = 0; next < V; next++) {
                if (adjMatrix[node][next] == 1 && !visited[next]) {
                    visited[next] = true;
                    q.push(next);
                }
            }
        }
    }
};

int main() {
    int V, E;

    cout << "Enter number of vertices: ";
    cin >> V;

    Graph g(V);

    cout << "Enter number of edges: ";
    cin >> E;

    cout << "Enter edges:\n";

    for (int i = 0; i < E; i++) {
        int u, v;
        cin >> u >> v;
        g.addEdge(u, v);
    }

    int start;
    cout << "Enter starting vertex: ";
    cin >> start;

    // DFS
    auto startDFS = high_resolution_clock::now();

    cout << "\nDFS Traversal (Iterative, Adjacency Matrix): ";
    g.DFS(start);

    auto endDFS = high_resolution_clock::now();
    auto dfsTime = duration_cast<nanoseconds>(endDFS - startDFS);

    // BFS
    auto startBFS = high_resolution_clock::now();

    cout << "\nBFS Traversal (Adjacency Matrix): ";
    g.BFS(start);

    auto endBFS = high_resolution_clock::now();
    auto bfsTime = duration_cast<nanoseconds>(endBFS - startBFS);

    // Display execution time
    cout << "\n\nExecution Time:";
    cout << "\nDFS: " << dfsTime.count() << " ns";
    cout << "\nBFS: " << bfsTime.count() << " ns";

    return 0;
}
