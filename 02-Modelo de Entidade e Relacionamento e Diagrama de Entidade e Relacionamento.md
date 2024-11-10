# Modelo Entidade-Relacionamento (MER) e Diagrama Entidade-Relacionamento (DER)

O **Modelo Entidade-Relacionamento (MER)** é uma técnica de modelagem conceitual que representa a estrutura de um banco de dados de forma intuitiva. Ele descreve como os dados se relacionam entre si no contexto do seu projeto. No MER, o foco é desenhar de forma intuitiva, sem se preocupar com detalhes de implementação.

## Diagrama Entidade-Relacionamento (DER)

O **Diagrama Entidade-Relacionamento (DER)** é a representação gráfica do MER. Ele facilita a visualização das **entidades**, seus **atributos** e os **relacionamentos** entre elas, permitindo uma compreensão mais clara de como os dados estão interconectados.

---

## Componentes de um MER e DER

### **Entidades**

As **entidades** são os objetos principais que serão armazenados no banco de dados. Elas representam um conjunto, coleção, conceito ou objeto do mundo real que desejamos guardar informações. Por exemplo, uma entidade chamada **Cliente** se tornará uma tabela **Cliente**, onde cada linha da tabela apresenta o registro de um cliente específico, e os atributos (como nome, e-mail, CPF) serão as colunas dessa tabela. 

#### **Exemplos de Entidades:**

1. **Cliente**: Agrupa dados de clientes de uma loja ou empresa.
2. **Produto**: Representa os itens disponíveis para venda.
3. **Funcionário**: Representa os empregados de uma empresa.

#### **Dicas de Boas Práticas:**

- **Nomeação:**
  - Use nomes no **singular** para entidades e atributos.
  - Utilize **letras maiúsculas** para entidades e **letras minúsculas** para atributos.
  - Exemplo: **"Cliente"** ou **"CLIENTE"** em vez de "Clientes" ou "cliente"; "nome" em vez de "NOME" ou "nomes".

- **Clareza e Simplicidade:**
  - Escolha nomes significativos que reflitam claramente o que a entidade representa e armazena.
  - Evite abreviações ou siglas que possam gerar confusão.

#### **Representação Visual no DER:**

As entidades são representadas por **retângulos**, com o nome da entidade escrito dentro ou acima do retângulo.

| ![Exemplo de Entidades](./assets/entidades-fortes.png) |

#### **Tipos de Entidades:**

##### **1. Entidades Fortes**

- **Descrição:** São entidades que possuem existência independente, ou seja, não dependem de outras entidades para existir. Para uma entidade forte existir, obrigatóriamente ela terá uma **chave primária própria**, que identifica essa entidade unicamente.

- **Exemplos:**

  1. **Cliente**: Um cliente pode existir independentemente de outras entidades. Não importa se a loja tem produtos ou pedidos, ainda sim pode ser interessante para a empresa armazenar dados de possíveis clientes. O cliente é identificado por um **id_cliente** único, ou **cpf**.
  2. **Produto**: Um produto tem sua própria identidade e não depende de outras entidades. Não precisa de clientes ou qualquer outra entidade para existir um produto.
  3. **Funcionário**: Um funcionário existe na empresa mesmo que não tenha clientes ou produtos associados. O funcionário é identificado por um **id_funcionario**, um **cpf** ou **matricula**, que são únicos.

- **Dicas de Boas Práticas:**

  - **Pergunta-chave:** "Essa entidade pode existir sozinha, sem depender de outra?" Se a resposta for "sim", ela é uma entidade forte e deverá ter uma chave primária.
  - **Consistência:** Certifique-se de que a entidade possui uma chave primária única.
  - **Simplicidade:** Evite entidades complexas que misturam múltiplos conceitos, como "ClienteProdutoFuncionario".
  - **Reutilização:** Considere reutilizar entidades existentes em vez de criar novas com dados semelhantes.
  - **Observação:** Na maioria dos casos, as entidades são fortes. Pode existir bancos com apenas entidades fortes.

- **Representação Visual no DER:**

  Entidades fortes são representadas por **retângulos simples**.

| ![Exemplo de Entidades Fortes](./assets/entidades-fortes.png) |

##### **2. Entidades Fracas**

- **Descrição:** São entidades que dependem de outra entidade (entidade forte) para existir. Elas não possuem uma chave primária própria suficiente para identificá-las unicamente, precisam de uma chave estrangeira que as conecte a uma entidade forte.

- **Exemplos:**

  1. **Dependente**: Dependente de um funcionário, como filhos ou cônjuge. Não faz sentido existir um dependente sem um funcionário associado. O dependente é identificado pela combinação de **id_funcionário** e **nome**.
  2. **Turma**: Turmas que dependem de uma disciplina específica. Em uma universidade, se você diz que se matriculou na "Turma 1", vão perguntar "Turma 1 de que disciplina?". A turma é identificada pela combinação de **id_disciplina** e **número**. Repare que a Turma não tem uma identidade própria, ela depende da Disciplina.
  3. **Endereço**: Endereços podem depender de um cliente ou funcionário. Um endereço sozinho pode não ter utilidade no seu banco. Mas isso depende do contexto do seu sistema. Pode ser que em algum caso, o endereço seja uma entidade forte.

- **Dicas de Boas Práticas:**

  - **Pergunta-chave:** "Essa entidade depende de outra para existir?" Se a resposta for "sim", ela é uma entidade fraca, e não deve ter uma chave primária própria. Deve ter uma chave estrangeira que a conecte a uma entidade forte.
  - **Chave Parcial:** Utilize um identificador parcial combinado com a chave primária da entidade forte, como **id_disciplina** e **número**.

- **Representação Visual no DER:**

  Entidades fracas são representadas por **retângulos com bordas duplas**.

| ![Exemplo de Entidades Fracas](../assets/entidades-fracas.png) |

> **Nota Importante:** A decisão sobre uma entidade ser forte ou fraca depende do contexto e dos requisitos do sistema. Por exemplo, se em um projeto é necessário que a entidade **Turma** exista independentemente de uma **Disciplina**, então ela seria modelada como uma entidade forte.

##### **3. Entidades Associativas:** Falaremos sobre elas após aprendermos sobre **Relacionamentos** e **Cardinalidades**.

---

### **Atributos**

Os **atributos** são as características ou propriedades que descrevem uma entidade. Eles correspondem às colunas das tabelas no banco de dados. Também podem ser vistos como itens pertencentes a um conjunto e existem vários tipos de atributos, como **simples**, **compostos**, **multivalorados** e **derivados**.

![Tipos de Atributos](./assets/tipos-de-atributos.png)

#### **Tipos de Atributos:**

##### **1. Atributos Simples**

- **Descrição:** Não podem ser divididos em partes menores.

- **Exemplos:**

  1. **nome**: "Ana".
  2. **CPF**: "123.456.789-00".
  3. **email**: "ana@example.com".

- **Dicas de Boas Práticas:**

  - Use nomes claros e significativos.
  - Evite armazenar múltiplas informações em um único atributo simples.

- **Representação Visual no DER:**

  Representados por **elipses** conectadas à entidade.

| ![Exemplo de Atributos Simples](./assets/atributos-simples.png) |

##### **2. Atributos Compostos**

- **Descrição:** Podem ser divididos em subpartes, cada uma com significado independente. Matematicamente, um atributo composto é um subconjunto de um conjunto maior.

- **Exemplos:**

  1. **endereço**, dividido em:
     - **rua**: "Avenida Paulista".
     - **número**: "1000".
     - **cidade**: "São Paulo".
     - **CEP**: "01311-000".
  2. **nomeCompleto**, dividido em:
     - **primeiroNome**: "Maria".
     - **sobrenome**: "Silva".
  3. **data**, dividido em:
     - **dia**: "15".
     - **mês**: "08".
     - **ano**: "2024".

- **Dicas de Boas Práticas:**

  - Avalie se as subpartes do atributo serão usadas separadamente no sistema.
  - Se as subpartes forem frequentemente utilizadas, considere armazená-las separadamente.
  
>**IMPORTANTE:** A decisão de manter um atributo composto ou separá-lo em atributos simples depende do contexto e das necessidades do sistema. No modelo lógico, um atributo composto é **dividido em vários atributos** na mesma tabela. Por exemplo, o atributo composto **endereço** se transforma em colunas como **rua**, **número**, **cidade** e **CEP** na tabela principal.

