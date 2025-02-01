**Links Úteis**  
- [SQL Tutorial  |  Cheat Sheet](https://www.sqltutorial.org/)  
- [Practice SQL  |  Exercises](https://www.sql-practice.com)  
- [SQL Easy  |  Exercises](https://www.sql-easy.com)
- [SQL Online  |  Sandbox](https://sqliteonline.com/)  

---

# Banco de Dados

**Dado:** Conjunto de Bits/Bytes  
**Informação:** Dados com identificação e significado; dado processado  
**Conhecimento:** Informação aplicada a uma utilidade; auxilia na tomada de decisão  
	
**Banco de Dados:** Coleção de dados inter-relacionados e persistentes  

**Arquitetura Three-Schema  |  ANSI-SPARC**  
- American National Standards Institute - Standards Planning and Requirements Committee
- Padrão americano de projeto abstrato para um sistema de gerenciamento de banco de dados
- Proposto em 1978
- Objetivo: separar as aplicações do banco de dados
- *Esquema Externo:* Visão do usuário
- *Esquema Conceitual:* Visão conceitual
- *Esquema Interno:* Visão interna

**SGBD - Sistema Gerenciador de BD:** Coleção de programas responsável pelo gerenciamento dos dados em um BD; podem ser classificados pelo modelo (Relacional, Hierárquico, Redes, Orientado a Objetos, Objeto-Relacional, NoSQL)  

**Redução do Consumo de Memória**  
- *Filtragem de dados:* Operações otimizadas trazem poucos dados, operando diretamente no servidor  
	- Não é necessário carregar (select) dados para realizar operações  
	- Realizar todas as operações com o menor número de comandos possível (client side)

**Transações ACID**  
- *Atomicidade:* Transações são, geralmente, compostas de várias declarações (comandos / operações), a atomicidade garante que cada transação seja tratada como uma entidade única; se uma única operação do bloco falhar, toda a transação deverá ser cancelada
- *Consistência:* Assegurar que uma transação somente leve o banco de dados de um estado válido a outro, mantendo a estabilidade do banco
- *Isolamento:* As transações são isoladas para que as simultâneas não interfiram ou afetem umas às outras; cada solicitação é tratada como se estivesse ocorrendo de forma independente, mesmo que ocorram simultaneamente
- *Durabilidade:* Garante que as alterações de dados feitas por transações executadas com sucesso sejam preservadas, mesmo em caso de falha do sistema.

## Modelagem de Dados

- Organizar a o conhecimento sobre os dados; construção de um *modelo de dados* consistente para ser aplicado em qualquer SGBD moderno
- Estabelece o vínculo entre as necessidades do usuário e a solução de software correspondente, gerando uma redução da complexidade do projeto

**Abstração:** Ocultação de detalhes técnicos para o usuário final; destacar apenas recursos essenciais  
- *Projeto Conceitual:* Visão do usuário; entidades, atributos e relacionamentos
	- MER (Modelo Entidade-Relacionamento)
	- DER (Diagrama Entidade-Relacionamento)
- *Projeto Lógico:* Voltado para implementação; requisitos + modelo de BD
	- Modelo relacional (tabelas)
	- Modelo hierárquico e XML (árvore)
	- Modelo orientado a objetos (classes e objetos complexos)
- *Projeto Físico:*  implementação, codificação

### Modelo Relacional

- 1970 (IBM)
- Representar dados como uma coleção de relações
- Cada relação em formato de tabelas (colunas, linhas)

**Domínio:** Conjunto de valores permitidos para um dado; restrição para preenchimento dos dados; para um domínio existem operações válidas (somar, dividir, extrair dia...)  
- *Domínios básicos:* inteiro, string
- *Domínios compostos:* data, hora
- *Domínios definidos:* (0, 120), (‘M’, ‘F’)

**Atributos:** Campo; item de dado do BD; possui nome e domínio  
- nome: string
- idade: (0, 120)

**Tupla:** Registro; conjunto de pares (atributo, valor); define ocorrência de um fato do mundo real  
- Valor de um atributo é definido no momento da criação da tupla; deve ser compatível com o domínio ou NULL; deve ser atômico (indivisível)
- Tupla de aluno: `{(nome, ‘João’), (idade, 34), (matrícula, 03167034), ...}`

**Relação:** Tabela (coleção de tuplas); composto por um cabeçalho e um corpo  
- *Cabeçalho:* Número fixo de atributos (grau da relação) 
- *Corpo:* Número variável de tuplas (cardinalidade da relação)

**Chave:** Identificadores dos dados; pode ser valores/campos combinados (chave composta)
- *Chave primária (pk):* Identificação única; $$pk (R)$$
- *Chave estrangeira (fk):* Equivalência de valor com chave primária; $$fk(R_1) \rightarrow pk(R_2)$$ 

**Dicionário de Dados:** Lista organizada com todos os elementos que compõem
um BD; repositório centralizado com informações sobre os dados, como: significado, relacionamentos, origem, uso e formatos  

### Normalização do BD

- Reorganização das entidades 
- Garante boa estrutura da tabela e consistência dos dados
- Técnica de *design de banco de dados* que reduz a redundância de dados e elimina anomalias
- Divisão de tabelas maiores em tabelas menores

**Anomalias:** Ocorrem devido ao mau planejamento e não normalização de BDs, geralmente por excesso de dados em uma mesma tabela; dependências parciais e transitivas
- *Inclusão:* Repetição desnecessária de valores ao inserir um dado
- *Atualização:* Inconsistências no bd ao excluir um dado
- *Exclusão:* Inconsistências no bd ao atualizar um dado

**Dependências** 
- *Funcional :* Relação entre atributos/colunas
	- ex. `CPF | Nome`
- *Funcional Parcial:* Coluna não depende da PK ou de toda PK (se for composta)
	- ex. PK = `ID_Aluno` + `ID_Materia` + `Semestre` | `Nome_Materia` | `Nota`
	- Nome_Materia depende apenas de ID_Materia
- *Funcional Transitiva:* Coluna depende de outra coluna que não é uma PK
	- ex. PK = `ID_Funcionario` | `Nome_Funcionario` | `ID_Cargo` | `Nome_Cargo` | `Salario`
	- Nome_Cargo depende de ID_Cargo

**Atributos**  
- *Multivalorados:* Podem conter mais de um valor para o mesmo registro (linha)
	- ex. campo Telefone contem dois números, fixo e celular
- *Compostos:* Atributos que poderiam ser subdivididos em vários atributos
	- ex. Endereço com Rua, Bairro, Cidade e UF

**Formas Normais**  
*1NF*  
- Dados atômicos (indivisíveis) e únicos
- Eliminar atributos multivalorados (nova tabela) e compostos (nova coluna)
1. Criar uma tabela separada para cada conjunto de dados relacionados
2. Identificar cada conjunto de dados relacionados com uma PK

*2NF*  
- Depende da 1NF
- Eliminar dependência funcional parcial (nova tabela)
- Cada atributo não-chave deve depender da PK
1. Criar tabelas separadas para cada PK ou combinação de atributos que se aplicam a vários registros
2. Relacionar essas tabelas com uma FK

*3NF*  
- Depende da 2NF
-  Eliminar dependência funcional parcial transitiva (nova tabela)
- Atributo não-chave depende de outro atributo não-chave 
 1. Eliminar campos que não dependem da PK
 2. Alocar em uma nova tabela e relacionar a uma PK

---

# SQL (Structured Query Language)

- Linguagem de Consulta Estruturada para banco de dados não relacional comerciais  
- Padrão para SGBDs

> `*`  (asterisco): All  
> `LIKE`: Semelhante  
> `?`: Substitui char  
 >  `DESCRIBE`: Apresenta informações sobre a estrutura de objetos da base de dados  

## Tipos de Dados

**FOAT e DOUBLE**  
- Tipo de ponto flutuante, armazenado como notação científica: parte significativa e expoente
- ex. 3,54 seria armazenado como = $355 * (10²)$ 
	- é armazenado apenas 345 e -2, tendo 10 como base
- Como a base dos computadores é binária, números simples precisariam de mais bits para serem representados com precisão
- Para números que sofrerão cálculos consecutivos, podem haver arredondamentos que geram *imprecisão no resultado final*
- O mesmo ocorre com tipos double, com menor efeito por poder armazenar com maior precisão

**DECIMAL**  
- Tipo de ponto fixo
- Não possui os mesmos prolemas que float e double
- Definido em quantidade de dígitos e quantidade de casas decimais 
	- `DECIMAL(10,2)` - para valores financeiros

![Tipos de Dados em SQL](docs/Banco-Dados/img/tipos-dados.png)

## Constraints

Restrições; regras pré definidas impostas às colunas; controlar dados que são inseridos  
- `NOT NULL`
- `UNIQUE`
- `CHECK`
- `DEFAULT`

**Primary Key  X Unique**  

| Primary Key                                        | Unique                                                |
| -------------------------------------------------- | ----------------------------------------------------- |
| Identifica cada linha de forma única em uma tabela | Identifica valores únicos em uma coluna de uma tabela |
| Não aceita valores NULL                            | Aceita valores NULL                                   |
| Uma tabela pode ter somente 1                      | Uma tabela pode ter mais de 1                         |
| Um índice clusterizado é criado por padrão         | Índices não-clusterizados são criados nas colunas     |


## Comandos

### Data Definition Language (DDL)

Usado para definir o esquema do banco de dados; criar e modificar a estrutura dos objetos

- `CREATE`: Criar tabela
- `DROP`: Excluir tabela
- `ALTER`: Modificar estrutura; adicionar, alterar, excluir colunas; modificar restrições, índices; renomear tabela
	- `MODIFY`: Modificar atributos de colunas em uma tabela existente, como o tipo de dado ou tamanho
 ㅤㅤㅤ  
- `PRIMARY KEY`: Unica, exclusiva; não pode ser nulo; tabela possui apenas uma chave primária
- `FOREIGN KEY`: Estabelecer e manter a integridade dos dados entre tabelas relacionadas; pode ser nula (registro órfão); possível ter mais de uma na tabela 
	- `CONSTRAINT`: Aplica regra a um campo ou conjunto de campos para garantir a integridade dos dados
	- `REFERENCES`: Especifica a tabela e a coluna que a chave estrangeira deve referenciar
	- `CASCADE, SET NULL, SET DEFAULT, RESTRIC`:
		- `CASCADE`: Propaga a operação para as tabelas dependentes 
		- `SET NULL:` Define os campos relacionados como NULL quando a operação é realizada (ex. se registro pai é deletado, campos da chave estrangeira nos filhos são definidos como NULL)
		- `SET DEFAULT`: Define os campos relacionados para um valor padrão predefinido 
		- `RESTRICT`: Impede que a operação seja realizada se houver registros dependentes
	- `ON DELETE`: Especifica o que acontece com os registros dependentes quando um registro pai é excluído
	- `ON UPDATE`: Define o comportamento dos registros dependentes quando um registro pai é atualizado


**Primary Key - Foreign Key**  

```sql
-- PK / FK
Id INT AUTO_INCREMENT PRIMARY KEY;

ALTER TABLE table_name
ADD CONSTRAINT fk_example
FOREIGN KEY (fk_example)
REFERENCES table2(pk_example);

-- Chave composta
CREATE TABLE table_name(
   column1 INT NOT NULL,
   column2 INT NOT NULL,
   PRIMARY KEY AUTO_INCREMENT (column1, column2)
);
```

**Criar tabela  |  Inserção de Dados**  

```sql
CREATE TABLE table_name(
	id, INT(10) UNSIGNED NOT NULL,
	name VARCHAR(50) NOT NULL,
	phone INT(10),
	PRIMARY KEY(id));

-- Auto increment
CREATE TABLE table_name(
   personalized_id INT PRIMARY KEY AUTOINCREMENT
   column1 INT NOT NULL,
   column2 INT NOT NULL,
);

-- Criar tabela a partir de outra
CREATE TABLE table_name LIKE origin_table;
-- Criar tabela a partir de seleção em outra tabela
CREATE TABLE table_name SELECT * FROM origin_table;
```

**Alterações**  

```sql
-- ALTERANDO ESTRUTURA
RENAME TABLE table_name TO new_name; -- renomeia tabela

ALTER TABLE table_name MODIFY column_name <new-column-type>;
ALTER TABLE table_name MODIFY column_name INTEGER; -- altera o tipo de dados
ALTER TABLE table_name MODIFY COLUMN column_name DECIMAL(10,2) NOT NULL; -- torna não nulo

ALTER TABLE table_name ADD COLUMN column_name VARCHAR(25); -- adiciona coluna
ALTER TABLE table_name CHANGE sigla UF CHAR(2) DEFAULT ‘SP’; -- renomeia coluna define tipo de dado e define valor padrão

ALTER TABLE table_name DROP column; -- elimina coluna
```

### Data Manipulation Language (DML)

- Interagem com *dados* dentro de tabelas; adicionar, editar ou excluir dados de um banco de dados  
- `INSERT`: Insere dados em uma tabela específica  
	- Conteúdo a ser inserido (Values) deve estar indicado entre apóstrofo (' ')  
- `UPDATE`: Atualiza dados em uma tabela especificada  
	- Critérios `WHERE` são indicados como WHERE  
- `DELETE`: Exclui dados de uma tabela especificada  
	
> `WHERE`: Especifica critérios de seleção da consulta  
> `ORDER BY`: Especifica critérios para ordenação dos registros da tabela; `ASC` (ascendente), `DESC` (descendente)  
	
```sql
-- INSERINDO DADOS

INSERT INTO table_name(id, name, phone)
			VALUE (10, "Name", 40566700);

INSERT INTO clientes(ID, Nome, Telefone) VALUES
			(1,"Name", 40566700),
			(2,"Name 2", 6534674);

-- ALTERANDO DADOS
UPDATE table_name SET column = "new_column_name" WHERE chave = "key_column";

-- REMOVER DADOS
DELETE from table_name WHERE key_column = condição;
DELETE FROM client WHERE name LIKE "A%"; -- apagar todos que começam com A

DELETE FROM table_name; -- apaga todos registros da tabela

```

### (DQL) Data Query

- Seleciona dados de uma ou mais tabelas para leitura ou consulta  
- `SELECT`

**Funções Agregadas**  
- `SUM()`
- `COUNT()`
- `AVG()`
- `MIN()`
- `MAX()`

```sql
-- Consultar múltiplas tabelas
SELECT * FROM table_name1, table_name2;

-- Concatenar strings
SELECT
  CONCAT(first_name, ' ', last_name) AS full_name
FROM table_name;

-- REFINAR CONSULTA
SELECT * FROM table_name WHERE column='data';
SELECT * FROM table_name WHERE name='Bob';

SELECT * FROM table_name 
WHERE name LIKE("%a%") -- contém "a" em qualquer parte
OR name LIKE("_a%") -- contém "a" na segunda posição
OR name LIKE("A%"); -- incia com "A"

SELECT * FROM table WHERE field='data' AND field2 > 100;

-- Valores específicos
SELECT * FROM table_name
WHERE column IN(1,2,3,4);

SELECT first_name, last_name, pet
FROM table_name
WHERE pet IN('cat', 'dog');

SELECT * FROM table_name
WHERE species NOT IN('cat', 'dog');

-- FILTROS

-- Ordenação
SELECT * FROM table_name ORDER BY column [ASC | DESC];
SELECT * FROM table_name ORDER BY LEN(field);
SELECT * FROM table_name LIMIT 4;

-- Formatação
SELECT LCASE('STRING'); 
SELECT UPPER('string');

-- Filtrar por data e hora
SELECT CURRENT_DATE();
SELECT CURDATE();

SELECT CURRENT_TIME();
SELECT CURTIME();

SELECT DATE_FORMAT('2022/02/18','%d/%m/%Y'); -- 18-02-2022
SELECT DATE_FORMAT(CURDATE(),'%d/%m/%y'); -- 21-10-2022
SELECT DATE_FORMAT(CURDATE(),'%D/%M/%Y'); -- 14st/março/2019
SELECT DATE_FORMAT(CURDATE(),'%W - %D /%M /%Y'); -- quinta - 10st/março/2018
SELECT DATE_FORMAT(CURDATE(),'%W - %D /%M /%Y - %j dias corridos'); -- quinta - 21st /março /2020 - 80 dias corridos

SELECT DATE_FORMAT(CURTIME(),'%h : %i : %s '); -- 15 : 12 : 422
ou
SELECT TIME_FORMAT(CURTIME(),'%h : %i : %s '); -- 15 : 12 : 422

-- Filtrar por valores
SELECT
  first_name,
  last_name,
  MAX(height) AS height
FROM table_name;

SELECT MIN(value) FROM table_name;
SELECT MAX(value) FROM table_name;
SELECT SUM(value) FROM table_name;
SELECT AVG(value) FROM table_name; -- média

SELECT COUNT(value) FROM table_name;
SELECT COUNT(value) FROM table_name WHERE id=10; -- exemplo

-- Distringuir
SELECT DISTINCT column1, column2, ...
FROM table_name;

-- Agrupar
SELECT column_name(s)
FROM table_name
WHERE condition
GROUP BY column_name(s)
ORDER BY column_name(s);
```

**Consultas Avançadas**  
 - Na sua forma básica, a declaração SELECT recupera linhas e colunas de uma tabela
 - A cláusula WHERE é usada para filtrar as linhas que serão retornadas pela SELECT
 - Pode-se utilizar a palavra-chave AS para renomear cabeçalhos das colunas retornadas por um SELECT
 - JOIN permite recuperação de dados relacionados 
 - Condições JOIN dizem como recuperar os dados especificados na cláusula FROM

```sql
-- JOINS
SELECT * FROM table_name 
[ INNER/LEFT/RIGHT ] JOIN ohter_table 
ON table_name.column = ohter_table.field;

-- criar "apelidos" para tabelas e campos com AS; facilita legibilidade da consulta
SELECT * FROM table_name AS A 
INNER JOIN ohter_table AS B 
ON A.column = B.column;

--exemplos
SELECT first_name, last_name, city_name
FROM patients 
JOIN city_names 
ON patients.city_id = city_names.city_id;

SELECT * FROM students AS S
INNER JOIN class AS C
ON S.cod_class = C.cod_class;

SELECT * FROM students 
INNER JOIN class 
ON students.cod_class = class.cod_class 
WHERE class.name LIKE ('E%') OR class.name LIKE ('I%');

-- SUBCONSULTAS

SELECT column1, column2 
FROM table_name 
WHERE column > ( SELECT AVG(column) FROM table_name );
```

![](docs/Banco-Dados/img/sql-join.png)


### Data Control Language (DCL)

- Controlar a parte de segurança do bando de dados; estabelece permissões e privilégios  
- `GRANT`: permite
- `REVOKE`: revoga

```sql
SELECT user, host FROM mysql.user; -- visualizar usuários

SELECT GRANTS FOR user-name; -- visualizar privilégios dos usuários

CREATE USER user-name; -- criação de usuário sem senha/privilégio
ALTER USER user-name IDENTIFIED BY '12345'; -- alterar a senha de usuário

-- CRIAÇÃO DE USUÁRIO (com senha/privilégios)

-- Acesso a todas as bases de dados
GRANT ALL ON *.* TO user-name IDENTIFIED BY '12345'; 
GRANT ALL PRIVILEGES ON db-name.* TO user-name; 
-- Acesso a todas as bases de dados; pode conceder e retirar privilégios
GRANT ALL On *.* To user-name Identified BY '12345' WITH GRANT OPTION;

-- Acesso a uma base de dados ou tabela específica
GRANT ALL ON db-name.* TO user-name IDENTIFIED BY '12345'; 
GRANT USAGE ON db-name.table TO user-name IDENTIFIED BY '12345'; 

-- Acesso parcial
GRANT SELECT, INSERT, UPDATE, DELETE ON db-name.* TO user-name@;
GRANT SELECT(first_name, last_name), UPDATE(first_name) ON
db.table TO user-name;

-- Remover privilégios
REVOKE ALL On db-name.* FROM user-name;
REVOKE DELETE ON db-name.* FROM user-name;
REVOKE ALL, GRANT OPTION FROM user1, user-name@localhost;
```

### Transaction Control Language (TCL)

Controle de transações (comandos DML) no SQL  

- `STORED PRODECURES`: conjunto de comandos que podem ser executados de uma só vez
- `TRIGGERS`: gatilho p/ evento especial (pode afetar outras tabelas)
 ㅤㅤㅤ  
- `BEGIN`: inicia nova transação
- `COMMIT`: salva ação
- `ROLLBACK`: desfazer ação
- `SAVEPOINT`: subdivisão de transição longa

```sql
BEGIN TRANSACTION transaction_name;

-- Efetivar as ações (pós GRANT ou REVOKE)
COMMIT;
FLUSH PRIVILEGES;

-- Usuário para acesso remoto
GRANT ALL ON *.* TO 'user-name@%' IDENTIFIED BY '1234';
```

## Views

- Tabelas virtuais que permitem visualizar resultados de consultas de tabelas reais
- Traz visão otimizada dos dados
- Restringe acesso total a base de dados por qualquer usuário

```sql
CREATE VIEW view_name 
AS SELECT field1, field2 
FROM table_name;
```

## Índices

- Auxiliam o SGBD a localizar registros com mais facilidade, para consultas frequentes
- Economiza tempo de operações I/O
- Podem ser criados em tabelas, views e tabelas temporárias
- Fornecem uma pesquisa ordenada de informação para consultas
- É possível criar índices na criação de uma tabela
- Index != Chave

```sql
CREATE INDEX index_name 
ON table_name(field);

ALTER TABLE table_name
ADD INDEX index_name(field);

DROP INDEX index_name
ON table_name;

SHOW INDEX FROM table_name;

SELECT * FROM table_name WHERE field LIKE "A%"; --exemplo de acesso
-- índice não é informado, mas o SGBD
-- sabe que para o campo existe um índice criado
```

## Sequências

- Permite criar um objeto na base de dados que gera uma sequência automática de números (autoincremento)
- O objeto é um elemento externo às tabelas
- Pode ser usado para alimentar atributos que necessitem de um campo com essa característica; por exemplo se aplicações externas que ao acessarem o banco de dados, um novo número e exclusivo pode ser gerado

```sql
CREATE SEQUENCE obj_sequence 
START WITH initial_value INCREMENT BY increment_value;

SELECT NEXTVAL(obj_sequence); -- verificar número atual
```


