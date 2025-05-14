### **1. Definição dos Requisitos**

#### **1.1 Requisitos Funcionais**

O sistema **EventHub** deve permitir que:

1. Os usuários possam **se cadastrar e autenticar**.
    
2. Os usuários possam **criar, visualizar, editar e excluir eventos**.
    
3. O sistema permita **buscar eventos** por palavras-chave usando **Trie**.
    
4. O sistema recomende eventos com base em preferências e interações, utilizando **Grafos**.
    
5. O sistema envie **notificações assíncronas** sobre eventos via **Kafka ou RabbitMQ**.
    

#### **1.2 Requisitos Não Funcionais**

1. O sistema deve ser **escalável**, utilizando **Docker e Kubernetes**.
    
2. O sistema deve ter **alta disponibilidade e ser tolerante a falhas**.
    
3. A autenticação deve ser segura, utilizando **JWT ou OAuth2**.
    
4. As respostas da API devem ser rápidas, garantindo uma **latência baixa** para buscas.

#### **2. Diagrama de Casos de Uso (UML)**

![[diagramas-caso-uml.png]]

#### **3. Diagrama de Classes (UML))**

![[diagramas-classe-uml.png]]

#### **4. Diagrama de Sequência (Exemplo: Fluxo de Busca de Evento)**
![[diagramas-busca-evento.png]]


#### **5. Fluxo de Dados (DFD - Nível 1)**

![[diagramas-fluxo-dados.png]]

#### **6. Estrutura do projeto**

```
eventhub/
│
├── pom.xml 
├── Dockerfile
├── docker-compose.yml
├── .env
├── README.md
│
└── src/
    ├── main/
    │   ├── java/
    │   │   └── com/eventhub/
    │   │       ├── EventHubApplication.java
    │   │       │
    │   │       ├── core/   # Núcleo de domínio
    │   │       │   ├── user/
    │   │       │   │   ├── model/
    │   │       │   │   │   └── User.java
    │   │       │   │   ├── port/
    │   │       │   │   │   ├── UserRepository.java
    │   │       │   │   └── usecase/
    │   │       │   │       └── UserManagementUseCase.java
	│	│		│	│	    └── UserManagementUseCaseImpl.java
    │   │       │   │
    │   │       │   ├── event/
    │   │       │   │   ├── model/
    │   │       │   │   │   ├── Event.java
    │   │       │   │   │   └── Category.java
    │   │       │   │   ├── port/
    │   │       │   │   │   ├── EventRepository.java
    │   │       │   │   └── usecase/
    │   │       │   │       └── EventManagementUseCase.java
    │   │       │   │       └── EventManagementUseCaseImpl.java    
    │   │       │   │
    │   │       │   ├── search/
    │   │       │   │   ├── model/
    │   │       │   │   │   └── TrieNode.java
    │   │       │   │   ├── port/
    │   │       │   │   │   └── SearchRepository.java
    │   │       │   │   └── usecase/
    │   │       │   │       └── EventSearchUseCase.java
    │   │       │   │       └── EventSearchUseCaseImpl.java
    │   │       │   │
    │   │       │   ├── recommendation/
    │   │       │   │   ├── model/
    │   │       │   │   │   └── UserEventGraph.java
    │   │       │   │   ├── port/
    │   │       │   │   │   └── RecommendationRepository.java
    │   │       │   │   └── usecase/
    │   │       │   │       └── PersonalizedRecommendationUseCase.java
    │   │       │   │       └── PersonalizedRecommendationUseCaseImpl.java    
    │   │       │   │
    │   │       │   └── notification/ 
    │   │       │       ├── model/
    │   │       │       │   ├── Notification.java
    │   │       │       │   └── NotificationType.java
    │   │       │       ├── port/
    │   │       │       │   ├── NotificationRepository.java
    │   │       │       └── usecase/
    │   │       │           └── NotificationManagementUseCase.java
    │   │       │           └── NotificationManagementUseCaseImpl.java    
    │   │       │
    │   │       ├── infrastructure/ # Implementações de infraestrutura
    │   │       │   ├── config/
    │   │       │   │   ├── SecurityConfig.java
    │   │       │   │   ├── MessagingConfig.java
    │   │       │   │   ├── OpenApiConfig.java
    │   │       │   │   └── PersistenceConfig.java
    │   │       │   │
    │   │       │   ├── persistence/
    │   │       │   │   ├── user/
    │   │       │   │   │   └── UserRepositoryImpl.java
    │   │       │   │   ├── event/
    │   │       │   │   │   └── EventRepositoryImpl.java
    │   │       │   │   ├── search/
    │   │       │   │   │   └── TrieSearchIndex.java
    │   │       │   │   └── notification/
    │   │       │   │       └── NotificationRepositoryImpl.java
    │   │       │   │
    │   │       │   ├── messaging/
    │   │       │   │   ├── kafka/
    │   │       │   │   │   ├── KafkaEventProducer.java
    │   │       │   │   │   └── KafkaEventListener.java
    │   │       │   │   └── notification/
    │   │       │   │       ├── NotificationProducer.java
    │   │       │   │       └── NotificationConsumer.java
    │   │       │   │
    │   │       │   └── web/ # Adaptadores de entrada (REST)
    │   │       │       ├── user/
    │   │       │       │   ├── UserController.java
    │   │       │       │   └── dto/
    │   │       │       │       ├── UserRegistrationDTO.java
    │   │       │       │       ├── UserLoginDTO.java
    │   │       │       │       ├── UserProfileDTO.java
    │   │       │       │       └── UserResponseDTO.java
    │   │       │       │
    │   │       │       ├── event/
    │   │       │       │   ├── EventController.java
    │   │       │       │   └── dto/
    │   │       │       │       ├── EventCreationDTO.java 
    │   │       │       │       ├── EventUpdateDTO.java
    │   │       │       │       └── EventResponseDTO.java
    │   │       │       │
    │   │       │       ├── search/
    │   │       │       │   ├── SearchController.java
    │   │       │       │   └── dto/
    │   │       │       │       ├── SearchRequestDTO.java
    │   │       │       │       └── SearchResultDTO.java
    │   │       │       │
    │   │       │       ├── recommendation/
    │   │       │       │   ├── RecommendationController.java
    │   │       │       │   └── dto/
    │   │       │       │       └── RecommendationResponseDTO.java
    │   │       │       │
    │   │       │       └── notification/
    │   │       │           ├── NotificationController.java
    │   │       │           └── dto/ # DTOs específicos para notification
    │   │       │               ├── NotificationDTO.java
    │   │       │               └── NotificationPreferenceDTO.java
    │   │       │
    │   │       └── common/   # Componentes compartilhados
    │   │           ├── dto/  # DTOs compartilhados/genéricos
    │   │           │   ├── PageRequestDTO.java
    │   │           │   ├── PageResponseDTO.java
    │   │           │   └── ErrorResponseDTO.java
    │   │           │
    │   │           ├── exception/  # Exceções customizadas
    │   │           │   ├── BusinessException.java
    │   │           │   ├── ResourceNotFoundException.java
    │   │           │   ├── ValidationException.java
    │   │           │   └── handler/
    │   │           │       └── GlobalExceptionHandler.java
    │   │           │
    │   │           └── util/        # Utilitários
    │   │               ├── ValidationUtils.java
    │   │               ├── SecurityUtils.java
    │   │               └── DateTimeUtils.java
    │   │
    │   └── resources/
    │       ├── application.yml     # Usando YAML para configuração
    │       ├── db/
    │       │   └── migration/      # Migrações de banco de dados
    │       ├── static/             # Recursos estáticos
    │       └── logback-spring.xml  # Configuração de logs
    │
    └── test/                       # Testes automatizados
        └── java/
            └── com/eventhub/
                ├── core/    # Testes unitários para o core
                │   ├── user/
                │   ├── event/
                │   ├── search/
                │   ├── recommendation/
                │   └── notification/
                │
                ├── infrastructure/     # Testes de infraestrutura
                │   ├── persistence/
                │   ├── messaging/
                │   └── web/
                │
                └── integration/    # Testes de integração
                    ├── UserIntegrationTest.java
                    ├── EventIntegrationTest.java
                    └── SearchIntegrationTest.java
```