- **Representação Visual no DER:**

  Uma elipse principal conectada a subelipses.

| ![Exemplo de Atributos Compostos](./assets/atributos-compostos.png) |

##### **3. Atributos Multivalorados**

- **Descrição:** Podem ter múltiplos valores para uma única entidade.

- **Exemplos:**

  1. **telefones**: "+55 61 9999-1111", "+55 82 8888-2222".
  2. **e-mailsAlternativos**: "ana@hotmail.com", "ana@yahoo.com".
  3. **habilidades**: "Java", "Python", "SQL".

**IMPORTANTE:** A decisão de como lidar com um atributo multivalorado depende do contexto e das necessidades do sistema. No modelo lógico, é recomendável **criar uma tabela separada** para armazenar esses valores múltiplos, associando-os por meio de uma **chave estrangeira**. Por exemplo, se um cliente pode ter **vários números de telefone**, é melhor criar uma tabela **Telefones** com colunas para **número** e a **referência ao cliente**. Isso evita armazenar vários valores em uma única coluna, o que tornaria a busca e a manipulação dos dados mais difíceis.

- **Representação Visual no DER:**

  Representados por **elipses com bordas duplas**.

| ![Exemplo de Atributos Multivalorados](./assets/atributos-multivalorados.png) |

##### **4. Atributos Derivados**

- **Descrição:** Seu valor pode ser calculado a partir de outros atributos. Em alguns casos, é mais eficiente calcular o valor do que armazená-lo diretamente. Porém, existem casos em que é necessário armazenar o valor derivado para otimizar consultas, mas nesse caso esse atributo deixaria de ser derivado.

- **Exemplos:**

  1. **idade**, pode ser calculado a partir da **dataNascimento**.
  2. **saldo**, pode ser calculado a partir de **entradas** e **saídas** em uma conta.
  3. **duração**, pode ser calculado a partir da **dataInício** e **dataFim** de um projeto.

- **Dicas de Boas Práticas:**

  - Evite armazenar atributos derivados para não duplicar dados.
  - Calcule o valor quando necessário, garantindo dados atualizados.
  - Em alguns casos, pode ser que o cálculo do atributo derivado seja complexo e demorado, o que justifica armazenar o valor, mas isso faz com que o banco não siga a 3ª forma normal.

**IMPORTANTE:** Atributos derivados são calculados a partir de outros atributos e, por isso, em grande parte das vezes **não devem ser armazenados diretamente** no banco de dados, apenas aparecem no Modelo Entidade Relacionamento. Em vez disso, seu valor é gerado dinamicamente com base em uma fórmula ou cálculo. Por exemplo, a **idade** de uma pessoa pode ser derivada a partir de sua **data de nascimento**. Armazenar atributos derivados como colunas fixas pode causar inconsistências e duplicações, além de ocupar espaço desnecessário. Mas vale lembrar: ***DEPENDE DO CONTEXTO E DO QUE O SISTEMA PRECISA***

- **Representação Visual no DER:**

  Representados por **elipses com linha tracejada**.

| ![Exemplo de Atributos Derivados](./assets/atributos-derivados.png) |

---

### **Chaves**

As **chaves** são usadas para identificar unicamente registros em uma tabela e para estabelecer relacionamentos entre tabelas.

#### **Tipos de Chaves:**

##### **1. Chave Primária (Primary Key)**

- **Descrição:** Atributo ou conjunto de atributos que identifica unicamente cada registro.

- **Exemplos:**

  1. **ID_Cliente** em uma tabela **Cliente**.
  2. **CPF** em uma tabela **Pessoa**.
  3. **matricula** em uma tabela **Estudantes**.

- **Dicas de Boas Práticas:**

  - Utilize atributos que são sempre únicos e não nulos.
  - Evite atributos que possam mudar ao longo do tempo.
  - Não utilize "nome" ou "email" como chave primária, pois podem não ser únicos. Existem muitos "José Silva Souza" no mundo.

**CURIOSIDADE:** As universidades preferem usar **números de matrícula** como chave primária ao invés de **CPF** por razões de **privacidade, segurança e controle interno**. A matrícula é um identificador único gerado pela própria instituição, permitindo mais flexibilidade para gerenciar alunos, incluindo estrangeiros (que não possuem CPF), sem expor informações sensíveis. Além disso, ela pode seguir padrões que ajudam a identificar ano de ingresso e curso (a UnB usa o ano de ingresso no início da matrícula), facilitando a organização dos registros acadêmicos.

- **Representação Visual no DER:**

  Atributo **sublinhado**.

| ![Exemplo de Chave Primária](./assets/chave-primaria.png) |

##### **2. Chave Estrangeira (Foreign Key)**

- **Descrição:** Atributo em uma tabela que referencia a chave primária de outra tabela, estabelecendo um relacionamento entre elas.

- **Exemplos:**

  1. **idCliente** na tabela **Pedido**, referenciando **Cliente**.
  2. **idProduto** na tabela **ItemPedido**, referenciando **Produto**.
  3. **idAutor** na tabela **Livro**, referenciando **Autor**.

- **Dicas de Boas Práticas:**

  - Mantenha a consistência de nomes para facilitar o entendimento. Por exemplo, não coloque somente "id" como prefixo, mas sim "idCliente", "idProduto". Isso ajuda a entender qual tabela está sendo referenciada.

- **Representação Visual no DER:**

  Indicada através dos **relacionamentos** entre entidades, colocando a chave estrangeira em um atributo da entidade.

##### **3. Chave Candidata (Candidate Key)**

- **Descrição:** Atributo(s) que poderiam ser escolhidos como chave primária. Essa definião é importante para a normalização do banco de dados, que visa reduzir a redundância e a inconsistência dos dados.

- **Exemplos:**

  1. **CPF** e **RG** em **Pessoa**; ambos são únicos, mas apenas um pode ser a chave primária. O outro seria uma chave candidata.
  2. **email** e **nomeUsuario** em **Usuário**.
  3. **placa** e **chassi** em **Veículo**.

- **Dicas de Boas Práticas:**

  - Analise todos os atributos únicos antes de escolher a chave primária.
  - Considere estabilidade e imutabilidade ao selecionar a chave primária.

- **Representação Visual no DER:**

  Apenas a chave primária é sublinhada; chaves candidatas são atributos normais.

##### **4. Chave Alternativa (Alternate Key)**

- **Descrição:** Chave candidata que não foi escolhida como chave primária.

- **Exemplos:**

  1. **RG** em **Pessoa**, se **CPF** for a chave primária.
  2. **email** em **Cliente**, se **ID_Cliente** for a chave primária.
  3. **nomeUsuario** em **Usuário**, se **ID_Usuario** for a chave primária.

- **Dicas de Boas Práticas:**

  - Podem ser utilizadas para garantir a unicidade em outros atributos.
  - Defina restrições únicas no banco de dados para essas chaves.

- **Representação Visual no DER:**

  Não há distinção visual específica; tratadas como atributos normais.

##### **5. Chave Composta (Composite Key)**

- **Descrição:** Chave primária formada por dois ou mais atributos.

- **Exemplos:**

  1. **idDisciplina** e **número** em **Turma**.
  2. **idCliente** e **idProduto** em **ItemPedido**.
  3. **idAutor** e **idLivro** em **Autoria**.

- **Dicas de Boas Práticas:**

  - Use quando nenhum atributo sozinho pode identificar unicamente um registro.
  - Certifique-se de que a combinação dos atributos seja sempre única.

- **Representação Visual no DER:**

  Atributos que compõem a chave são **sublinhados**.

| ![Exemplo de Chave Composta](./assets/chave-composta.png) |

##### **6. Chave Secundária (Secondary Key)**

- **Descrição:** Atributo usado para criar índices e acelerar consultas, mas que não é necessariamente único.

- **Exemplos:**

  1. **nome** em **Cliente** para buscas frequentes por nome.
  2. **categoria** em **Produto** para filtrar produtos.
  3. **dataCompra** em **Pedido** para consultas por período.

- **Dicas de Boas Práticas:**

  - Identifique atributos frequentemente usados em consultas.
  - Crie índices no banco de dados para esses atributos.

- **Representação Visual no DER:**

  Não há representação específica; são atributos normais.

##### **7. Chave Super (Super Key)**

- **Descrição:** Qualquer conjunto de atributos que identifica unicamente uma linha na tabela. Inclui a chave primária e outras combinações que podem ser supérfluas.

