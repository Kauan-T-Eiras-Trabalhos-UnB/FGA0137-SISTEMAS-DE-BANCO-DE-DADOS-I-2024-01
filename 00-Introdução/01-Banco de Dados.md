# Sistema de Banco de Dados

## Definição e Importância

Um **banco de dados (BD)** é uma coleção organizada de dados que serve a um propósito específico. Eles fornecem informações estruturadas e organizadas, facilitando a busca e manipulação de grandes volumes de dados.

Os bancos de dados são essenciais em várias áreas como negócios, educação, medicina e muitos outros setores que precisam de organização e consulta eficiente de informações.

### Características dos Bancos de Dados

- **Dados logicamente coerentes**: Os dados armazenados devem fazer sentido em conjunto, formando informações úteis.
- **Propósito específico**: Cada banco de dados é projetado para resolver um problema ou atender uma necessidade específica.
- **Reflexo da realidade**: O banco de dados reflete uma parte do mundo real, como as informações de uma empresa ou de uma escola.
- **Metadados**: Além dos dados em si, um banco de dados também armazena descrições sobre a estrutura dos dados, chamados de **metadados**.

## Níveis de Abstração dos Bancos de Dados

Os bancos de dados utilizam três níveis de abstração para fornecer uma visão clara dos dados aos usuários:

![Níveis de Abstração](../assets/niveis-de-abstracao.png)

### 1. **Nível Externo: Visão dos Dados para o Usuário**
No nível externo, o foco é na apresentação dos dados para diferentes usuários ou aplicações. Aqui temos o resultado final, onde o usuário ou aplicação vê tabelas, consultas e resultados.

Por exemplo, quando um usuário faz uma consulta SQL para buscar ou modificar dados, ele vê um resultado estruturado:

```sql
SELECT Título, Autor FROM Livros WHERE Categoria = 'Fantasia';
```

O banco de dados retorna uma tabela como resultado da consulta:

| **Título**        | **Autor**       | **Categoria** | **Ano** |
|-------------------|-----------------|---------------|---------|
| O Hobbit          | J.R.R. Tolkien  | Fantasia      | 1937    |
| Harry Potter      | J.K. Rowling    | Fantasia      | 1997    |

### 2. **Nível Conceitual: Estrutura Lógica Completa**
No nível conceitual, é definida a **estrutura completa dos dados** e seus relacionamentos, independentemente de como são fisicamente armazenados.

- **Modelo Entidade-Relacionamento (MER)**: Um MER é utilizado para representar entidades como "Livros", "Autores" e "Categorias" e seus relacionamentos. Depois, ele é transformado em um **Diagrama Entidade-Relacionamento (DER)**, que mostra graficamente esses elementos.

![exemplo de DER](../assets/DER-exemplo.png)

- **Modelo Lógico**: A partir do DER, criamos o modelo lógico que transforma as entidades e seus relacionamentos em tabelas de banco de dados. Por exemplo:
  - Tabela "Livros" com colunas "Título", "AutorID", "CategoriaID".
  - Tabela "Autores" com colunas "AutorID", "Nome".

- **Definições SQL**: Para definir essas tabelas usamos a Linguagem de Definição de Dados (DDL):

  ```sql
  CREATE TABLE Livros (
    ID SERIAL PRIMARY KEY,
    Título VARCHAR(100),
    AutorID INT REFERENCES Autores(AutorID),
    CategoriaID INT REFERENCES Categorias(CategoriaID)
  );
  ```

### 3. **Nível Interno: Armazenamento Físico dos Dados**
No nível interno, é mostrado como os dados são armazenados fisicamente no disco. É aqui onde os detalhes técnicos, como estruturas de arquivos e índices, são definidos. Geralmente não nos preocupamos com esse nível no dia a dia, pois é mais técnico.

## Linguagens de Banco de Dados
Para manipular os dados e a estrutura dos bancos de dados, usamos linguagens específicas. A principal linguagem utilizada é o **SQL** (Structured Query Language). Ela possui diferentes tipos de comandos, cada um com uma função específica.

### 1. **DDL (Data Definition Language) - Linguagem de Definição de Dados**
A **DDL** é usada para **criar, alterar ou apagar** a estrutura do banco de dados. Pense nela como o "construtor" do banco de dados, definindo tabelas, colunas e outras estruturas.

- **Exemplos de comandos DDL**:
  - **CREATE**: Cria novas tabelas ou bancos de dados.
    ```sql
    CREATE TABLE Livros (
      ID INT PRIMARY KEY,
      Título VARCHAR(100),
      Autor VARCHAR(50)
    );
    ```
  - **ALTER**: Altera a estrutura de uma tabela existente.
    ```sql
    ALTER TABLE Livros ADD AnoPublicacao INT;
    ```
  - **DROP**: Apaga uma tabela ou banco de dados.
    ```sql
    DROP TABLE Livros;
    ```

### 2. **DML (Data Manipulation Language) - Linguagem de Manipulação de Dados**
A **DML** é usada para **manipular os dados** dentro das tabelas. Isso inclui **inserir, atualizar, apagar e consultar** os dados.

- **Exemplos de comandos DML**:
  - **INSERT**: Insere novos registros em uma tabela.
    ```sql
    INSERT INTO Livros (ID, Título, Autor) VALUES (1, 'O Hobbit', 'J.R.R. Tolkien');
    ```
  - **UPDATE**: Atualiza registros existentes.
    ```sql
    UPDATE Livros SET Autor = 'J.R.R. Tolkien' WHERE ID = 1;
    ```
  - **DELETE**: Apaga registros específicos.
    ```sql
    DELETE FROM Livros WHERE ID = 1;
    ```

### 3. **DQL (Data Query Language) - Linguagem de Consulta de Dados**
A **DQL** é usada para **consultar e obter informações** do banco de dados. O comando principal é o **SELECT**.

- **Exemplo de comando DQL**:
  - **SELECT**: Consulta dados de uma ou mais tabelas.
    ```sql
    SELECT Título, Autor FROM Livros WHERE Categoria = 'Fantasia';
    ```

### Resumo Simples
- **DDL**: Cria ou altera a estrutura do banco (construtor).
- **DML**: Manipula os dados dentro das tabelas (manipulador).
- **DQL**: Consulta os dados existentes (pesquisador).

## Conclusão
Os bancos de dados são ferramentas essenciais para organizar e acessar dados de forma eficiente. Usamos diferentes níveis de abstração para facilitar o entendimento dos dados e linguagens como SQL para manipulá-los de forma adequada. Esses conceitos são a base para projetos de sistemas que lidam com informações no nosso dia a dia, sejam eles pequenos ou grandes.

## Bibliografia

### Básica
ELMASRI, R. e NAVATHE, S. B. Sistemas de Banco de Dados, 6a. ed., Pearson, 2011.  
PRAMOD, J. S. and MARTIN, F. NoSQL Distilled: A Brief Guide to the Emerging World of Polyglot Persistence, 2013.  
PRABHU, S. and VENKATESAN, N. Data Mining and Warehousing. New Age International, 2006. [EBRARY]

### Complementar
DATE, C. J. Introdução a Sistemas de Bancos de Dados, 8a. Ed., Campus, 2004.  
KRISHNAN, K. The Morgan Kaufmann Series on Business Intelligence: Data Warehousing in the Age of Big Data. Morgan Kaufmann, 2013. [EBRARY]

