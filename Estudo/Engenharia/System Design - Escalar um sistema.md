
Artigo baseado do video: [Como escalar um sistema pra 1 milhão de usuários](https://www.youtube.com/watch?v=epp1YdODUk4&ab_channel=JonathanMoura)

### Infraestrutura Inicial

* O serviço começa com o usuário acessando via web browser/mobile app via DNS -> onde é retornado o IP para o browser ->  o browser encaminha a chamada para esse IP -> vai para o web server -> o web server retornar o HTML para o usuário.

![[01-system-design.png]]

* Para lidar com muitos usuários, são adicionados múltiplos web servers e um load balancer para distribuir o tráfego.
	* O load balancer é adicionado para que ele saiba quais serviços e para onde encaminhar as chamadas. Caso um servidor caia ele faz o encaminhamento automatico para o proximo. Com isso é tirado o acesso direito ao Web Servers do usuário, e deixa apenas o public IP do Load Balancer, que vai ser encarregado de chamar o IP privado dos servidores.

![[02-system-design.png]]

* Para o banco de dados, podemos adicionar um método chamado **Master and Slave**.
	* Onde o banco Master irá receber os **writes**, e os Slaves os **reads**. O porque dessa condição? R: Se temos vários web servers acessando e/ou alterando o mesmo record, poderia acabar sobrepondo algum registro.
	* Caso o **Master** caia, um **Slave** é elegido como mestre.

![[03-system-design.png]]

*(A aplicação ficaria assim.)*
![[04-system-design.png]]

* Como melhorar a performance da aplicação:
	* Vamos passar a utilizar um banco para cache.
	* Caso o dado exista no cache, leia do cache, caso não existe, busca no banco de dados e salva no cache.
	
	 ![[05-system-design.png]]
	* **CDN:** Implementa-se uma CDN (Content Delivery Network) para armazenar conteúdo estático (como imagens, por exemplo.) mais perto do usuário, melorando os tempos de carregamento.
	* É basicamente a mesma coisa que um cache, ele busca a imagem no CDN, caso não houver, ele busca no server e armazena no CDN, que retorna para o usuário.
	* É importante no CDN considerar os custos, como por exemplo quando esses dados irão expirar
	 ![[07-system-design.png]]

* *(Assim ficaria a aplicação).*
	 ![[06-system-design.png]]

* **Stateless Web Tier**: Para escalar ainda mais, o estado do usuário é removido dos servidores web e armazenado em um "shared storage", como um banco de dados NoSQL.

	 ![[08-system-design.png]]
	
* Ficando assim nossa aplicação:
  ![[09-system-design.png]]

* **Múltiplos Data Centers**: Para melhorar a latência e a disponibilidade, são adicionados múltiplos data centers, como o tráfego sendo direcionado para o data center mais próximo do usuário (pode ser feito direto no código da aplicação via Geo-Rounted), diminuindo a latencia. Caso um dos servidores caia, é feito o redirecionamento de Web Servers.

	![[10-system-design.png]]

* **Desacoplamento - Message Queue**: Para desacoplar os serviços, é utilizada uma message queue (Kafka, RabbitMQ...), permitindo que o sistema seja separado em micro serviços, e cada parte diferente do sistema se comuniquem de forma assíncrona.
	* Porque isso é bom? Caso haja uma demanta alta desse sistema, podemos adicionar mais producers e consumers conforme a demanda. Também é uma camada a mais de segurança, pois caso um serviço atrelado ao consumer caia, as requisições irão ficar pendentes de processo, e ao voltar não tera perca.

* **Monitoramento e segurança**: É crucual monitorar o sistema com logs e métricas, além de implementar pipelines de CI/CD para garantir a segurançar e previnir problemas.

	![[11-system-design.png]]

* **Sharding Banco de Dados**: Para lidar com grandes volumes de dados, o banco de dados é dividido em shards, distribuindo os dados entre múltiplos servidores.
	* **Vertical Scaling** é o incremento de CPU, RAM, Armazenamento e etc..
	* **Horizontal Scaling** é a adição de novos servidores.
	* Como o Sharding funciona? Os dados são dividios entre banco de dados diferentes, porém que tem a mesma estrutura *Ex: É mais facil encontrar um usuário buscando em um banco com 100 record, do que em um com 10000*.
	
![[12-system-design.png]]

### Considerações finais

Há muitos outros aspectos a serem considerados em um sistema real, como recharging, escolha de tecnologias específicas, e funcionamento detalhado do load balancer e etc, esse é apenas um exemplo de um escopo simples de como escalonar um sistema generico.