- **Exemplos:**

  1. **ID_Cliente** sozinho, ou **ID_Cliente** combinado com **CPF** em **Cliente**.
  2. **matricula** em **Funcionário**, ou **matricula** e **CPF** juntos.
  3. **ID_Pedido**, ou **ID_Pedido** e **dataPedido** em **Pedido**.

- **Dicas de Boas Práticas:**

  - Evite usar super chaves com atributos desnecessários.
  - Prefira chaves simples e eficientes.

- **Representação Visual no DER:**

  Não são explicitamente representadas.

---

### **Relacionamentos**

Os **relacionamentos** definem como as entidades interagem entre si no modelo de dados. Eles são fundamentais para entender como as informações estão conectadas e como os dados serão armazenados no banco de dados. Compreender os tipos de relacionamentos é essencial para criar um banco de dados eficiente e bem estruturado.

Existem três tipos principais de relacionamentos:

1. **Relacionamento Um-para-Um (1:1)**
2. **Relacionamento Um-para-Muitos (1:N)**
3. **Relacionamento Muitos-para-Muitos (N:M)**

Esses números (1:1, 1:N, N:M) representam as **cardinalidades** dos relacionamentos, ou seja, quantos registros de uma entidade estão associados a quantos registros da outra entidade.

Repare que os relacionamentos conectam as entidades passando uma ideia clara, como no exemplo: "Cliente Faz Pedido".

| ![Exemplo de Relacionamento](./assets/relacionamentos-binarios.png) |


Os **relacionamentos** também podem ser vistos como **conjuntos**, onde cada conjunto é uma entidade e itens do conjunto A estão relacionados a itens do conjunto B. Por exemplo, o conjunto de **Clientes** está relacionado ao conjunto de **Pedidos**.

![Exemplo de Relacionamento Conjunto](./assets/relacionamento_conjunto.png)

#### **1. Relacionamento Um-para-Um (1:1)**

- **Descrição:**

  No relacionamento **um-para-um**, cada registro (ou linha) da entidade A está associado a **no máximo um** registro da entidade B, e vice-versa. Isso significa que para cada dado na tabela A, existe **no máximo um** dado correspondente na tabela B.

- **Exemplos Simples:**

  1. **Pessoa e Carteira de Identidade:**

     - **Pessoa**: Cada pessoa possui uma única carteira de identidade.
     - **Carteira de Identidade**: Cada carteira de identidade pertence a uma única pessoa.
  
  2. **Usuário e Perfil:**

     - **Usuário**: Cada usuário em um sistema tem um perfil único com suas configurações.
     - **Perfil**: Cada perfil está associado a um único usuário.

  3. **País e Capital:**

     - **País**: Cada país tem uma única capital.
     - **Capital**: Cada capital é de um único país.

- **Como Representar no DER:**

  No Diagrama Entidade-Relacionamento (DER), um relacionamento um-para-um é representado por um losango conectado a duas entidades, com o número "1" próximo às linhas que ligam o relacionamento às entidades.

    |![Exemplo de Relacionamento 1:1 - Pessoa:Identidade](./assets/relacionamento11_PessoaIdentidade.png)

    >**OBSERVAÇÃO:** A seta utilizada no diagrama é apenas para indicar o sentido da frase. Não é uma regra de modelagem. É uma boa prática, pois facilita a leitura do diagrama. Carteira de Identidade **Possui** Pessoa não faz sentido. Por isso, a seta é usada para indicar a direção correta.

- **Como Transformar em Tabelas:**

  Existem duas abordagens para implementar um relacionamento 1:1 no banco de dados:

  **1. Combinar as Entidades em uma Única Tabela:**

     - **Quando Usar:** Se as duas entidades sempre existem juntas e têm uma relação direta.
     - **Implementação:** Criar uma única tabela que contém os atributos de ambas as entidades.
     - **Exemplo:**
       - Tabela `Pessoa` com atributos de pessoa e carteira de identidade.

  **2. Manter Entidades Separadas com Chave Estrangeira Única:**

     - **Quando Usar:** Quando as entidades podem existir separadamente ou para manter uma estrutura mais organizada.
     - **Implementação:**
       - Adicionar uma chave estrangeira em uma das tabelas que referencia a chave primária da outra tabela.
       - Garantir que essa chave estrangeira seja única (definir como UNIQUE).
     - **Exemplo:**
       - Tabela `Pessoa` com atributo `carteira_identidade_id` que referencia `CarteiraIdentidade`.
       - Ou tabela `CarteiraIdentidade` com `pessoa_id` que referencia `Pessoa`.

- **Exemplo Prático:**

  **Tabelas:**

  - **Pessoa**
    - `pessoa_id` (PK)
    - `nome`
    - `data_nascimento`
    - `carteira_identidade_id` (FK, UNIQUE)

  - **CarteiraIdentidade**
    - `carteira_identidade_id` (PK)
    - `numero`
    - `data_emissao`
    - `pessoa_id` (FK, UNIQUE) *alternativa*

- **Dicas de Boas Práticas:**

  - **Avalie a Necessidade de Separação:**
    - Se as entidades são conceitualmente distintas e podem existir separadamente, mantenha-as em tabelas separadas. Em algumas vezes você não precisa pegar todos os dados de uma entidade, então é melhor separar, para não trazer dados desnecessários nas consultas.
  - **Integridade Referencial:**
    - Use restrições de chave estrangeira para garantir a integridade dos dados.
  - **Chave Única:**
    - Defina a chave estrangeira como UNIQUE para manter o relacionamento 1:1.

---

#### **2. Relacionamento Um-para-Muitos (1:N)**

- **Descrição:**

  No relacionamento **um-para-muitos**, um registro da entidade A pode estar associado a **vários** registros da entidade B, mas cada registro de B está associado a **apenas um** registro de A.

- **Exemplos Simples:**

  1. **Cliente e Pedido:**

     - **Cliente**: Um cliente pode fazer vários pedidos.
     - **Pedido**: Cada pedido é feito por um único cliente.
    
  ```
  [Cliente] 1 --------- N [Pedido]
  ```

  2. **Professor e Turma:**

     - **Professor**: Um professor pode lecionar em várias turmas.
     - **Turma**: Cada turma é ministrada por um único professor.
    
  ```
  [Professor] 1 --------- N [Turma]
  ```

  3. **Departamento e Funcionário:**

     - **Departamento**: Um departamento tem vários funcionários.
     - **Funcionário**: Cada funcionário trabalha em um único departamento.
    
  ```
  [Departamento] 1 --------- N [Funcionário]
  ```

- **Como Representar no DER:**

  No DER, o relacionamento um-para-muitos é representado por um losango conectado às entidades, com "1" próximo à entidade do lado "um" e "N" ou "*" próximo à entidade do lado "muitos".

![Exemplo de Relacionamento 1:N - Professor:Turma](./assets/relacionamentoN1_Turma.png)

- **Como Transformar em Tabelas:**

  **Passos:**

  - **Adicionar Chave Estrangeira na Tabela do Lado "Muitos":**
    - Adicionar uma coluna na tabela da entidade "muitos" que referencia a chave primária da entidade "um".

  - **Implementação:**
    - Na tabela `Turma`, adicionar `professor_id` como chave estrangeira para `Professor`.

- **Exemplo Prático:**

  **Tabelas:**

  - **Professor**
    - `professor_id` (PK)
    - `nome`
    - `especialidade`

  - **Turma**
    - `disciplina_id` (PK)
    - `numero` (PK)
    - `horario`
    - `professor_id` (FK para `Professor`)

- **Dicas de Boas Práticas:**

  - **Integridade Referencial:**
    - Defina a chave estrangeira com restrições para garantir que cada turma esteja associada a um professor existente.
  - **Nomeação Clara:**
    - Use nomes de colunas que deixem claro o relacionamento, como `professor_id`.
  - **Evitar Redundância:**
    - Não armazene informações do professor na tabela `Turma` além da chave estrangeira.

---

#### **3. Relacionamento Muitos-para-Muitos (N:M)**

- **Descrição:**

  No relacionamento **muitos-para-muitos**, vários registros da entidade A podem estar associados a vários registros da entidade B, e vice-versa.

- **Exemplos Simples:**

  1. **Aluno e Disciplina:**

     - **Aluno**: Um aluno pode se matricular em várias disciplinas.
     - **Disciplina**: Uma disciplina pode ter vários alunos matriculados.

