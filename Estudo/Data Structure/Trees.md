Trees are hierarchical structures with a root node and child nodes. Threes are efficient structures for searching, inserting and removing data, specially when kept balanced.

**Example:**
```java
class Node {
    int valor;
    Node esquerda;
    Node direita;
    
    public Node(int valor) {
        this.valor = valor;
        this.esquerda = null;
        this.direita = null;
    }
}

public class ArvoreBinariaBusca {
    Node raiz;
    
    public ArvoreBinariaBusca() {
        this.raiz = null;
    }
    
    // Método para inserir um valor
    public void inserir(int valor) {
        raiz = inserirRecursivo(raiz, valor);
    }
    
    private Node inserirRecursivo(Node raiz, int valor) {
        // Se a árvore estiver vazia, cria um novo nó
        if (raiz == null) {
            raiz = new Node(valor);
            return raiz;
        }
        
        // Caso contrário, percorre a árvore
        if (valor < raiz.valor) {
            raiz.esquerda = inserirRecursivo(raiz.esquerda, valor);
        } else if (valor > raiz.valor) {
            raiz.direita = inserirRecursivo(raiz.direita, valor);
        }
        
        return raiz;
    }
    
    // Método para buscar um valor
    public boolean buscar(int valor) {
        return buscarRecursivo(raiz, valor);
    }
    
    private boolean buscarRecursivo(Node raiz, int valor) {
        // Caso base: árvore vazia ou valor encontrado
        if (raiz == null) {
            return false;
        }
        if (raiz.valor == valor) {
            return true;
        }
        
        // Busca à esquerda se o valor for menor
        if (valor < raiz.valor) {
            return buscarRecursivo(raiz.esquerda, valor);
        }
        
        // Busca à direita se o valor for maior
        return buscarRecursivo(raiz.direita, valor);
    }
    
    // Percurso em ordem (inorder traversal)
    public void percursoEmOrdem() {
        percursoEmOrdemRecursivo(raiz);
    }
    
    private void percursoEmOrdemRecursivo(Node raiz) {
        if (raiz != null) {
            percursoEmOrdemRecursivo(raiz.esquerda);
            System.out.print(raiz.valor + " ");
            percursoEmOrdemRecursivo(raiz.direita);
        }
    }
    
    public static void main(String[] args) {
        ArvoreBinariaBusca arvore = new ArvoreBinariaBusca();
        
        // Inserindo valores
        arvore.inserir(50);
        arvore.inserir(30);
        arvore.inserir(70);
        arvore.inserir(20);
        arvore.inserir(40);
        arvore.inserir(60);
        arvore.inserir(80);
        
        // Percurso em ordem (inorder)
        System.out.println("Percurso em ordem:");
        arvore.percursoEmOrdem();
        System.out.println();
        
        // Buscando valores
        System.out.println("40 está na árvore? " + arvore.buscar(40));
        System.out.println("90 está na árvore? " + arvore.buscar(90));
    }
}
```

#### Best used when
Use trees to represent hierarchies and perform efficient searches.