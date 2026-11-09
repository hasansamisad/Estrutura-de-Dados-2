# Revisão de estrutura de árvores (Atividade individual remota para o dia 28/09)

**Nome:** Hasan Sami Sad
**Turma:** D1
**Disciplina:** Estrutura de Dados II — **Professora:** Profa. Kadidja Valéria  
**Modalidade:** individual, remota e assíncrona

---

## Etapa 1 — Revisão bibliográfica (resumo)

**Conceitos básicos.** O nó (ou vértice) é a unidade de armazenamento da arvore que contem os dados (chave e valor) e os ponteiros de referência para seus nós filhos, cada elemento da árvore é um nó. A raiz é o nó inicial, que não possui pais, ou seja, não possui arestas chegando a ele. Um nó pai é aquele que a partir dele se referencia para outro nó, ja o nó filho é aquele que é referenciado por alguém, que é o nó pai. A folha é o nó que não possui filhos, são os ultimos elementos da arvore. A altura é o comprimenento do caminho mais longo da raiz até qualquer folha. O percurso é a sequencia de nós e arestas que conectam a raiz a um nó especifico

**Árvore geral e árvore binária.** Na árvore geral, cada nó pode ter qualquer número de filhos. Na árvore binária, cada nó tem no máximo dois (esquerdo e direito).

**BST.** Possui uma organização hierarquica a partir da raiz, onde os valores menor são inseridos a esquerda e os valores maiores são inseridos a direita. Essa propiedade permite realizar buscas, inserções e remoções em um tempo médio de O(log n) que é excelente.

**AVL.** É uma ABB que mantém, em todo nó, a diferença de altura entre as subárvores esquerda e direita (fator de balanceamento) em {-1, 0, 1}. Após inserir ou remover, o fator é recalculado no caminho de volta e, se algum nó violar a regra, aplicam-se rotações simples ou duplas. A altura fica em O(log n).

**- Rubro-negra.** A Árvore Rubro-Negra é uma árvore binária de busca auto-balanceável (assim como a AVL), mas em vez de guardar a altura nos nós, ela guarda uma cor (Vermelho ou Preto) e segue 5 regras rígidas para se manter balanceada:

- Regra da Cor: Todo nó é Vermelho ou Preto.

- Regra da Raiz:A raiz é sempre Preta.

- Regra das Folhas: Todas as folhas nulas (NIL / ponteiros vazios) são consideradas Pretas.

- Regra dos Vermelhos (Sem Vermelhos Consecutivos): Se um nó é Vermelho, seus filhos devem ser Pretos (não pode haver pai e filho vermelhos).

- Regra da Altura-Preta: Todo caminho da raiz até qualquer folha nula possui o mesmo número de nós pretos.

**Árvore B.** A Árvore B é uma árvore multi-caminho (não é binária) projetada para trabalhar com grandes volumes de dados armazenados em disco rígido (HD/SSD).

- Múltiplas Chaves por Nó: Ao contrário das árvores binárias onde cada nó tem apenas 1 chave e 2 filhos, um nó na Árvore B de ordem $M$ pode guardar várias chaves e ter até $M$ filhos.

- Dados nos Nós Internos: Os dados/ponteiros para os registros ficam armazenados tanto nos nós internos quanto nas folhas.

- Todas as Folhas no Mesmo Nível: A Árvore B cresce "de baixo para cima". Todas as folhas estão exatamente na mesma profundidade, garantindo um balanceamento perfeito.

- Propósito: Minimizar o número de leituras de bloco no disco (operações de I/O).

**Árvore B+.** (Suas 2 diferenças com a arvore B)

**1-Separação de Índices e Dados:**

- Os nós internos guardam apenas chaves de navegação/índices (sem os dados reais).

- TODOS os dados reais e apontadores para os registros ficam exclusivamente nas folhas.

**2- Folhas Encadeadas:**

- As folhas são conectadas entre si por uma lista encadeada simples ou dupla.

- Isso torna buscas por intervalo (range queries, como WHERE idade BETWEEN 20 AND 30) incrivelmente rápidas: o algoritmo faz a busca binária até a primeira folha e depois apenas percorre a lista encadeada para o lado, sem precisar voltar para a raiz.

## Etapa 2 — Quadro comparativo