```
  [Aluno] N --------- N [Disciplina]
```
  
  2. **Produto e Pedido:**

     - **Produto**: Um produto pode estar em vários pedidos.
     - **Pedido**: Um pedido pode conter vários produtos.

```
  [Produto] N --------- N [Pedido]
```

  3. **Autor e Livro:**

     - **Autor**: Um autor pode escrever vários livros.
     - **Livro**: Um livro pode ter vários autores.

```
  [Autor] N --------- N [Livro]
```

- **Como Representar no DER:**

  No DER, o relacionamento muitos-para-muitos é representado por um losango conectado às entidades, com "N" ou "*" próximo a ambas as entidades.

![Exemplo de Relacionamento N:M - Aluno:Disciplina](./assets/relacionamentoNN_Matricula.png)

- **Como Transformar em Tabelas:**

  **Passos:**

  - **Criar uma Entidade Associativa (Tabela Intermediária):**
    - Criar uma nova tabela que representa o relacionamento.
    - Essa tabela contém chaves estrangeiras para cada uma das entidades relacionadas.
    - As chaves estrangeiras juntas formam a chave primária da tabela intermediária (ou você pode criar uma chave primária própria).

  - **Implementação:**
    - Criar a tabela `Matrícula` com `aluno_id` e `disciplina_id` como chaves estrangeiras.

- **Exemplo Prático:**

  **Tabelas:**

  - **Aluno**
    - `aluno_id` (PK)
    - `nome`
    - `curso`

  - **Disciplina**
    - `disciplina_id` (PK)
    - `nome`
    - `creditos`

  - **Matrícula**
    - `matricula_id` (PK) *opcional, se não usar chave composta*
    - `aluno_id` (FK para `Aluno`)
    - `disciplina_id` (FK para `Disciplina`)
    - `nota`
    - `frequencia`
    - `status`

    - **Chave Primária:** Pode ser composta por (`aluno_id`, `disciplina_id`) ou um campo `matricula_id`. Além disso, podem ser adicionados atributos adicionais à tabela intermediária, como `nota`, `frequencia` e `status`.

- **Dicas de Boas Práticas:**

  - **Nomeação Significativa:**
    - Dê um nome claro à tabela intermediária, como `Matrícula`, `ItemPedido`, `AutorLivro`.
  - **Atributos Adicionais:**
    - Se houver informações específicas sobre o relacionamento (como `data_matricula`), inclua-as na tabela intermediária.
  - **Integridade Referencial:**
    - Defina chaves estrangeiras com restrições para manter a consistência dos dados.

---

#### **Transformação dos Relacionamentos em Tabelas**

Vamos detalhar como os relacionamentos são transformados em tabelas, com base nos exemplos anteriores.

#### **Exemplo 1: Cliente e Pedido (1:N)**

- **Entidades:**

  - **Cliente**
    - `cliente_id` (PK)
    - `nome`
    - `email`

  - **Pedido**
    - `pedido_id` (PK)
    - `data_pedido`
    - `valor_total`

- **Implementação do Relacionamento:**

  - Na tabela `Pedido`, adicionar `cliente_id` como chave estrangeira para `Cliente`.

- **Tabelas Finais:**

  - **Cliente**
    - `cliente_id` (PK)
    - `nome`
    - `email`

  - **Pedido**
    - `pedido_id` (PK)
    - `data_pedido`
    - `valor_total`
    - `cliente_id` (FK para `Cliente`)

#### **Exemplo 2: Produto e Pedido (N:M)**

- **Entidades:**

  - **Produto**
    - `produto_id` (PK)
    - `nome`
    - `preco`

  - **Pedido**
    - `pedido_id` (PK)
    - `data_pedido`
    - `valor_total`

- **Entidade Associativa:**

  - **ItemPedido**
    - `item_pedido_id` (PK) *opcional*
    - `pedido_id` (FK para `Pedido`)
    - `produto_id` (FK para `Produto`)
    - `quantidade`
    - `preco_unitario`

    - **Chave Primária:** Pode ser composta por (`pedido_id`, `produto_id`) ou um campo `item_pedido_id`.

- **Tabelas Finais:**

  - **Produto**
    - `produto_id` (PK)
    - `nome`
    - `preco`

  - **Pedido**
    - `pedido_id` (PK)
    - `data_pedido`
    - `valor_total`

  - **ItemPedido**
    - `item_pedido_id` (PK) *se houver*
    - `pedido_id` (FK para `Pedido`)
    - `produto_id` (FK para `Produto`)
    - `quantidade`
    - `preco_unitario`

#### **Exemplo 3: Autor e Livro (N:M)**

- **Entidades:**

  - **Autor**
    - `autor_id` (PK)
    - `nome`

  - **Livro**
    - `livro_id` (PK)
    - `titulo`

- **Entidade Associativa:**

  - **AutorLivro**
    - `autor_livro_id` (PK) *opcional*
    - `autor_id` (FK para `Autor`)
    - `livro_id` (FK para `Livro`)

    - **Chave Primária:** Pode ser composta por (`autor_id`, `livro_id`) ou um campo `autor_livro_id`.

- **Tabelas Finais:**

  - **Autor**
    - `autor_id` (PK)
    - `nome`

  - **Livro**
    - `livro_id` (PK)
    - `titulo`

  - **AutorLivro**
    - `autor_livro_id` (PK) *se houver*
    - `autor_id` (FK para `Autor`)
    - `livro_id` (FK para `Livro`)

> **IMPORTANTE:** A decisão da cardinalidade do relacionamento depende de cada projeto. Pode ser que em algum projeto, vários professores possam lecionar em uma unica turma e o mesmo professor lecionar em várias turmas. Nesse caso, o relacionamento seria N:M, diferente de um dos nossos exemplos passados. Por isso, é importante entender o contexto do sistema e os requisitos do projeto para definir a cardinalidade correta. 

---

### **Relacionamentos Não Binários e Outros Tipos de Relacionamentos**

Além dos relacionamentos binários (entre duas entidades), existem outros tipos de relacionamentos no modelo Entidade-Relacionamento (ER) que são importantes compreender para modelar corretamente um banco de dados. Vamos explorar os **relacionamentos unários (recursivos)**, **relacionamentos ternários** e outros relacionamentos especiais que podem surgir durante a modelagem.

#### **1. Relacionamento Unário (Recursivo)**

- **Descrição:**

  Um **relacionamento unário** ou **relacionamento recursivo** ocorre quando uma entidade está relacionada **consigo mesma**. Isso significa que os registros dessa entidade podem se relacionar com outros registros da **mesma entidade**.

- **Exemplos Simples:**

  1. **Pessoa e Conjugue:**

     - **Pessoa**: Uma pessoa pode ser casada com outra pessoa.
     - **Relacionamento**: Uma pessoa pode ser conjugue de outra pessoa.

  2. **Produto e Componente:**

     - **Produto**: Um produto pode ser composto por outros produtos.
     - **Relacionamento**: Um produto pode ser componente de outro produto.

  3. **Pasta e Subpasta:**

     - **Pasta**: Uma pasta pode conter outras pastas.
     - **Relacionamento**: Uma pasta pode ser subpasta de outra pasta.
  
  4. **Funcionário e Gerente:**

     - **Funcionário**: Um funcionário pode ser gerenciado por outro funcionário.
     - **Relacionamento**: Um funcionário pode ser gerente de outro funcionário.


##### Como Representar no DER:**

  No Diagrama Entidade-Relacionamento (DER), o relacionamento unário é representado por um losango que conecta a entidade a si mesma.

  ![Exemplo de Relacionamento Unário - Funcionário:Gerencia](./assets/relacionamentoUnario_FuncionarioGerencia.png)

  > **Nota:** A linha que volta para a entidade indica o relacionamento recursivo.

##### Como Transformar em Tabelas:**

  **Passos:**

  - **Adicionar uma Chave Estrangeira que Referencia a Própria Tabela:**
    - Adicionar uma coluna na tabela que referencia a chave primária da mesma tabela.

  - **Implementação:**
    - Na tabela `Funcionário`, adicionar `gerente_id` como chave estrangeira que referencia `funcionario_id` na própria tabela.

- **Exemplo Prático:**

  **Tabela: Funcionário**

  - `funcionario_id` (PK)
  - `nome`
  - `cargo`
  - `salario`
  - `gerente_id` (FK para `funcionario_id` em `Funcionário`)

