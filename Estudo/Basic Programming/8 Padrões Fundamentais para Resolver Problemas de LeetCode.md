## 1. **Sliding Window (Janela Deslizante):**

- Este padrão é usado para processar segmentos contínuos de dados, como substrings ou subarrays.
- É útil quando você precisa encontrar subconjuntos que atendam a uma determinada condição.
- **Complexidade temporal:** Geralmente O(n) em vez de O(n²).
- **Quando usar:** Problemas envolvendo subconjuntos contíguos, sequências, ou quando precisamos rastrear um subconjunto de elementos em um array/string.

**Exemplo otimizado:** Encontrar a substring mais longa com K caracteres únicos.

```java
public int longestSubstringWithKUniqueChars(String s, int k) {
    if (s == null || s.length() == 0 || k <= 0) return 0;
    
    int maxLength = 0;
    int start = 0;
    Map<Character, Integer> charFrequency = new HashMap<>();
    
    // Expandir a janela
    for (int end = 0; end < s.length(); end++) {
        char rightChar = s.charAt(end);
        charFrequency.put(rightChar, charFrequency.getOrDefault(rightChar, 0) + 1);
        
        // Contrair a janela até termos exatamente k caracteres únicos
        while (charFrequency.size() > k) {
            char leftChar = s.charAt(start);
            charFrequency.put(leftChar, charFrequency.get(leftChar) - 1);
            if (charFrequency.get(leftChar) == 0) {
                charFrequency.remove(leftChar);
            }
            start++;
        }
        
        // Atualizar o comprimento máximo quando tivermos exatamente k caracteres únicos
        if (charFrequency.size() == k) {
            maxLength = Math.max(maxLength, end - start + 1);
        }
    }
    
    return maxLength;
}
```

**Outro exemplo:** Encontrar a soma máxima de um subarray de tamanho k.

```java
public int maxSumSubarrayOfSizeK(int[] arr, int k) {
    int maxSum = 0;
    int windowSum = 0;
    int start = 0;
    
    for (int end = 0; end < arr.length; end++) {
        windowSum += arr[end]; // Adicionar o elemento atual
        
        // Quando atingimos o tamanho k, comparamos e deslizamos a janela
        if (end >= k - 1) {
            maxSum = Math.max(maxSum, windowSum);
            windowSum -= arr[start]; // Remover o elemento que sai da janela
            start++; // Deslizar a janela
        }
    }
    
    return maxSum;
}
```
## 2. **Subset (Subconjunto):**

- Este padrão é usado para gerar todas as combinações possíveis de elementos de um conjunto.
- Pode envolver ou não repetições, dependendo do problema.
- **Complexidade:** O(2ⁿ) para um conjunto de tamanho n, já que cada elemento pode estar dentro ou fora do subconjunto.
- **Quando usar:** Problemas de combinação, permutação ou qualquer tipo de problema que exija explorar todas as possibilidades.

**Exemplo:** Gerar todos os subconjuntos de um conjunto.

```java
public List<List<Integer>> subsets(int[] nums) {
    List<List<Integer>> result = new ArrayList<>();
    result.add(new ArrayList<>()); // Adicionar o conjunto vazio
    
    for (int num : nums) {
        int size = result.size();
        // Para cada subconjunto existente, criar um novo com o elemento atual
        for (int i = 0; i < size; i++) {
            List<Integer> newSubset = new ArrayList<>(result.get(i));
            newSubset.add(num);
            result.add(newSubset);
        }
    }
    
    return result;
}
```

Exemplo de permutações:

```java
public List<List<Integer>> permute(int[] nums) {
    List<List<Integer>> result = new ArrayList<>();
    backtrack(nums, new ArrayList<>(), result);
    return result;
}

private void backtrack(int[] nums, List<Integer> current, List<List<Integer>> result) {
    // Se o tamanho atual é igual ao comprimento do array, temos uma permutação completa
    if (current.size() == nums.length) {
        result.add(new ArrayList<>(current));
        return;
    }
    
    for (int i = 0; i < nums.length; i++) {
        // Pular se o elemento já está na permutação atual
        if (current.contains(nums[i])) continue;
        
        // Incluir o elemento
        current.add(nums[i]);
        
        // Recursivamente gerar permutações para os elementos restantes
        backtrack(nums, current, result);
        
        // Remover o elemento para backtracking
        current.remove(current.size() - 1);
    }
}
```

## 3. **Modified Binary Search (Busca Binária Modificada):**

- Baseia-se na ideia de dividir o espaço de busca pela metade repetidamente.
- Requer ajustes na lógica padrão para se adequar a problemas específicos.
- **Complexidade:** O(log n) para efetuar a busca em um array ordenado.
- **Quando usar:** Problemas que envolvem arrays ordenados ou parcialmente ordenados.

**Exemplo (busca em array rotacionado):**

