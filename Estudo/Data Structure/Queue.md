Queue is an interface that represents a FIFO (First-In-First-Out) structure. A common implementation is LinkedList. Queues are useful in situations such as in-order processing of tasks, messaging systems, and breadth-first search algorithms.

**Example:**
```java
import java.util.LinkedList;
import java.util.Queue;

public class ExampleQueue {
	public static void main(String[] args) {
		Queue<String> queue = new LinkedList<>();

		queue.add("Client 1");
		queue.add("Client 2");
		queue.add("Client 3");

		System.out.println("Next client: " + queue.peek());
		String clientAttend = queue.poll();
		System.out.println("Client attend: " + clientAttend);
		System.out.println("Client in queue: " + queue.size());

		for (String client : queue) {
			System.out.println(client);
		}		
	}
}
```

#### Best used when
To process data in FIFO (First-In-First-Out) order.