- **Dicas de Boas Práticas:**

  - **Permitir Valores Nulos na Chave Estrangeira:**
    - O gerente de um funcionário pode ser nulo se o funcionário não tiver gerente (por exemplo, é o diretor geral).
  - **Integridade Referencial:**
    - Defina a chave estrangeira com restrições para manter a consistência dos dados.
  - **Nomeação Clara:**
    - Use nomes descritivos como `gerente_id` para deixar claro o propósito da coluna.

---

#### **2. Relacionamento Ternário**

- **Descrição:**

  Um **relacionamento ternário** envolve **três entidades** que estão relacionadas entre si em um único relacionamento. É utilizado quando a interação entre as três entidades não pode ser adequadamente representada por relacionamentos binários separados.

- **Exemplos Simples:**

  1. **Médico, Paciente e Medicamento:**

     - **Médico**: Prescreve medicamentos.
     - **Paciente**: Recebe prescrições de médicos.
     - **Medicamento**: É prescrito a pacientes por médicos.
     - **Relacionamento**: A prescrição envolve um médico, um paciente e um medicamento.

  2. **Fornecedor, Produto e Armazém:**

     - **Fornecedor**: Fornece produtos.
     - **Produto**: É fornecido por fornecedores.
     - **Armazém**: Armazena produtos fornecidos.
     - **Relacionamento**: O fornecimento de produtos envolve um fornecedor, um produto e um armazém.

  3. **Professor, Disciplina e Semestre:**

     - **Professor**: Leciona disciplinas.
     - **Disciplina**: É lecionada por professores.
     - **Semestre**: Período em que a disciplina é lecionada.
     - **Relacionamento**: A atribuição de disciplinas envolve um professor, uma disciplina e um semestre.

##### **Como Representar no DER:**

  No DER, um relacionamento ternário é representado por um losango que conecta as três entidades envolvidas.

  ![Exemplo de Relacionamento Ternário - Médico:Paciente:Medicamento](./assets/relacionamentoTernario_Prescricao.png)

##### **Como Transformar em Tabelas:**

  **Passos:**

  - **Criar uma Tabela de Associação para o Relacionamento:**
    - Criar uma tabela que representa o relacionamento ternário.
    - Essa tabela contém chaves estrangeiras para cada uma das três entidades.
    - As chaves estrangeiras juntas formam a chave primária da tabela (ou você pode criar uma chave primária própria).

  - **Implementação:**
    - Criar a tabela `Prescrição` com `medico_id`, `paciente_id` e `medicamento_id` como chaves estrangeiras.

- **Exemplo Prático:**

  **Tabelas:**

  - **Médico**
    - `medico_id` (PK)
    - `nome`
    - `especialidade`

  - **Paciente**
    - `paciente_id` (PK)
    - `nome`
    - `data_nascimento`

  - **Medicamento**
    - `medicamento_id` (PK)
    - `nome`
    - `dosagem`

  - **Prescrição**
    - `prescricao_id` (PK) *opcional*
    - `medico_id` (FK para `Médico`)
    - `paciente_id` (FK para `Paciente`)
    - `medicamento_id` (FK para `Medicamento`)
    - `data_prescricao`
    - `posologia`

    - **Chave Primária:** Pode ser composta por (`medico_id`, `paciente_id`, `medicamento_id`) ou um campo `prescricao_id`.

##### **Dicas de Boas Práticas:**

  - **Atributos Adicionais:**
    - Inclua na tabela de associação os atributos que descrevem o relacionamento, como `data_prescricao` e `posologia`.
  - **Integridade Referencial:**
    - Defina chaves estrangeiras com restrições para manter a consistência dos dados.
  - **Nomeação Clara:**
    - Dê um nome significativo à tabela de relacionamento, como `Prescrição`, para refletir o contexto do relacionamento.

---

#### **3. Relacionamentos de Ordem Superior**

- **Descrição:**

  Relacionamentos que envolvem mais de três entidades são chamados de **relacionamentos de ordem superior** (quaternários, quinários, etc.). Eles são menos comuns e geralmente indicam que o modelo pode ser simplificado.

- **Exemplo:**

  - **Projeto, Funcionário, Ferramenta e Localização:**

    - **Projeto**: Atividade em execução.
    - **Funcionário**: Trabalha em projetos.
    - **Ferramenta**: Utilizada em projetos.
    - **Localização**: Onde o projeto está sendo executado.
    - **Relacionamento Quaternário**: Um funcionário utiliza uma ferramenta em um projeto em uma determinada localização.

- **Como Representar no DER:**

  No DER, um relacionamento de ordem superior é representado por um losango conectado a todas as entidades envolvidas, assim como em relacionamentos ternários.

- **Como Transformar em Tabelas:**

  **Passos:**

  - **Criar uma Tabela de Associação para o Relacionamento:**
    - Criar uma tabela que representa o relacionamento de ordem superior.
    - A tabela contém chaves estrangeiras para cada entidade envolvida.
    - As chaves estrangeiras juntas formam a chave primária da tabela (ou você pode criar uma chave primária própria).

- **Exemplo Prático:**

  **Tabelas:**

  - **Projeto**
    - `projeto_id` (PK)
    - `nome`
    - `descricao`

  - **Funcionário**
    - `funcionario_id` (PK)
    - `nome`
    - `cargo`

  - **Ferramenta**
    - `ferramenta_id` (PK)
    - `nome`
    - `tipo`

  - **Localizacao**
    - `localizacao_id` (PK)
    - `endereco`
    - `cidade`

  - **Alocacao**
    - `alocacao_id` (PK) *opcional*
    - `projeto_id` (FK para `Projeto`)
    - `funcionario_id` (FK para `Funcionário`)
    - `ferramenta_id` (FK para `Ferramenta`)
    - `localizacao_id` (FK para `Localizacao`)
    - `data_inicio`
    - `data_fim`

    - **Chave Primária:** Pode ser composta por todas as chaves estrangeiras ou um campo `alocacao_id`.

- **Dicas de Boas Práticas:**

  - **Simplicidade:**
    - Avalie se o relacionamento pode ser decomposto em relacionamentos menores para simplificar o modelo.
  - **Clareza:**
    - Certifique-se de que o relacionamento de ordem superior é realmente necessário e agrega valor ao modelo.
  - **Integridade Referencial:**
    - Defina chaves estrangeiras adequadas e restrições para manter a consistência dos dados.

#### **Dicas Gerais para Modelagem de Relacionamentos Não Binários**

- **Análise Detalhada do Domínio:**
  - Compreenda completamente os requisitos do negócio para identificar corretamente os relacionamentos.
- **Simplificação do Modelo:**
  - Sempre que possível, simplifique relacionamentos de ordem superior decompondo-os em relacionamentos binários.
- **Representação Clara no DER:**
  - Utilize símbolos e notações adequadas para representar os diferentes tipos de relacionamentos.
- **Consistência na Nomeação:**
  - Use nomes claros e consistentes para entidades, relacionamentos e atributos.
- **Integridade dos Dados:**
  - Defina chaves primárias e estrangeiras apropriadas.
  - Implemente restrições de integridade referencial no banco de dados.
- **Documentação:**
  - Mantenha uma documentação detalhada do modelo para facilitar a compreensão e manutenção.

#### **Exemplos Adicionais**

1. **Relacionamento Unário - Produto e Subproduto:**

   - **Produto**: Item produzido ou vendido.
   - **Relacionamento**: Um produto pode ser composto por outros produtos (subprodutos).
   - **Implementação:**
     - Na tabela `Produto`, adicionar `produto_pai_id` como chave estrangeira para `produto_id`.

2. **Relacionamento Ternário - Aluno, Disciplina e Professor:**

   - **Aluno**: Estudante matriculado.
   - **Disciplina**: Matéria oferecida.
   - **Professor**: Profissional que leciona.
   - **Relacionamento**: Atribuição de aluno a uma disciplina com um professor específico.
   - **Implementação:**
     - Criar a tabela `Aula` com chaves estrangeiras `aluno_id`, `disciplina_id`, `professor_id`.

3. **Agregação - Evento, Participante e Patrocinador:**

   - **Evento**: Ocasião organizada.
   - **Participante**: Pessoa que participa do evento.
   - **Patrocinador**: Empresa que apoia o evento.
   - **Relacionamento:**
     - `Evento` é uma agregação do relacionamento entre `Participante` e `Atividade`.
     - `Evento` se relaciona com `Patrocinador`.

