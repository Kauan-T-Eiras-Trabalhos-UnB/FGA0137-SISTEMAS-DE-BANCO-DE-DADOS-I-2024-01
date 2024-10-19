# **Normalização no Banco de Dados**

A **normalização** é o processo de organizar os dados de um banco de dados para minimizar a redundância e melhorar a integridade dos dados. O objetivo é garantir que as tabelas estejam estruturadas de maneira eficiente, evitando a duplicação de informações e problemas de anomalias durante operações de **inserção**, **atualização**, e **remoção**.

O processo de normalização segue uma série de etapas chamadas de **Formas Normais** (Normal Forms). Cada forma normal possui um conjunto de regras que as tabelas devem seguir. O banco de dados passa por uma série de transformações para atender a essas regras e se ajustar às formas normais mais elevadas, garantindo uma estrutura mais eficiente e robusta.

## **Formas Normais e Como Verificá-las**:

### **Primeira Forma Normal (1FN)**

#### **Regras**:
1. Atributos com **valores compostos** devem ser transformados em **valores atômicos**, ou seja, cada célula da tabela deve conter **apenas um valor** (não pode haver listas ou conjuntos de valores em uma única célula).

Exemplo de tabela não normalizada:
| Cliente | Endereço |
|---------|----------|
| Ana     | Rua A, 123, Bairro X, Cidade Y, 73770-000|

**Problema**: O atributo **Endereço** contém vários valores (Rua, Número, Bairro, Cidade, CEP) em uma única célula, violando a 1FN.

**Correção para 1FN**: Separe os valores em colunas distintas.

| Cliente | Rua    | Número | Bairro | Cidade | CEP      |
|---------|--------|--------|--------|--------|----------|
| Ana     | Rua A  | 123    | Bairro X | Cidade Y | 73770-000|

2. Atributos Multivalorados devem ser transformados em **tabelas separadas**. 
   
Exemplo de tabela não normalizada:
| id_cliente | Cliente | Telefones |
|----|---------|-----------|
| 1  | Ana     | 123456789 |
| 1  | Ana     | 987654321 |
| 2  | João    | 111111111 |
| 2  | João    | 222222222 |
| 2  | João    | 333333333 |

**Problema**: O atributo **Telefones** contém vários números de telefone para um mesmo cliente em várias linhas, o que não é ideal. O problema com essa estrutura é que ela pode resultar em redundâncias e inconsistências.

#### **Correção para 1FN**: Crie uma tabela separada para armazenar os números de telefone de cada cliente, relacionando-os com a tabela de clientes.

##### Tabela de **Clientes**:
| id_cliente | Cliente |  
|------------|---------|  
| 1          | Ana     |  
| 2          | João    |  

##### Tabela de **Telefones**:
| id_telefone | id_cliente | Telefone  |
|-------------|------------|-----------|
| 101         | 1          | 123456789 |
| 102         | 1          | 987654321 |
| 103         | 2          | 111111111 |
| 104         | 2          | 222222222 |
| 105         | 2          | 333333333 |

Agora, os números de telefone estão separados em uma tabela diferente, com uma relação clara com os clientes, eliminando o problema de valores multivalorados.

---

### **Segunda Forma Normal (2FN)**

#### **Regras**:
1. A tabela deve estar em **1FN**.
2. Todos os atributos não-chave devem depender **completamente** da chave primária. Não pode haver dependência parcial de atributos em relação a uma chave composta.

#### Exemplo de tabela não normalizada (dependência parcial):
| ID_Pedido | ID_Produto | Nome_Produto | Quantidade | Data_Pedido |
|-----------|------------|--------------|------------|-------------|
| 1         | 101        | Teclado      | 2          | 01/09/2023  |
| 1         | 102        | Mouse        | 1          | 01/09/2023  |
| 2         | 101        | Teclado      | 1          | 05/09/2023  |

**Problema**: O atributo **Nome_Produto** depende apenas de **ID_Produto**, e não da chave composta inteira (**ID_Pedido** e **ID_Produto**), o que gera uma dependência parcial, violando a 2FN.

#### **Correção para 2FN**: Separe as informações de produtos em uma tabela distinta.

##### Tabela de **Pedidos**:
| ID_Pedido | Data_Pedido |
|-----------|-------------|
| 1         | 01/09/2023  |
| 2         | 05/09/2023  |

##### Tabela de **Produtos**:
| ID_Produto | Nome_Produto |
|------------|--------------|
| 101        | Teclado      |
| 102        | Mouse        |

