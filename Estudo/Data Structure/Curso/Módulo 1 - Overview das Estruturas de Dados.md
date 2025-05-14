## Resumo das estruturas de dados mais importantes

**Array**: 
Espaço contíguo na memória onde itens estão inseridos. 
ex: [0, 3, 4, 5, 7, 1]
* Acesso por índice: Rápido, O(1), porque você vai direto à posição correta.
* Inserir ou remover no meio: O(n), porque você precisa deslocar os itens para abrir espaço ou preencher o vazio. Talvez seja necessário mover o array inteiro dependendo da disposição da memória

**Hashmap**: 
Dicionário, armazena conjunto chave/valor.
* Inserir, remover ou buscar um item: Geralmente muito rápido, O(1), porque você vai direto ao compartimento certo. Mas no pior caso, pode ser O(n) se muitos itens forem para o mesmo compartimento (colisões).

**Linked List (Lista Ligada):**
Cada vagão nó carrega um item e sabe quem é o próximo nó. Para percorrer os itens, você começa na "head" e vai percorrendo de nó em nó. 
* Inserir ou remover no início: Muito rápido, O(1). Só inserir o novo item e alterar o ponteiro de "head" ou "tail".
* Acesso a um item específico: Lento, O(n), porque você precisa passar por cada nó até chegar ao que quer. 
* Inserir ou remover no meio ou no fim: Lento, O(n), porque você precisa percorrer a lista para chegar ao ponto desejado