**Explicação da Estrutura:**
A  estrutura segue o padrão de Arquitetura Hexagonal (Ports and Adapters), que promove:

- **Desacoplamento**: Separação clara entre regras de negócio e implementações técnicas
- **Testabilidade**: Facilita testes unitários e de integração
- **Flexibilidade**: Permite mudanças de infraestrutura sem impactar o núcleo do domínio
### 2. Estrutura de Pacotes

#### `core/`

- Contém o modelo de domínio e as regras de negócio
- Pacotes:
    - `model/`: Entidades de domínio puras
    - `port/`: Interfaces para repositórios e serviços
    - `usecase/`: Casos de uso que orquestram a lógica de negócio
#### `infrastructure/`

- Implementações concretas de interfaces do núcleo
- Pacotes:
    - `config/`: Configurações de framework
    - `persistence/`: Implementações de repositórios
    - `messaging/`: Processamento de eventos e mensageria
    - `web/`: Controladores e adaptadores REST
#### `common/`

- Componentes compartilhados entre módulos
- DTOs, exceções customizadas, utilitários
### 3. Benefícios da Estrutura

- **Baixo Acoplamento**: Módulos independentes
- **Alta Coesão**: Cada pacote tem responsabilidade única
- **Evolução para Microserviços**: Fácil separação futura
- **Manutenibilidade**: Código organizado e modular

## Recomendações Técnicas

### Dependências

- Spring Boot como framework principal
- Hibernate/JPA para persistência
- Kafka para mensageria
- Springdoc OpenAPI para documentação
- Testcontainers para testes de integração

### Práticas de Implementação

- Usar interfaces para definir contratos
- Implementar validações no nível de domínio
- Utilizar DTOs para transferência de dados
- Implementar tratamento de exceções centralizado

## Estruturas de Dados Customizadas

### Trie para Busca de Eventos

- Implementar `TrieSearchIndex` no pacote `infrastructure/search/`
- Método de busca eficiente para palavras-chave de eventos

### Grafo para Recomendações

- Classe `UserEventGraph` no pacote `core/recommendation/model/`
- Modelar conexões entre usuários e eventos
- Algoritmos de recomendação baseados em grafos

## Considerações Adicionais

1. Configurar `.env` para gerenciar configurações sensíveis
2. Usar `docker-compose.yml` para ambiente de desenvolvimento
3. Implementar migração de banco de dados com Flyway
4. Configurar logs estruturados com Logback