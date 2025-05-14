HashMap implements the Map interface and stores data in key-value pairs, allowing quick access to values through their keys.
HashMaps offers O(1) constant-time access for basic operations like get and put, making it ideal for situations where access speed is important.

**Example:**
```java
import java.util.HashMap;
import java.util.Map;

public class ExampleHashMap() {
	public static void main(String[] args) {
		HashMap<String, Integer> ages = new HashMap<>();

		ages.put("João", 25);
		ages.put("Maria", 30);
		ages.put("Pedro", 35);

		System.out.println("Idade de Maria: " + ages.get("Maria"));
		System.out.println("Contém Carlos? " + ages.containsKey("Carlos"));
		System.out.println("Alguém tem 35 anos ? " + ages.containsValue(35));

		ages.remove("Pedro");

		for (Map.Entry<String, Integer> entrance : ages.entrySet()) {
			System.out.println(entrances.getKey() + ": " + entrances.getValue());
		}
	}
}
```

#### Best used when
 For fast key-based look. It is ideal for situations where access speed is important. More common in databases, caches, frequency counts. 