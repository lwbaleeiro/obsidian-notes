Stack is a LIFO (Last-in-First-Out) structure where elements are added and removed from the same side. Stacks are useful in algorithms such as parathesis validation, expression evaluation, and history navigation.

**Example:**
```java
import java.util.Stack;

public class ExampleStack{
	public static void main(String[] args) {
		Stack<String> books = new Stack<>();

		books.push("Harry Potter");
		books.push("Lord of the Rings");
		books.push("Percy Jackson");

		System.out.println("Books on top: " + books.peek());

		String removedBook = books.pop();
		System.out.println("Removed book: " + removedBook);
		System.out.println("Empty Stack? " + books.isEmpty());
		System.out.println("Books size: " + books.size());
	}
}
```

#### Best used when
To process data in LIFO (Last-in-First-Out) order.