| Estrutura                     | Organização dos dados                                                                  | Regra ou propriedade principal                                                                  | Operação ou ajuste importante                                                                                                            | Exemplo de aplicação                                                                                                            | Referência consultada                                                                                                                                      |
| ----------------------------- | -------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Árvore geral                  | Cada nó tem número arbitrário de filhos; hierarquia sem ordem obrigatória entre irmãos | Estrutura hierárquica sem ciclos; um único pai por nó                                           | Percursos (pré-ordem, pós-ordem, em nível)                                                                                               | Sistema de arquivos e pastas; organograma; estrutura de um documento XML/HTML                                                   | CELES, W.; RANGEL, J. L. Árvores. In: Estruturas de Dados. Rio de Janeiro: PUC-Rio, [s.d.]. Cap. 13, p. 12-1 a 12-14.                                      |
| Árvore binária                | Cada nó tem no máximo dois filhos (esquerdo e direito)                                 | Grau máximo 2; sem regra de ordenação dos valores                                               | Percursos em ordem, pré-ordem, pós-ordem e em nível                                                                                      | Árvore de expressões aritméticas; base para ABB e heap                                                                          | CELES, W.; RANGEL, J. L. Árvores. In: Estruturas de Dados. Rio de Janeiro: PUC-Rio, [s.d.]. Cap. 13, p. 12-1 a 12-14.\_                                    |
| Árvore binária de busca (ABB) | Árvore binária; chaves menores à esquerda e maiores à direita de cada nó               | Ordenação: esq < nó < dir (em cada subárvore)                                                   | Busca e inserção O(h); remoção com 3 casos (folha, um filho, dois filhos, usando sucessor/antecessor). Pode degenerar em lista, com O(n) | Conjunto ordenado ou dicionário em memória com dados de ordem razoavelmente aleatória                                           | CELES, W.; RANGEL, J. L. Árvores. In: Estruturas de Dados. Rio de Janeiro: PUC-Rio, [s.d.]. Cap. 13, p. 12-1 a 12-14.\_                                    |
| AVL                           | ABB com altura controlada                                                              | Em todo nó, \|h(esq) − h(dir)\| ≤ 1                                                             | Rotações simples (esquerda/direita) e duplas (esq-dir/dir-esq) após inserção ou remoção; busca O(log n) garantida                        | Estruturas em memória com muitas consultas e poucas alterações (índices, tabelas de símbolos, dicionários de leitura intensiva) | Árvore AVL (1962): Adelson-Velsky, G.; Landis, E. M. "An algorithm for the organization of information". Proceedings of the USSR Academy of Sciences.\_    |
| Rubro-negra                   | ABB em que cada nó tem cor (vermelho ou preto)                                         | Raiz preta; vermelho não tem filho vermelho; mesmo número de nós pretos em todo caminho até NIL | Recoloração e rotações após inserção/remoção; altura ≤ 2·log₂(n+1)                                                                       | `map`/`set` do C++ (STL), `TreeMap` do Java, escalonador do kernel Linux                                                        | Árvore Rubro-Negra (1978): Guibas, L. J.; Sedgewick, R. "A dichromatic framework for balanced trees". IEEE Symposium on Foundations of Computer Science.\_ |
| B                             | Nós com várias chaves ordenadas e vários filhos (ordem m); folhas no mesmo nível       | Ocupação mínima dos nós (exceto raiz); todas as folhas na mesma profundidade                    | Inserção com _split_ e promoção da chave mediana; remoção com empréstimo ou fusão; altura muito baixa, poucas leituras de disco          | Índices de bancos de dados e sistemas de arquivos que acessam disco                                                             | Árvore B (1972): Bayer, R.; McCreight, E. "Organization and maintenance of large ordered indexes". Acta Informatica.\_                                     |
| B+                            | Registros somente nas folhas; nós internos só têm chaves-guia; folhas encadeadas       | Todas as folhas no mesmo nível; chaves internas são cópias das folhas                           | _Split_ de folha copia a chave ao pai (não a remove da folha); varredura sequencial pela lista de folhas para consultas por intervalo    | Índices de SGBDs (ex.: MySQL/InnoDB, PostgreSQL) e sistemas de arquivos                                                         | _Comer, D. (1979). "The Ubiquitous B-Tree". ACM Computing Surveys (CSUR), 11(2), 121-137._                                                                 |

---

## Etapa 3 — Identificação por analogias

### 1. Estante de números reorganizada por rotações quando um lado fica alto demais

- **Estrutura:** Árvore AVL.
- **Justificativa:** A AVL mantém o fator de balanceamento (diferença de alturas das subárvores) em {-1, 0, 1}; quando uma inserção ou remoção viola isso, rotações restauram o equilíbrio.
- **Limite da analogia:** A estante não deixa claro que o critério é numérico e local (diferença de altura ≤ 1 em cada nó) nem que a ordem das chaves (esq < nó < dir) é preservada pelas rotações. Além disso, a rubro-negra também usa rotações, então "rotação" sozinha não distingue as duas.

