Hashset implements the Set interface, not allowing duplicate elements and not guaranteeing the order of the elements. Is useful when we need to store a set of elements without duplicates and the order does not matter.

**Example**
```java
import java.util.HashSet;

public class ExampleHashSet {
	public static void main(String[] args) {
		HashSet<String> colors = new HashSet<>();

		colors.add("Red");
		colors.add("Green");
		colors.add("Blue");

		boolean added = cores.add("Green");
		System.out.println("Added duplicated element? " + added);
		System.out.println("Total of colors: " + colors.size());
		System.out.println("Has Green? ": colors.contains("Green"));

		colors.remove("Blue");

		for (String color: colors) {
			System.out.println(color);
		}
	}
}
```

#### Best used when
When need to store unique values in no specific order.
