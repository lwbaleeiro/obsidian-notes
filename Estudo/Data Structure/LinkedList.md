LikedList is a doubly linked list implementation, where each element contains references to the previous and next element.
LinkedList is more efficient for frequent insertions and deletions, especially at the beginning of the list, while [[ArrayList]] is more efficient for random access.

**Example:**
```java
import java.util.LinkedList;
public class ExemploLinkedList {
	public static void main(String[] args) {
		LinkedList<Integer> numbers = new LinkedList<>();

		numbers.add(10);
		numbers.add(20);

		numbers.addFirst(5);
		numbers.addLast(30);

		System.out.println("First: " + numbers.getFirst());
		System.out.println("Last: " + numbers.getLast());

		numbers.removeFirst();
		numbers.removeLast();

		for (Integer number : numbers) {
			System.out.println(numero);
		}
	}
}
```

### Best used when
For frequent insertions and removals at the beginning or middle of the list.