##### Tabela de **Detalhes do Pedido**:
| ID_Pedido | ID_Produto | Quantidade |
|-----------|------------|------------|
| 1         | 101        | 2          |
| 1         | 102        | 1          |
| 2         | 101        | 1          |

Agora, os atributos não-chave (como **Nome_Produto**) dependem da chave correta, e não de apenas parte dela.

---

### **Terceira Forma Normal (3FN)**

#### **Regras**:
1. A tabela deve estar em **2FN**.
2. Nenhum atributo não-chave deve depender de outro atributo não-chave. Todos os atributos não-chave devem depender **somente da chave primária**. Isso elimina **dependências transitivas**.

#### Exemplo de tabela não normalizada (dependência transitiva):
| ID_Cliente | Nome_Cliente | ID_Cidade | Nome_Cidade |  
|------------|--------------|-----------|-------------|  
| 1          | Ana          | 123       | São Paulo   |  
| 2          | João         | 124       | Rio de Janeiro |  

**Problema**: O atributo **Nome_Cidade** depende de **ID_Cidade**, que não é a chave primária. Isso cria uma dependência transitiva, violando a 3FN.

#### **Correção para 3FN**: Separe as informações de cidade em uma tabela distinta.

##### Tabela de **Clientes**:
| ID_Cliente | Nome_Cliente | ID_Cidade |
|------------|--------------|-----------|
| 1          | Ana          | 123       |
| 2          | João         | 124       |

##### Tabela de **Cidades**:
| ID_Cidade  | Nome_Cidade   |
|------------|---------------|
| 123        | São Paulo     |
| 124        | Rio de Janeiro|

Agora, todos os atributos não-chave dependem apenas da chave primária, e as dependências transitivas foram eliminadas.

---

### **Forma Normal de Boyce-Codd (BCNF)**

A **BCNF** é uma versão mais rigorosa da 3FN. Uma tabela pode estar na 3FN, mas ainda violar a BCNF, se houver uma dependência funcional onde o determinante (o atributo que determina outro atributo) **não é uma chave candidata**.

#### **Regras da BCNF**:
1. A tabela deve estar em **3FN**.
2. Para cada **dependência funcional**, o determinante deve ser uma **chave candidata**.

### **Exemplo prático** para explicar melhor:

Vamos considerar uma tabela que armazena informações sobre **professores**, **disciplinas** e **salas de aula**. Imagine que temos a seguinte tabela:

| Professor | Disciplina | Sala  |
|-----------|------------|-------|
| João      | Matemática | A101  |
| Maria     | Física     | B202  |
| João      | Física     | A101  |
| Maria     | Matemática | B202  |

A **dependência funcional** que temos é: 
- **Professor** → **Sala** (ou seja, dado o professor, você sabe em qual sala ele leciona).

### **Problema**:
A dependência funcional **Professor → Sala** não é uma dependência entre chaves candidatas, pois:
- A chave primária ideal da tabela seria a combinação de **Professor** e **Disciplina**, já que cada professor pode lecionar várias disciplinas, e cada disciplina pode ser lecionada por diferentes professores.
- No entanto, o professor **determina** a sala, mas o professor sozinho **não é** uma chave candidata. Isso cria uma **violação da BCNF**.

### **Correção para BCNF**:
A solução é **dividir a tabela** em duas, para separar as informações sobre as dependências de professor e sala de aula. Isso resolve a dependência onde o professor determina a sala, mas sem que essa dependência crie problemas no relacionamento com as disciplinas.

#### Tabela de **Professores e Salas**:
| Professor | Sala  |
|-----------|-------|
| João      | A101  |
| Maria     | B202  |

#### Tabela de **Disciplinas e Professores**:
| Disciplina  | Professor |
|-------------|-----------|
| Matemática  | João      |
| Física      | Maria     |
| Física      | João      |
| Matemática  | Maria     |

Agora, temos:
1. **Professor → Sala** na tabela "Professores e Salas", que é válida, pois **Professor** é a chave primária aqui.
2. **Disciplina → Professor** na tabela "Disciplinas e Professores", sem a dependência transitiva de sala.

---

### Outro exemplo:

Vamos imaginar um cenário em que uma empresa registra quais **funcionários** trabalham em quais **projetos** e quem é o **gerente** de cada projeto.

| Funcionário | Projeto  | Gerente |
|-------------|----------|---------|
| Ana         | ProjetoX | Carlos  |
| Bruno       | ProjetoY | Alice   |
| Ana         | ProjetoY | Alice   |
| Bruno       | ProjetoX | Carlos  |