---

### **Agregação**

**Agregação** é um conceito utilizado no Modelo Entidade-Relacionamento (MER) que permite tratar um **relacionamento** como se fosse uma **entidade**. Isso é especialmente útil quando precisamos que um relacionamento participe de outro relacionamento, ou seja, quando um relacionamento precisa se relacionar com outras entidades. A agregação nos ajuda a representar interações mais complexas de forma clara e organizada.

#### **Quando Usar Agregação**

- **Relacionamentos entre Relacionamentos**: Quando um relacionamento precisa se relacionar com outra entidade ou relacionamento.
- **Simplificação de Diagramas Complexos**: Para reduzir a complexidade visual em diagramas que possuem muitos relacionamentos.
- **Representar Interações Complexas**: Quando o relacionamento em si possui atributos próprios ou é significativo no contexto do negócio.

#### **Exemplo Simples de Agregação**

Imagine uma empresa onde:

- **Funcionários** trabalham em **Projetos**.
- **Clientes** solicitam **Projetos**.

Agora, queremos representar que um **Funcionário** trabalha em um **Projeto** específico para um **Cliente**. O relacionamento "trabalha em" precisa se relacionar com a entidade **Cliente**.

Para modelar isso, podemos usar a **agregação**.

#### **Passo a Passo da Agregação**

1. **Identificar o Relacionamento que Precisa ser Agregado**

   - O relacionamento "trabalha em" entre **Funcionário** e **Projeto**.

2. **Transformar o Relacionamento em uma Entidade**

   - Criamos uma nova entidade chamada **Alocação** (ou outro nome apropriado).
   - Esta entidade representa o fato de um funcionário estar alocado em um projeto.

3. **Associar a Nova Entidade com a Terceira Entidade**

   - **Alocação** se relaciona com **Cliente**.
   - Isso nos permite registrar para qual cliente o funcionário está trabalhando em determinado projeto.

4. **Adicionar Atributos Relevantes**

   - **Alocação** pode ter atributos como:
     - **data_inicio**
     - **data_fim**
     - **papel** (ex.: desenvolvedor, gerente)
     - **horas_trabalhadas**

#### **Representação Visual no DER**

- **Funcionário** e **Projeto** estão ligados pelo relacionamento "trabalha em".
- Aplicamos a agregação e transformamos "trabalha em" na entidade **Alocação**.
- **Alocação** então se relaciona com **Cliente**.
- O diagrama reflete essa estrutura de forma clara.

![Exemplo de Agregação](./assets/agregacao-exemplo.png)

#### **Como Transformar em Tabelas**

**1. Tabela Funcionário**

- `funcionario_id` (PK)
- `nome`
- Outros atributos do funcionário

**2. Tabela Projeto**

- `projeto_id` (PK)
- `nome`
- Outros atributos do projeto

**3. Tabela Cliente**

- `cliente_id` (PK)
- `nome`
- Outros atributos do cliente

**4. Tabela Alocação**

- `alocacao_id` (PK)
- `funcionario_id` (FK para Funcionário)
- `projeto_id` (FK para Projeto)
- `cliente_id` (FK para Cliente)
- `data_inicio`
- `data_fim`
- `papel`
- `horas_trabalhadas`

**Explicação:**

- A tabela **Alocação** reúne as chaves estrangeiras de **Funcionário**, **Projeto** e **Cliente**.
- Armazena informações específicas da alocação do funcionário no projeto para um cliente.

#### **Outro Exemplo de Agregação**

Considere um sistema acadêmico:

- **Professor** ensina **Disciplina**.
- **Disciplina** faz parte de um **Curso**.

Queremos relacionar que o **Professor** ensina uma **Disciplina** em um **Curso** específico.

**Passo a Passo:**

1. **Identificar o Relacionamento a ser Agregado**

   - O relacionamento "ensina" entre **Professor** e **Disciplina**.

2. **Transformar o Relacionamento em uma Entidade**

   - Criamos a entidade **Ensino**.

3. **Associar a Nova Entidade com a Terceira Entidade**

   - **Ensino** se relaciona com **Curso**.

4. **Adicionar Atributos Relevantes**

   - **Ensino** pode ter atributos como:
     - **semestre**
     - **ano**
     - **sala**

**Tabelas Resultantes:**

- **Professor**
  - `professor_id` (PK)
  - `nome`
- **Disciplina**
  - `disciplina_id` (PK)
  - `nome`
- **Curso**
  - `curso_id` (PK)
  - `nome`
- **Ensino**
  - `ensino_id` (PK)
  - `professor_id` (FK)
  - `disciplina_id` (FK)
  - `curso_id` (FK)
  - `semestre`
  - `ano`
  - `sala`

#### **Dicas de Boas Práticas**

- **Clareza e Simplicidade**

  - Use a agregação quando ela tornar o modelo mais fácil de entender.
  - Evite complicar o modelo com agregações desnecessárias.

- **Nomeação Significativa**

  - Dê nomes claros às entidades agregadas, refletindo seu propósito.
  - **Exemplo:** "Alocação" em vez de "TrabalhoProjetoCliente".

- **Documentação**

  - Explique o porquê da agregação e como as entidades estão relacionadas.
  - Isso ajuda outros desenvolvedores a entenderem o modelo.

- **Consistência**

  - Seja consistente na forma como aplica a agregação no modelo.
  - Use padrões que facilitem a leitura e manutenção.

#### **Quando Evitar a Agregação**

- **Complexidade Desnecessária**

  - Se a agregação não adicionar valor ou clareza, é melhor evitá-la.
  - Mantenha o modelo o mais simples possível.

- **Alternativas Mais Simples**

  - Às vezes, uma entidade associativa simples resolve o problema.
  - Avalie se a agregação é realmente necessária.

---

### **Entidades Associativas**

  As **Entidades Associativas** quando um **relacionamento precisa se relacionar com outro relacionamento**. Nesse caso, o relacionamento é elevado ao status de entidade para que possa:

  - **Armazenar atributos próprios:** Quando o relacionamento em si possui informações adicionais que precisam ser registradas.
  - **Participar de outros relacionamentos:** Quando o relacionamento precisa se conectar com outras entidades ou relacionamentos no modelo.
  - **Representar um conceito importante:** Quando o relacionamento é significativo no domínio do problema e precisa ser tratado como uma entidade independente.

  Isso permite uma modelagem mais rica e precisa dos dados, especialmente em situações complexas.

- **Exemplos:**

  1. **Atendimento** como Entidade Associativa entre **Paciente** e **Médico**, que se relaciona com **Hospital**:

     - **Contexto:** Um paciente é atendido por um médico. O atendimento possui atributos como data, horário, diagnóstico, e precisa se relacionar com o hospital onde ocorreu.
     - **Como é modelado:**
       - **Entidades Principais:** `Paciente` e `Médico`.
       - **Relacionamento Original:** `AtendidoPor`.
       - **Entidade Associativa:** `Atendimento`, criada a partir do relacionamento `AtendidoPor`, com atributos próprios.
       - **Relacionamento Adicional:** `Atendimento` se relaciona com `Hospital`.

     ![Exemplo de Entidade Associativa - Atendimento](./assets/atendimento-entidade-associativa.png)

  2. **Transação** como Entidade Associativa entre **Conta Bancária** e **Operação**, que se relaciona com **Funcionário**:

     - **Contexto:** Uma conta bancária realiza operações financeiras (depósito, saque, transferência). Cada transação possui atributos como valor, data, e precisa se relacionar com o funcionário que a autorizou.
     - **Como é modelado:**
       - **Entidades Principais:** `Conta Bancária` e `Operação`.
       - **Relacionamento Original:** `Realiza`.
       - **Entidade Associativa:** `Transação`, com atributos como `valor`, `data`.
       - **Relacionamento Adicional:** `Transação` se relaciona com `Funcionário`.

  3. **Contrato** como Entidade Associativa entre **Empresa** e **Fornecedor**, que se relaciona com **Produto**:

     - **Contexto:** Uma empresa firma contratos com fornecedores. O contrato possui atributos como valor total, prazo, e precisa se relacionar com os produtos fornecidos.
     - **Como é modelado:**
       - **Entidades Principais:** `Empresa` e `Fornecedor`.
       - **Relacionamento Original:** `Firma`.
       - **Entidade Associativa:** `Contrato`, com atributos como `valorTotal`, `prazo`.
       - **Relacionamento Adicional:** `Contrato` se relaciona com `Produto`.

  4. **Reserva** como Entidade Associativa entre **Cliente** e **Voo**, que se relaciona com **Pagamento**:

     - **Contexto:** Um cliente faz reservas em voos. A reserva possui atributos como número de assento, classe, e precisa se relacionar com o pagamento efetuado.
     - **Como é modelado:**
       - **Entidades Principais:** `Cliente` e `Voo`.
       - **Relacionamento Original:** `Reserva`.
       - **Entidade Associativa:** `Reserva`, com atributos como `assento`, `classe`.
       - **Relacionamento Adicional:** `Reserva` se relaciona com `Pagamento`.

  5. **Pedido** como Entidade Associativa entre **Cliente** e **Vendedor**, que se relaciona com **Produto** e **Entrega**:

     - **Contexto:** Um cliente faz um pedido a um vendedor. O pedido possui atributos como data, valor total, e precisa se relacionar com os produtos vendidos e a entrega.
     - **Como é modelado:**
       - **Entidades Principais:** `Cliente` e `Vendedor`.
       - **Relacionamento Original:** `FazPedido`.
       - **Entidade Associativa:** `Pedido`, com atributos como `data`, `valorTotal`.
       - **Relacionamentos Adicionais:** `Pedido` se relaciona com `Produto` e `Entrega`.

