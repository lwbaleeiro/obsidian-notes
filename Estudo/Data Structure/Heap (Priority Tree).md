Heaps are complete or nearly complete binary trees where each node satisfies the heap property (maximum or minimum). Heaps are useful in algorithms like Dijkstra (shortest path search), HeapSort sorting, and problems involving finding the k-th larges/smallest element.

**Example:**
```java
import java.util.PriorityQueue;

public class ExamplePriorityQueue {
	public static void main(String[] args) {
		PriorityQueue<Integer> minHeap = new PriorityQueue<>();

		minHeap.add(30);
		minHeap.add(10);
		minHeap.add(20);
		minHeap.add(5);

		System.out.println("Elementos em ordem de prioridade:");
		while(!minHeap.isEmpty()) {
			System.out.print(minHeap.poll() + " ");
		}
		System.out.println();

		 // Criando um max-heap usando um comparador reverso
		PriorityQueue<Integer> maxHeap = new PriorityQueue<>((a, b) -> b - a);
		maxHeap.add(30); 
		maxHeap.add(10); 
		maxHeap.add(20); 
		maxHeap.add(5);

		// O maior elemento sempre é o próximo a sair
		System.out.println("Elementos em ordem decrescente de prioridade:"); 
		while (!maxHeap.isEmpty()) { 
			System.out.print(maxHeap.poll() + " "); 
		}
	}
}
```

**Best used when**
When you need to process elements in priority order.