```java
public int searchRotatedArray(int[] nums, int target) {
    int left = 0, right = nums.length - 1;
    
    while (left <= right) {
        int mid = left + (right - left) / 2;
        
        if (nums[mid] == target) return mid;
        
        // Verificar qual lado está ordenado
        if (nums[left] <= nums[mid]) { // Lado esquerdo está ordenado
            if (target >= nums[left] && target < nums[mid]) {
                right = mid - 1; // O alvo está na porção ordenada à esquerda
            } else {
                left = mid + 1; // O alvo está na porção à direita
            }
        } else { // Lado direito está ordenado
            if (target > nums[mid] && target <= nums[right]) {
                left = mid + 1; // O alvo está na porção ordenada à direita
            } else {
                right = mid - 1; // O alvo está na porção à esquerda
            }
        }
    }
    
    return -1; // Elemento não encontrado
}
```

**Outro exemplo:** Encontrar o primeiro e o último elemento em um array ordenado.

```java
public int[] searchRange(int[] nums, int target) {
    int[] result = {-1, -1};
    if (nums == null || nums.length == 0) return result;
    
    // Encontrar a primeira ocorrência
    int left = 0, right = nums.length - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] == target) {
            if (mid == 0 || nums[mid-1] != target) {
                result[0] = mid;
                break;
            }
            right = mid - 1;
        } else if (nums[mid] > target) {
            right = mid - 1;
        } else {
            left = mid + 1;
        }
    }
    
    // Se não encontrou a primeira ocorrência, o elemento não existe
    if (result[0] == -1) return result;
    
    // Encontrar a última ocorrência
    left = result[0];
    right = nums.length - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] == target) {
            if (mid == nums.length - 1 || nums[mid+1] != target) {
                result[1] = mid;
                break;
            }
            left = mid + 1;
        } else if (nums[mid] > target) {
            right = mid - 1;
        } else {
            left = mid + 1;
        }
    }
    
    return result;
}
```

## 4. **Top K Elements (K Elementos Principais):**

- Usado para selecionar os K elementos principais de um conjunto de dados, com base em uma condição específica.
- Comumente usado para encontrar elementos de maior ranking.
- **Complexidade:** O(n log k) com heap, ou O(n) com partition selection (QuickSelect).
- **Quando usar:** Problemas que pedem para encontrar os k maiores/menores elementos, ou os k elementos mais frequentes.

**Exemplo:** Encontrar os k elementos mais frequentes em um array.

```java
public int[] topKFrequent(int[] nums, int k) {
    // Criar mapa de frequência
    Map<Integer, Integer> frequencyMap = new HashMap<>();
    for (int num : nums) {
        frequencyMap.put(num, frequencyMap.getOrDefault(num, 0) + 1);
    }
    
    // Criar min heap baseado na frequência
    PriorityQueue<Integer> minHeap = new PriorityQueue<>(
        (a, b) -> frequencyMap.get(a) - frequencyMap.get(b)
    );
    
    // Adicionar elementos ao heap
    for (int num : frequencyMap.keySet()) {
        minHeap.add(num);
        // Se o heap exceder k, remover o elemento com menor frequência
        if (minHeap.size() > k) {
            minHeap.poll();
        }
    }
    
    // Construir o resultado
    int[] result = new int[k];
    for (int i = k - 1; i >= 0; i--) {
        result[i] = minHeap.poll();
    }
    
    return result;
}
```

**Exemplo com QuickSelect:** Encontrar o k-ésimo maior elemento.

```java
public int findKthLargest(int[] nums, int k) {
    return quickSelect(nums, 0, nums.length - 1, nums.length - k);
}

private int quickSelect(int[] nums, int start, int end, int k) {
    if (start == end) return nums[start];
    
    int pivotIndex = partition(nums, start, end);
    
    if (pivotIndex == k) return nums[k];
    else if (pivotIndex < k) return quickSelect(nums, pivotIndex + 1, end, k);
    else return quickSelect(nums, start, pivotIndex - 1, k);
}

private int partition(int[] nums, int start, int end) {
    int pivot = nums[end];
    int i = start;
    
    for (int j = start; j < end; j++) {
        if (nums[j] <= pivot) {
            swap(nums, i, j);
            i++;
        }
    }
    
    swap(nums, i, end);
    return i;
}

private void swap(int[] nums, int i, int j) {
    int temp = nums[i];
    nums[i] = nums[j];
    nums[j] = temp;
}
```
## 5. **Depth-First Search (DFS) para Binary Tree (Busca em Profundidade):**

- Permite visitar todos os nós de uma árvore, focando em um ramo por vez.
- Geralmente implementado usando recursão.
- **Complexidade:** O(n) onde n é o número de nós na árvore.
- **Quando usar:** Problemas que envolvem árvores ou grafos, especialmente quando precisamos explorar até o fim de um caminho antes de retroceder.

