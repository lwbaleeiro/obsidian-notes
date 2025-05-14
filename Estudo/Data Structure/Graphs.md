Graphs represent sets of objects and their relationships. A simple implementation using adjacency lists. Graphs are used to model networks, transportation systems, social relationships, and many other real-world structures.

**Example:**
```java
import java.util.*;

public class Graph {
	private int V;
	private  LinkedList<Integer>[] adj;

	public Graph(int V) {
		this.V = v;
		adj = new LinkedList[v];
		for (int i = 0; i < v; i++) {
			adj[i] = new LinkedList<>();
		}
	}

	public void adicionaAresta(int origem, int destino) {
		adj[origem].add(destino);
	}

	// Busca em largura (BFS)
	public void BFS(int inicial) {
		boolean[] visitados = new boolean[V];
	
		LinkedList<Integer> file = new LinkedList<>();
		//Marca o vertice atual como visitado
		visitados[inicial] = true;
		fila.add(inicial);

		while (!fila.empty()) {
			// Remove um vertice da fila e o imprime
			inicial = fila.poll();
			System.out.println(inicial + " ");

			// Obtem todos os vertices adjacentes ao vertice removido
			// Se um adjacente não foi visitado, marca-o como visitado
			// E o adiciona na fila.
			Interator<Integer> i = adj[inicial].listInterator();
			while(i.hasNext()) {
				int n = i.next();
				if (!visitados[n]) {
					visitados[n] = true;
					fila.add(n);
				}
			}
		}
	}

	// Busca em profundidade (DFS)
	public void DFS(int inicial) {
		// Marca todos os vertices como não visitados
		boolean[] visitados = new boolean[V];
		// Chama o metodo auxiliar recursivo
		DFSUtil(inicial, visitados);
	}

	private void DFSUtil(int v, boolean[] visitados) {
		// Marca o vertice atual como visitado e o imprime
		visitados[v] = true;
		System.out.println(v + " ");

		// Recorre a todos os vertices adjacentes a este vertice
		Iterator<Integer> i = adj[v].listIterator();
		while(i.hasNext()) {
			int n = i.next();
			if (!visitados[n])  {
				DFSUtil(n, visitados);
			}
		}
	}

	public static void main(String[] args) {
		Grafo g = newGrafo(6);
		
		g.adicionarAresta(0, 1);
        g.adicionarAresta(0, 2);
        g.adicionarAresta(1, 3);
        g.adicionarAresta(2, 3);
        g.adicionarAresta(2, 4);
        g.adicionarAresta(3, 4);
        g.adicionarAresta(3, 5);
        g.adicionarAresta(4, 5);

		System.out.println("BFS começando do vértice 0:"); 
		g.BFS(0); 
		
		System.out.println("\nDFS começando do vértice 0:"); 
		g.DFS(0);
	}
}
```

**Best used when:**
To model relationships between objects.