#### Dependências Funcionais:
- **Projeto → Gerente**: Dado o projeto, sabemos quem é o gerente responsável.
- A chave primária seria a combinação de **Funcionário** e **Projeto**.

### **Problema**:
Aqui, o projeto determina o gerente, mas o projeto sozinho não é uma chave candidata, já que a chave candidata é a combinação de **Funcionário** e **Projeto**. Isso cria uma violação da BCNF.

### **Correção para BCNF**:
Divida a tabela em duas, separando a dependência entre **Projeto** e **Gerente**.

#### Tabela de **Projetos e Gerentes**:
| Projeto  | Gerente |
|----------|---------|
| ProjetoX | Carlos  |
| ProjetoY | Alice   |

#### Tabela de **Funcionários e Projetos**:
| Funcionário | Projeto  |
|-------------|----------|
| Ana         | ProjetoX |
| Bruno       | ProjetoY |
| Ana         | ProjetoY |
| Bruno       | ProjetoX |

Agora:
1. **Projeto → Gerente** está em sua própria tabela, e o projeto é a chave primária.
2. **Funcionário → Projeto** é mantido na tabela "Funcionários e Projetos", sem violar a BCNF.

---

### **Quarta Forma Normal (4FN)**

A **Quarta Forma Normal (4FN)** trata especificamente de dependências multivaloradas, um tipo de anomalia que pode ocorrer em tabelas quando um atributo depende de outro, mas sem que haja uma relação direta entre os outros atributos da tabela. O objetivo da 4FN é garantir que, se houver múltiplos valores possíveis para um atributo, esses valores sejam representados de forma independente, sem gerar redundância.

#### **Regras da 4FN**:
1. A tabela deve estar em **BCNF**.
2. Não deve haver **dependências multivaloradas**, o que significa que cada tabela deve conter apenas uma relação entre os atributos.


#### **Dependências multivaloradas:**
Uma **dependência multivalorada** ocorre quando, para um determinado valor de um atributo, há múltiplos valores possíveis de outro atributo, e esses valores não estão diretamente relacionados a outros atributos da tabela.

### **Exemplo de tabela não normalizada (violação da 4FN)**:

Vamos usar uma tabela que armazena informações sobre **produtos**, **fornecedores**, e **lojas**. Suponha que diferentes produtos podem ser fornecidos por diferentes fornecedores e vendidos em diferentes lojas. Cada produto pode ter mais de um fornecedor e ser vendido em várias lojas.

| Produto   | Fornecedor | Loja       |
|-----------|------------|------------|
| Laptop    | FornA      | Loja1      |
| Laptop    | FornB      | Loja1      |
| Laptop    | FornA      | Loja2      |
| Laptop    | FornB      | Loja2      |
| Smartphone| FornC      | Loja1      |
| Smartphone| FornD      | Loja2      |
| Tablet    | FornA      | Loja3      |
| Tablet    | FornC      | Loja3      |

#### **Problema**:
A tabela acima tem uma dependência multivalorada entre **Produto → Fornecedor** e **Produto → Loja**. Os fornecedores e as lojas não dependem diretamente um do outro, mas ambos dependem do produto. Essa estrutura leva à duplicação de dados, pois estamos repetindo informações sobre fornecedores e lojas para cada combinação, o que pode gerar anomalias de atualização e inconsistências.

#### **Correção para 4FN**: Dividir a tabela em duas, separando as dependências multivaloradas de **Produto → Fornecedor** e **Produto → Loja** em tabelas distintas.

#### Tabela de **Produtos e Fornecedores**:
| Produto    | Fornecedor |
|------------|------------|
| Laptop     | FornA      |
| Laptop     | FornB      |
| Smartphone | FornC      |
| Smartphone | FornD      |
| Tablet     | FornA      |
| Tablet     | FornC      |

#### Tabela de **Produtos e Lojas**:
| Produto    | Loja  |
|------------|-------|
| Laptop     | Loja1 |
| Laptop     | Loja2 |
| Smartphone | Loja1 |
| Smartphone | Loja2 |
| Tablet     | Loja3 |

Agora, a relação entre **Produto e Fornecedor** está separada da relação entre **Produto e Loja**, eliminando a redundância e as dependências multivaloradas.

---

### **Como verificar se uma tabela está em 4FN**:
1. A tabela deve estar em **BCNF**.
2. Verifique se há **dependências multivaloradas**, onde um atributo tem múltiplos valores dependentes de outro atributo, mas os outros atributos na tabela não estão diretamente relacionados a esses valores.
3. Se houver dependências multivaloradas, divida a tabela em duas, separando cada dependência em sua própria tabela.