**Exemplo (profundidade máxima):**

```java
public int maxDepth(TreeNode root) {
    if (root == null) return 0;
    
    int leftDepth = maxDepth(root.left);
    int rightDepth = maxDepth(root.right);
    
    return Math.max(leftDepth, rightDepth) + 1;
}
```

Exemplo de travessias DFS:

```java
// Pré-ordem (raiz, esquerda, direita)
public List<Integer> preorderTraversal(TreeNode root) {
    List<Integer> result = new ArrayList<>();
    preorderHelper(root, result);
    return result;
}

private void preorderHelper(TreeNode node, List<Integer> result) {
    if (node == null) return;
    
    result.add(node.val);           // Visitar a raiz
    preorderHelper(node.left, result);  // Visitar a subárvore esquerda
    preorderHelper(node.right, result); // Visitar a subárvore direita
}

// In-ordem (esquerda, raiz, direita)
public List<Integer> inorderTraversal(TreeNode root) {
    List<Integer> result = new ArrayList<>();
    inorderHelper(root, result);
    return result;
}

private void inorderHelper(TreeNode node, List<Integer> result) {
    if (node == null) return;
    
    inorderHelper(node.left, result);   // Visitar a subárvore esquerda
    result.add(node.val);            // Visitar a raiz
    inorderHelper(node.right, result);  // Visitar a subárvore direita
}

// Pós-ordem (esquerda, direita, raiz)
public List<Integer> postorderTraversal(TreeNode root) {
    List<Integer> result = new ArrayList<>();
    postorderHelper(root, result);
    return result;
}

private void postorderHelper(TreeNode node, List<Integer> result) {
    if (node == null) return;
    
    postorderHelper(node.left, result);  // Visitar a subárvore esquerda
    postorderHelper(node.right, result); // Visitar a subárvore direita
    result.add(node.val);             // Visitar a raiz
}
```

## 6. **Topological Sort (Ordenação Topológica):**

- Usado para ordenar elementos com dependências entre si.
- Particularmente útil para grafos acíclicos direcionados (DAGs).
- **Complexidade:** O(V + E) onde V é o número de vértices e E é o número de arestas.
- **Quando usar:** Problemas que envolvem dependências ou pré-requisitos.

**Exemplo:** Ordenar tarefas com dependências.

```java
public int[] findOrder(int numCourses, int[][] prerequisites) {
    // Construir grafo
    List<List<Integer>> graph = new ArrayList<>();
    for (int i = 0; i < numCourses; i++) {
        graph.add(new ArrayList<>());
    }
    
    int[] inDegree = new int[numCourses];
    for (int[] prereq : prerequisites) {
        graph.get(prereq[1]).add(prereq[0]);
        inDegree[prereq[0]]++;
    }
    
    // BFS para ordenação topológica
    Queue<Integer> queue = new LinkedList<>();
    for (int i = 0; i < numCourses; i++) {
        if (inDegree[i] == 0) {
            queue.offer(i);
        }
    }
    
    int[] result = new int[numCourses];
    int index = 0;
    
    while (!queue.isEmpty()) {
        int current = queue.poll();
        result[index++] = current;
        
        for (int neighbor : graph.get(current)) {
            if (--inDegree[neighbor] == 0) {
                queue.offer(neighbor);
            }
        }
    }
    
    // Se nem todos os cursos foram incluídos, existe um ciclo
    return index == numCourses ? result : new int[0];
}
```

Implementação alternativa usando DFS:

```java
public int[] findOrder(int numCourses, int[][] prerequisites) {
    // Construir grafo
    List<List<Integer>> graph = new ArrayList<>();
    for (int i = 0; i < numCourses; i++) {
        graph.add(new ArrayList<>());
    }
    
    for (int[] prereq : prerequisites) {
        graph.get(prereq[1]).add(prereq[0]);
    }
    
    // 0: não visitado, 1: em processamento, 2: processado
    int[] visited = new int[numCourses];
    List<Integer> result = new ArrayList<>();
    
    for (int i = 0; i < numCourses; i++) {
        if (visited[i] == 0 && hasCycle(graph, i, visited, result)) {
            return new int[0]; // Ciclo detectado
        }
    }
    
    // Converter para array e inverter
    int[] order = new int[numCourses];
    for (int i = 0; i < numCourses; i++) {
        order[i] = result.get(numCourses - i - 1);
    }
    
    return order;
}

private boolean hasCycle(List<List<Integer>> graph, int node, int[] visited, List<Integer> result) {
    if (visited[node] == 1) return true;  // Ciclo detectado
    if (visited[node] == 2) return false; // Já processado
    
    visited[node] = 1; // Marcar como em processamento
    
    for (int neighbor : graph.get(node)) {
        if (hasCycle(graph, neighbor, visited, result)) {
            return true;
        }
    }
    
    visited[node] = 2; // Marcar como processado
    result.add(node);  // Adicionar ao resultado
    
    return false;
}
```