- **Dicas de Boas Práticas:**
  
  - **Relacionamentos entre Relacionamentos:**
    - Quando um relacionamento precisa se relacionar com outra entidade ou relacionamento, utilize uma entidade associativa para permitir essa conexão.
  
  - **Clareza na Modelagem:**
    - Nomeie a entidade associativa de forma que reflita claramente seu propósito no modelo.
    - Mantenha a consistência na representação gráfica para facilitar a compreensão.

- **Representação Visual no DER:**

  - **Entidade Associativa:**
    - Representada por um **retângulo**, como outras entidades.
    - Conectada às entidades originais através de relacionamentos.
  
  - **Relacionamentos Adicionais:**
    - A entidade associativa pode participar de novos relacionamentos com outras entidades ou até mesmo com outros relacionamentos transformados em entidades.
  
  - **Exemplo Genérico:**

    ![Representação Visual no DER](./assets/atendimento-entidade-associativa.png)

---

### **Especialização e Generalização**

No modelo de banco de dados, **especialização** e **generalização** são técnicas usadas para organizar e simplificar a estrutura dos dados. Elas ajudam a representar situações em que algumas entidades (tabelas) compartilham características comuns, mas também têm diferenças específicas. Esses conceitos são como criar uma "família" de entidades, onde algumas são mais genéricas (pais) e outras são mais específicas (filhos).

#### **O que é Generalização?**

**Generalização** é o processo de identificar características comuns em duas ou mais entidades específicas e criar uma entidade mais genérica que as engloba. Pense nisso como subir um nível para criar uma categoria mais ampla que abrange todas as entidades menores.

- **Imagine que você está agrupando coisas parecidas em uma única categoria maior.**

##### **Exemplos Práticos de Generalização:**

1. **Animais Domésticos: Cachorro e Gato**

   - **Entidades Específicas:**
     - **Cachorro**: Tem atributos como raça, tamanho, necessidade de exercícios.
     - **Gato**: Tem atributos como pelagem, independência, preferência por ambientes.
   - **Características em Comum:**
     - Ambos são animais domésticos, têm nome, idade, dono, precisam de alimentação.
   - **Entidade Generalizada:**
     - **Animal Doméstico**: Cria-se uma entidade que contém os atributos comuns.
   - **Como Funciona:**
     - **Cachorro** e **Gato** se tornam entidades que herdam de **Animal Doméstico**.
  
2. **Veículos: Carro e Bicicleta**

   - **Entidades Específicas:**
     - **Carro**: Possui motor, número de portas, tipo de combustível.
     - **Bicicleta**: Tem número de marchas, tipo de freio.
   - **Características em Comum:**
     - Ambos são meios de transporte, têm marca, modelo, cor.
   - **Entidade Generalizada:**
     - **Veículo**: Contém os atributos comuns.
   - **Como Funciona:**
     - **Carro** e **Bicicleta** herdam de **Veículo** e mantêm seus atributos específicos.

3. **Funcionários: Professor e Administrador**

   - **Entidades Específicas:**
     - **Professor**: Disciplina que leciona, carga horária.
     - **Administrador**: Departamento, nível de acesso.
   - **Características em Comum:**
     - Ambos têm nome, CPF, salário, data de contratação.
   - **Entidade Generalizada:**
     - **Funcionário**: Agrupa os atributos comuns.
   - **Como Funciona:**
     - **Professor** e **Administrador** herdam de **Funcionário**.

#### **O que é Especialização?**

**Especialização** é o tudo aquilo que não tem valor compartilhado com outras entidades. São as caracteristicas únicas de um subtipo.

- **É como pegar uma categoria grande e dividi-la em partes menores com características únicas.**

##### **Exemplos Práticos de Especialização:**

1. **Pessoa sendo especializada em Aluno e Professor**

   - **Entidade Geral:**
     - **Pessoa**: Tem atributos como nome, endereço, telefone.
   - **Entidades Específicas:**
     - **Aluno**: Tem número de matrícula, curso.
     - **Professor**: Tem número de registro, disciplina que leciona.
   - **Como Funciona:**
     - **Aluno** e **Professor** herdam de **Pessoa** e adicionam seus próprios atributos.

2. **Conta Bancária sendo especializada em Conta Corrente e Conta Poupança**

   - **Entidade Geral:**
     - **Conta Bancária**: Número da conta, agência, saldo.
   - **Entidades Específicas:**
     - **Conta Corrente**: Limite de cheque especial.
     - **Conta Poupança**: Taxa de rendimento.
   - **Como Funciona:**
     - **Conta Corrente** e **Conta Poupança** herdam de **Conta Bancária**.

3. **Produto sendo especializado em Produto Digital e Produto Físico**

   - **Entidade Geral:**
     - **Produto**: Código, nome, preço.
   - **Entidades Específicas:**
     - **Produto Digital**: Formato do arquivo, tamanho em MB.
     - **Produto Físico**: Peso, dimensões, estoque.
   - **Como Funciona:**
     - **Produto Digital** e **Produto Físico** herdam de **Produto**.

##### **Como Representar no Diagrama (DER):**

- A generalização é representada por um **triângulo** que conecta as entidades específicas à entidade geral.
- O triângulo aponta para a entidade geral (a categoria mais ampla).

  ![Exemplo de Generalização - Animais Domésticos](./assets/generalizacao-animais.png)


#### **Tipos de Generalização e Especialização**
Existem tipos diferentes de generalização e especialização que podem ser aplicados dependendo do contexto do modelo de dados. Elas ajudam a manter a consistência dos dados e evitar repetições desnecessárias,  garantindo que as entidades sejam organizadas de forma lógica e eficiente.

1. **Generalização Total e Parcial**

   - **Generalização Total**: Todos os subtipos são obrigados a participar da generalização.
   - **Generalização Parcial**: Alguns subtipos podem não participar da generalização.
  
2. **Especialização Exclusiva e Não Exclusiva**
  
   - **Especialização Exclusiva**: Um subtipo só pode ser de um tipo específico.
   - **Especialização Não Exclusiva**: Um subtipo pode ser de mais de um tipo.

Sabendo disso, há combinações de generalização e especialização que podem ser representadas no DER com um parenteses com "(generalização, especialização)". Por exemplo:
- **Total Exclusiva -> (T, E):** Todos os subtipos são obrigados a participar da generalização e um subtipo só pode ser de um tipo específico, não podendo ser de mais de um tipo.
  Exemplo: **Animal** sendo generalizada em **Cachorro** e **Gato**. Um Animal não pode ser um Cachorro e um Gato ao mesmo tempo.

- **Parcial Exclusiva -> (P, E):** Alguns subtipos podem não participar da generalização e um subtipo só pode ser de um tipo específico, não podendo ser de mais de um tipo.
  Exemplo: **Veículo** sendo generalizada em **Carro** e **Bicicleta**. Alguns Veículos podem ser Carros ou Bicicletas, mas não ambos. Além disso, como a Generalização é Parcial, pode ter veículos que não são nem Carros nem Bicicletas, algo que não foi definido ainda.

