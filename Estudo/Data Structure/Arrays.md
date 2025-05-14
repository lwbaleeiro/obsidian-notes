Arrays are the most basic data structures, consisting of elements of the same type stored in contiguous memory locations.
Arrays have a fixed size after creation, which can be a limitation when working with dynamic datasets.

**Example:**
```java

int[] num = new int[5];
num[0] = 10;
num[1] = 20;

Strings[] names = {"Ana", "Bruno", "Carlos"};

for (int i = 0; i < names.length; i++){
	System.out.println(names[i]);
}

for (String name : names) {
	System.out.println(name);
}
```

#### Best used when
When you know the exact size of the data and need fast access by index.

## ArrayList

ArrayList is a resizable list implementation. Its is part of the Java collections library and offers more flexibility than regular arrays.

```java
import java.util.ArrayList;

public class ExemploArrayList {
	public static void main(String[] args) {
		ArrayList<String> fruits = new ArrayList<>();

		fruits.add("Apple");
		fruits.add("Orange");
		fruits.add("Banana");

		System.out.println("Second fruit: " + fruits.get(1));

		fruits.set(0, "Pear");
		fruits.remove("Orange");
		
		System.out.println("Toral of fruits: " + fruits.size());

		for (String fruit : fruits) {
			System.out.println(fruit);
		}

		System.out.println("Have Bananas? " + fruits.contains("Banana"));
	}
}
```

#### Best used when
When you need a dynamic list with fast access by index.