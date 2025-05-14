### ✅ O que é o **Redis**?

O **Redis** é um **banco de dados em memória** que funciona como um **cache super rápido**. Ele é usado principalmente para:

- Armazenar dados temporários.
    
- Compartilhar dados entre diferentes partes de um sistema.
    
- Reduzir o tempo de resposta de aplicações.
    

Redis trabalha com estruturas simples como:

- **Strings**
    
- **Listas**
    
- **Mapas (hashes)**
    
- **Conjuntos**
    
- **Contadores**

### 💡 Exemplo simples de uso com Java

Vamos fazer um exemplo básico: armazenar e buscar uma chave no Redis usando Java com a biblioteca **Jedis**, que é um cliente popular para Redis.

#### 1. Adicione a dependência no `pom.xml` (se estiver usando Maven):
```xml
<dependency>
    <groupId>redis.clients</groupId>
    <artifactId>jedis</artifactId>
    <version>5.1.0</version>
</dependency>
```

#### 2. Código Java de exemplo:
```java
import redis.clients.jedis.Jedis;

public class RedisExample {
    public static void main(String[] args) {
        // Conectando ao Redis (localhost na porta padrão 6379)
        Jedis jedis = new Jedis("localhost", 6379);

        // Salvando uma chave e valor
        jedis.set("usuario:1", "João");

        // Recuperando o valor
        String nome = jedis.get("usuario:1");
        System.out.println("Nome do usuário: " + nome);

        // Fechando a conexão
        jedis.close();
    }
}
```

---

### 🔁 O que acontece aqui:

1. Conectamos ao Redis local.
    
2. Salvamos uma string com chave `usuario:1`.
    
3. Buscamos essa string e mostramos no console.

### 🚀 **Cenários ideais para usar Redis**

#### 1. **Cache de dados**

- Para evitar consultas repetidas em banco de dados lento (ex: PostgreSQL, MySQL).
    
- Exemplo: guardar resultados de consultas SQL frequentes.
    

#### 2. **Sessões de usuário**

- Armazenar sessões de login de forma rápida e temporária (em apps web ou APIs).
    
- Exemplo: guardar token de autenticação ou informações da sessão.
    

#### 3. **Filas e processamento assíncrono**

- Redis pode ser usado como uma fila leve para tarefas (usando listas ou pub/sub).
    
- Exemplo: enviar e-mails em background, processar uploads, etc.
    

#### 4. **Contadores e rankings**

- Contadores de acessos, curtidas, views, etc. com extrema performance.
    
- Exemplo: ranking em jogos, contagem de visitas por página.
    

#### 5. **Rate limiting (limitação de requisições)**

- Controlar quantas requisições um usuário pode fazer por segundo/minuto.
    
- Exemplo: API que limita 100 requisições por hora por usuário.
    

#### 6. **Compartilhar estado entre serviços**

- Em microsserviços, Redis pode guardar dados acessados por múltiplos serviços.
    
- Exemplo: um token temporário ou estado de uma transação.
    

---

### ⚠️ Quando **não** usar Redis

- Para **armazenamento persistente e relacional** (como um banco SQL tradicional).
    
- Quando os **dados não cabem na memória RAM** (Redis guarda tudo na RAM).
    
- Quando a **durabilidade é crítica** (Redis pode perder dados se não for configurado com persistência).