- **Total Não Exclusiva -> (T, NE):** Todos os subtipos são obrigados a participar da generalização e um subtipo pode ser de mais de um tipo.
  Exemplo: **Pessoa** sendo generalizada em **Aluno** e **Professor**. Uma Pessoa deve ser um Aluno ou um Professor nesse exemplo. Ela não pode existir se não for um dos dois. Porém, como é uma especialização não exclusiva, uma Pessoa pode ser um Aluno e um Professor ao mesmo tempo.

- **Parcial Não Exclusiva -> (P, NE):** Alguns subtipos podem não participar da generalização e um subtipo pode ser de mais de um tipo.
  Exemplo: **Conta Bancária** possui atributos gerais. O usuário pode ter somente essa **Conta Bancária**, ou pode ter uma **Conta Corrente**, **Conta Poupança**, **Conta Salário**, outros tipos de conta, tudo dentro da mesma **Conta Bancária**.

#### **Como Transformar em Tabelas**
##### **1. Tabela Única para Todas as Entidades (Single Table Inheritance)**

- **Descrição:**
  - Criar uma única tabela que inclui todos os atributos da entidade geral e das entidades específicas.
  - Usar uma coluna extra para indicar o tipo de cada registro.
- **Vantagens:**
  - Simplicidade na estrutura do banco.
  - Fácil de consultar todos os registros.
- **Desvantagens:**
  - Muitos campos podem ficar vazios (nulos) se não forem aplicáveis a todos os registros.
  - Pode ficar confuso se houver muitas entidades específicas.

- **Exemplo Prático:**

  - **Tabela:** `Pessoa`
    - `pessoa_id` (PK)
    - `nome`
    - `endereco`
    - `telefone`
    - `tipo_pessoa` (indica se é "Aluno" ou "Professor")
    - **Atributos de Aluno:**
      - `numero_matricula`
      - `curso`
    - **Atributos de Professor:**
      - `numero_registro`
      - `disciplina`

##### **2. Tabelas Separadas com Herança (Class Table Inheritance)**

- **Descrição:**
  - Criar uma tabela para a entidade geral e tabelas separadas para cada entidade específica.
  - As tabelas específicas têm uma chave estrangeira que referencia a tabela geral.
- **Vantagens:**
  - Dados organizados de forma clara.
  - Evita campos nulos.
- **Desvantagens:**
  - Requer junções (joins) nas consultas para obter dados completos.
  - Estrutura mais complexa.

- **Exemplo Prático:**

  - **Tabela Geral:** `Pessoa`
    - `pessoa_id` (PK)
    - `nome`
    - `endereco`
    - `telefone`

  - **Tabela Específica:** `Aluno`
    - `pessoa_id` (PK, FK para `Pessoa`)
    - `numero_matricula`
    - `curso`

  - **Tabela Específica:** `Professor`
    - `pessoa_id` (PK, FK para `Pessoa`)
    - `numero_registro`
    - `disciplina`

##### **3. Tabelas Separadas sem Herança (Concrete Table Inheritance)**

- **Descrição:**
  - Criar tabelas separadas para cada entidade específica, incluindo os atributos da entidade geral.
  - Não há tabela para a entidade geral.
- **Vantagens:**
  - Consultas mais simples (não requer joins).
- **Desvantagens:**
  - Duplicação de dados comuns.
  - Dificuldade em manter a consistência dos dados comuns.

- **Exemplo Prático:**

  - **Tabela:** `Aluno`
    - `aluno_id` (PK)
    - `nome`
    - `endereco`
    - `telefone`
    - `numero_matricula`
    - `curso`

  - **Tabela:** `Professor`
    - `professor_id` (PK)
    - `nome`
    - `endereco`
    - `telefone`
    - `numero_registro`
    - `disciplina`

#### **Qual a melhor opção para cada tipo de Generalização e Especialização?**

##### 1. **Total e Exclusiva (T,E)**
   - **Descrição**: Todos os subtipos participam da generalização, e cada subtipo pode pertencer a apenas um tipo.
   - **Melhor abordagem**: **Class Table Inheritance (Tabelas Separadas com Herança)**
     - **Por quê?**: Como todos os subtipos são obrigatórios e mutuamente exclusivos, é vantajoso ter uma tabela separada para cada subtipo, ligada à tabela da entidade geral. Isso evita campos nulos, mantém as entidades específicas separadas e facilita a integridade referencial.
     - **Exemplo**:
       - **Tabela Geral:** `Animal`
         - `animal_id` (PK)
         - `nome`
         - `idade`
       - **Tabela Específica:** `Cachorro`
         - `animal_id` (PK, FK para `Animal`)
         - `raça`
         - `tamanho`
       - **Tabela Específica:** `Gato`
         - `animal_id` (PK, FK para `Animal`)
         - `pelagem`
         - `independência`

##### 2. **Total e Não Exclusiva (T,NE)**
   - **Descrição**: Todos os subtipos participam da generalização, mas um subtipo pode pertencer a mais de uma categoria.
   - **Melhor abordagem**: **Single Table Inheritance (Tabela Única para Todas as Entidades)**
     - **Por quê?**: Como todos os subtipos são obrigatórios, mas um registro pode pertencer a múltiplos subtipos, uma tabela única com uma coluna para indicar o tipo (ou tipos) é a abordagem mais eficiente. Isso evita a necessidade de junções complexas e permite uma consulta direta.
     - **Exemplo**:
       - **Tabela:** `Pessoa`
         - `pessoa_id` (PK)
         - `nome`
         - `endereço`
         - `telefone`
         - `tipo_pessoa` (pode ser "Aluno", "Professor" ou ambos)
         - Atributos específicos de `Aluno` e `Professor` nas colunas correspondentes, como `numero_matricula` e `disciplina`.

##### 3. **Parcial e Exclusiva (P,E)**
   - **Descrição**: Nem todos os subtipos precisam participar da generalização, e cada subtipo pode pertencer a apenas uma categoria.
   - **Melhor abordagem**: **Concrete Table Inheritance (Tabelas Separadas sem Herança)**
     - **Por quê?**: Como nem todos os subtipos participam e são exclusivos, criar tabelas separadas sem herança pode ser mais direto. Isso evita a necessidade de uma tabela geral e simplifica o design, já que as entidades não compartilhadas não precisam de uma tabela comum.
     - **Exemplo**:
       - **Tabela:** `Conta Corrente`
         - `conta_id` (PK)
         - `numero_conta`
         - `saldo`
         - `limite_cheque_especial`
       - **Tabela:** `Conta Poupança`
         - `conta_id` (PK)
         - `numero_conta`
         - `saldo`
         - `taxa_rendimento`
     - **Observação**: As tabelas de `Conta Corrente` e `Conta Poupança` podem existir separadamente, sem a necessidade de uma tabela geral de `Conta Bancária`.

##### 4. **Parcial e Não Exclusiva (P,NE)**
   - **Descrição**: Nem todos os subtipos participam da generalização, e um subtipo pode pertencer a mais de uma categoria.
   - **Melhor abordagem**: **Class Table Inheritance (Tabelas Separadas com Herança)**
     - **Por quê?**: Aqui, os subtipos podem não participar da generalização, mas quando o fazem, podem pertencer a várias categorias. O uso de tabelas separadas permite modelar essa flexibilidade sem redundâncias excessivas. Relacionamentos muitos-para-muitos podem ser geridos com tabelas de junção.
     - **Exemplo**:
       - **Tabela Geral:** `Produto`
         - `produto_id` (PK)
         - `nome`
         - `preço`
       - **Tabela Específica:** `Produto Digital`
         - `produto_id` (PK, FK para `Produto`)
         - `formato`
         - `tamanho_MB`
       - **Tabela Específica:** `Produto Físico`
         - `produto_id` (PK, FK para `Produto`)
         - `peso`
         - `dimensões`
       - Uma mesma instância de `Produto` pode estar presente nas duas tabelas específicas ao mesmo tempo, caso seja necessário.

##### Resumo das Melhores Abordagens:

| **Tipo**  | **Abordagem Recomendada**                         |
|-----------|---------------------------------------------------|
| **(T,E)** | Class Table Inheritance (Tabelas Separadas com Herança) |
| **(T,NE)**| Single Table Inheritance (Tabela Única)           |
| **(P,E)** | Concrete Table Inheritance (Tabelas Separadas sem Herança) |
| **(P,NE)**| Class Table Inheritance (Tabelas Separadas com Herança) |