### 2. Catálogo com várias chaves por página; quando a página enche, ela é dividida

- **Estrutura:** Árvore B.
- **Justificativa:** Cada nó (página) guarda várias chaves; ao exceder a capacidade, ocorre _split_ e a chave mediana é promovida ao pai. Isso mantém todas as folhas no mesmo nível.
- **Limite da analogia:** Um catálogo comum não mostra a promoção da mediana para a página "pai", nem que a árvore cresce pela raiz, nem a regra de ocupação mínima. Também vale para a B+, que igualmente divide páginas, então a analogia sozinha não separa B de B+.

### 3. Fila que mantém a tarefa de maior prioridade no topo para retirá-la primeiro

- **Estrutura:** Heap (max-heap), usado como fila de prioridade.
- **Justificativa:** A propriedade de heap garante que a raiz é o maior (ou menor) elemento; a remoção troca a raiz pelo último elemento e reorganiza com _sift-down_ em O(log n).
- **Limite da analogia:** Uma "fila" sugere ordem total de saída (FIFO ou totalmente ordenada). O heap só garante a relação entre pai e filhos, então os demais elementos não ficam completamente ordenados e a busca por uma chave qualquer é O(n). Também não é uma árvore de busca.

### 4. Índice que percorre letras sucessivas e compartilha o início de palavras com o mesmo prefixo

- **Estrutura:** Trie (árvore de prefixos).
- **Justificativa:** Cada nível representa uma posição da palavra, e palavras com o mesmo prefixo compartilham o caminho inicial; a busca custa O(k), onde k é o tamanho da palavra, independentemente de quantas palavras existem.
- **Limite da analogia:** A imagem do índice não mostra o marcador de fim de palavra (necessário para distinguir "car" de "carro"), nem o custo de memória, já que cada nó pode ter uma referência por símbolo do alfabeto.

### 5. Estrutura que usa cores, recolorações e rotações para manter controlada a altura dos caminhos

- **Estrutura:** Árvore rubro-negra.
- **Justificativa:** A regra de que todo caminho até NIL tem o mesmo número de nós pretos, e de que vermelho não tem filho vermelho, limita a altura a 2·log₂(n+1).
- **Limite da analogia:** As cores não existem fisicamente: são apenas um bit de metadado por nó para codificar a regra. Além disso, a analogia dá a ideia de equilíbrio perfeito, mas a rubro-negra é apenas aproximadamente balanceada (um caminho pode ter até o dobro do tamanho de outro), menos rígida que a AVL.

### 6. Índice que conduz às folhas com os registros, ligadas entre si para consultas por intervalo

- **Estrutura:** Árvore B+.
- **Justificativa:** Na B+, os registros ficam somente nas folhas, os nós internos só guardam chaves-guia e as folhas são encadeadas, permitindo achar o início do intervalo e percorrer sequencialmente.
- **Limite da analogia:** A descrição não mostra o fator de ramificação (ordem) que mantém a árvore baixa, nem que as chaves internas são cópias das chaves das folhas (e não os registros). Também não deixa claro que essa estrutura é pensada para minimizar acessos a disco.

### 7. Coleção de números em que cada nó direciona menores para a esquerda e maiores para a direita

- **Estrutura:** Árvore binária de busca (ABB).
- **Justificativa:** A propriedade de ordenação (esquerda < nó < direita) permite descartar uma subárvore a cada comparação, com custo O(h).
- **Limite da analogia:** A frase não indica que a forma da árvore depende da ordem de inserção: com chaves já ordenadas ela vira uma lista e a busca passa a O(n). Também não trata de chaves repetidas nem de remoção. Como a descrição só fala em ordem, uma AVL ou rubro-negra também a satisfaria, e o que falta é a garantia de balanceamento.

---

## Referências consultadas

\_- CELES, W.; RANGEL, J. L. Árvores. In: Estruturas de Dados. Rio de Janeiro: PUC-Rio, [s.d.]. Cap. 13, p. 12-1 a 12-14.

- Árvore AVL (1962): Adelson-Velsky, G.; Landis, E. M. "An algorithm for the organization of information". Proceedings of the USSR Academy of Sciences.\_
- Árvore Rubro-Negra (1978): Guibas, L. J.; Sedgewick, R. "A dichromatic framework for balanced trees". IEEE Symposium on Foundations of Computer Science.\_
- Árvore B (1972): Bayer, R.; McCreight, E. "Organization and maintenance of large ordered indexes". Acta Informatica.\_
  -Comer, D. (1979). "The Ubiquitous B-Tree". ACM Computing Surveys (CSUR), 11(2), 121-137.