## 7. **Breadth-First Search (BFS) para Binary Tree (Busca em Largura):**

- Explora todos os nós no mesmo nível antes de passar para o próximo nível.
- Utiliza uma fila (Queue) para manter a ordem de visita.
- **Complexidade:** O(n) onde n é o número de nós na árvore.
- **Quando usar:** Problemas que exigem procesar nós por níveis, encontrar caminhos mais curtos ou mais próximos.

**Exemplo (Level Order Traversal):**

```java
public List<List<Integer>> levelOrder(TreeNode root) {
    List<List<Integer>> result = new ArrayList<>();
    if (root == null) return result;
    
    Queue<TreeNode> queue = new LinkedList<>();
    queue.offer(root);
    
    while (!queue.isEmpty()) {
        int levelSize = queue.size();
        List<Integer> currentLevel = new ArrayList<>();
        
        for (int i = 0; i < levelSize; i++) {
            TreeNode node = queue.poll();
            currentLevel.add(node.val);
            
            if (node.left != null) queue.offer(node.left);
            if (node.right != null) queue.offer(node.right);
        }
        
        result.add(currentLevel);
    }
    
    return result;
}
```

**Exemplo com grafos:** Encontrar o caminho mais curto em um grafo não ponderado.

```java
public int shortestPath(int[][] graph, int start, int end) {
    if (start == end) return 0;
    
    int n = graph.length;
    boolean[] visited = new boolean[n];
    Queue<Integer> queue = new LinkedList<>();
    queue.offer(start);
    visited[start] = true;
    
    int distance = 0;
    
    while (!queue.isEmpty()) {
        int size = queue.size();
        distance++;
        
        for (int i = 0; i < size; i++) {
            int current = queue.poll();
            
            for (int neighbor = 0; neighbor < n; neighbor++) {
                if (graph[current][neighbor] == 1 && !visited[neighbor]) {
                    if (neighbor == end) return distance;
                    
                    visited[neighbor] = true;
                    queue.offer(neighbor);
                }
            }
        }
    }
    
    return -1; // Não há caminho
}
```

## 8. **Two Pointers (Dois Ponteiros):**

- Usado para iterar através de um array ordenado de forma eficiente.
- Emprega dois ponteiros para rastrear índices diferentes no array.
- **Complexidade:** Geralmente O(n) em vez de O(n²).
- **Quando usar:** Problemas de busca em arrays ordenados, verificação de palindromas, e operações que podem se beneficiar da exploração de dados a partir de extremidades opostas.

**Exemplo (Two Sum em array ordenado):**

```java
public int[] twoSumSorted(int[] nums, int target) {
    int left = 0, right = nums.length - 1;
    
    while (left < right) {
        int sum = nums[left] + nums[right];
        
        if (sum == target) {
            return new int[]{left, right};
        } else if (sum < target) {
            left++;  // Precisamos de um valor maior, então movemos o ponteiro esquerdo
        } else {
            right--; // Precisamos de um valor menor, então movemos o ponteiro direito
        }
    }
    
    return new int[]{-1, -1}; // Não encontrado
}
```

Exemplo de remoção de duplicatas em array ordenado:

```java
public int removeDuplicates(int[] nums) {
    if (nums.length == 0) return 0;
    
    int i = 0; // Ponteiro lento para elementos únicos
    
    // j é o ponteiro rápido para escanear o array
    for (int j = 1; j < nums.length; j++) {
        if (nums[j] != nums[i]) {
            i++;
            nums[i] = nums[j];
        }
    }
    
    return i + 1; // Comprimento do array após remover duplicatas
}
```

Exemplo de três ponteiros (3Sum):

```java
public List<List<Integer>> threeSum(int[] nums) {
    List<List<Integer>> result = new ArrayList<>();
    if (nums == null || nums.length < 3) return result;
    
    Arrays.sort(nums);
    
    for (int i = 0; i < nums.length - 2; i++) {
        // Evitar duplicatas para o primeiro número
        if (i > 0 && nums[i] == nums[i-1]) continue;
        
        int left = i + 1;
        int right = nums.length - 1;
        
        while (left < right) {
            int sum = nums[i] + nums[left] + nums[right];
            
            if (sum == 0) {
                result.add(Arrays.asList(nums[i], nums[left], nums[right]));
                
                // Evitar duplicatas para o segundo e terceiro números
                while (left < right && nums[left] == nums[left+1]) left++;
                while (left < right && nums[right] == nums[right-1]) right--;
                
                left++;
                right--;
            } else if (sum < 0) {
                left++;
            } else {
                right--;
            }
        }
    }
    
    return result;
}
```