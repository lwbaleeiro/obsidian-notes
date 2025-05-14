### What it is:
GraphQL is a query language to retrieve data from a server. It is an alternative to REST, SOAP, or gRPC

GraphQL é uma forma moderna de se comunicar com um servidor para buscar ou enviar dados. Diferente das APIs tradicionais (como REST), com GraphQL você pode pedir exatamente as informações que precisa — nada a mais, nada a menos — tudo em uma única requisição. Isso torna o processo mais rápido e eficiente.

### Cenário:

Suponha que você tem uma aplicação que gerencia **livros** e quer buscar apenas o **título** e o **autor** dos livros (sem precisar de todas as informações como número de páginas, data de publicação etc.).


1. **Schema GraphQL (resources/schema.graphqls)**
```java
type Book {
  id: ID
  title: String
  author: String
}

type Query {
  books: [Book]
}

```

2. **Model e Service (Java):**
```java
public class Book {
  private String id;
  private String title;
  private String author;

  // Construtores, getters e setters
}
```

```java
@Service
public class BookService {
  public List<Book> getAllBooks() {
    return List.of(
      new Book("1", "Dom Casmurro", "Machado de Assis"),
      new Book("2", "1984", "George Orwell")
    );
  }
}
```

3. **Resolver**
```java
@Component
public class BookResolver implements GraphQLQueryResolver {
  private final BookService bookService;

  public BookResolver(BookService bookService) {
    this.bookService = bookService;
  }

  public List<Book> books() {
    return bookService.getAllBooks();
  }
}

```


Inicialize a aplicação, e vá em:  [http://localhost:8080/graphiql](http://localhost:8080/graphiql)

Chame o endpoint através da aplicação com a query:
```json
query {
  books {
    title
    author
  }
}
```
Você receberá o que pediu:
```json
{
  "data": {
    "books": [
      {
        "title": "Dom Casmurro",
        "author": "Machado de Assis"
      },
      {
        "title": "1984",
        "author": "George Orwell"
      }
    ]
  }
}
```

Esse é um exemplo básico de como GraphQL funciona: você define o que quer e recebe só aquilo.
DOC:
https://spring.io/guides/gs/graphql-server

--------

### ✅ **1. Precisa buscar só os dados necessários**

Com GraphQL, o cliente escolhe exatamente quais campos quer receber — isso evita tráfego desnecessário.  
👉 _Exemplo:_ um app mobile que só precisa do nome do usuário, e não de todos os dados.

### ✅ **2. Tem muitas fontes de dados ou microserviços**

GraphQL pode unificar dados de várias fontes diferentes em uma única API.  
👉 _Exemplo:_ buscar perfil do usuário (em um serviço) e pedidos recentes (em outro), numa só requisição.

### ✅ **3. Requisições muito variadas ou dinâmicas**

Se os clientes precisam de combinações diferentes de dados em diferentes telas, GraphQL é ideal.  
👉 _Exemplo:_ um dashboard que exibe partes diferentes para cada tipo de usuário.

### ✅ **4. Deseja menos requisições HTTP**

GraphQL permite pedir tudo o que você precisa em **uma única chamada**, ao contrário do REST que pode exigir várias.

### ⚠️ **Quando evitar GraphQL?**

- Se sua API é simples e bem definida, com poucas mudanças ou endpoints, **REST pode ser mais direto**.
    
- Se você precisa de **caching HTTP padrão** (GraphQL não lida tão bem com isso sem ajuda extra).
    
- Para **uploads de arquivos**, REST ainda é mais prático.