# Modelagem de banco de dados completa

# 1 - Cenário
## Sistema de Gestão de Biblioteca
A Biblioteca Municipal está modernizando seu sistema de gestão para melhorar a eficiência do gerenciamento de livros, membros e empréstimos. O sistema de banco de dados será projetado para rastrear livros, membros, funcionários, empréstimos e categorias de livros.


# 2 - Modelagem Conceitual

![DER](https://github.com/joaop-dev/Modelagem-de-Banco-de-Dados-Completa/blob/main/img/MODELO_CONCEITUAL.png)


# 3 - Modelagem Lógica

![DER (2)](https://github.com/joaop-dev/Modelagem-de-Banco-de-Dados-Completa/blob/main/img/MODELO_LOGICO.png)

# 4 - Modelagem Física

```sql
    CREATE TABLE Categoria (
    ID_Categoria INT PRIMARY KEY AUTO_INCREMENT,
    Nome VARCHAR(100),
    Descrição TEXT
);

CREATE TABLE Livro (
    ID_Livro INT PRIMARY KEY AUTO_INCREMENT,
    Título VARCHAR(255),
    Autor_Nome VARCHAR(100),
    Autor_Sobrenome VARCHAR(100),
    ISBN VARCHAR(20),
    Data_Publicacao DATE,
    Quantidade INT,
    Capa JSON,
    Categoria_ID INT,
    FOREIGN KEY (Categoria_ID) REFERENCES Categoria(ID_Categoria)
);

CREATE TABLE Membro (
    ID_Membro INT PRIMARY KEY AUTO_INCREMENT,
    Primeiro_Nome VARCHAR(100),
    Sobrenome VARCHAR(100),
    Data_Nascimento DATE,
    Rua VARCHAR(100),
    Número VARCHAR(10),
    Cidade VARCHAR(100),
    Estado VARCHAR(50),
    CEP VARCHAR(10),
    Telefone VARCHAR(15),
    Email VARCHAR(100),
    Data_Cadastro DATE,
    Status ENUM('Ativo', 'Inativo'),
    Livros_Alugados INT DEFAULT 0
);

CREATE TABLE Funcionario (
    ID_Funcionario INT PRIMARY KEY AUTO_INCREMENT,
    Primeiro_Nome VARCHAR(100),
    Sobrenome VARCHAR(100),
    Data_Contratacao DATE,
    Cargo VARCHAR(100),
    Salario DECIMAL(10, 2),
    Supervisor_ID INT,
    FOREIGN KEY (Supervisor_ID) REFERENCES Funcionario(ID_Funcionario)
);

CREATE TABLE Emprestimo (
    ID_Emprestimo INT PRIMARY KEY AUTO_INCREMENT,
    Data_Emprestimo DATE,
    Data_Devolucao DATE,
    Status ENUM('Pendente', 'Devolvido'),
    Livro_ID INT,
    Membro_ID INT,
    Funcionario_ID INT,
    FOREIGN KEY (Livro_ID) REFERENCES Livro(ID_Livro),
    FOREIGN KEY (Membro_ID) REFERENCES Membro(ID_Membro),
    FOREIGN KEY (Funcionario_ID) REFERENCES Funcionario(ID_Funcionario)
);
```
# 5 - Inserção de Dados

```sql
INSERT INTO Categoria (Nome, Descricao) VALUES 
('Ficção', 'Livros de ficção científica e fantasia.'),
('Não-Ficção', 'Livros baseados em fatos reais.'),
('Romance', 'Livros de romance e drama.'),
('Terror', 'Livros de terror e suspense.'),
('Infantil', 'Livros infantis.'),
('Aventura', 'Livros de aventura e ação.'),
('História', 'Livros de história e biografias.'),
('Filosofia', 'Livros de filosofia e pensamento crítico.'),
('Ciência', 'Livros científicos e educacionais.'),
('Autoajuda', 'Livros de autoajuda e motivação.'),
('Fantasia', 'Livros de fantasia e magia.'),
('Mistério', 'Livros de mistério e investigação.'),
('Tecnologia', 'Livros sobre tecnologia e inovação.'),
('Economia', 'Livros de economia e negócios.'),
('Psicologia', 'Livros de psicologia e comportamento.'),
('Saúde', 'Livros sobre saúde e bem-estar.'),
('Política', 'Livros de política e governo.'),
('Arte', 'Livros de arte e design.'),
('Religião', 'Livros de religião e espiritualidade.'),
('Humor', 'Livros de humor e comédia.');


INSERT INTO Livro (Titulo, Autor_Nome, Autor_Sobrenome, ISBN, Data_Publicacao, Quantidade, Capa, Categoria_ID) VALUES 
('Duna', 'Frank', 'Herbert', '9780441013593', '1965-06-01', 10, 'img1.jpg', 1),
('1984', 'George', 'Orwell', '9780451524935', '1949-06-08', 15, 'img3.jpg', 2),
('Orgulho e Preconceito', 'Jane', 'Austen', '9781503290563', '1813-01-28', 8, 'img4.jpg', 3),
('It - A Coisa', 'Stephen', 'King', '9780451169518', '1986-09-15', 5, 'img6.jpg', 4),
('O Pequeno Príncipe', 'Antoine', 'de Saint-Exupéry', '9780156012195', '1943-04-06', 20, 'img7.jpg', 5),
('O Senhor dos Anéis', 'J.R.R.', 'Tolkien', '9780544003415', '1954-07-29', 12, 'img8.jpg', 1),
('O Apanhador no Campo de Centeio', 'J.D.', 'Salinger', '9780316769488', '1951-07-16', 14, 'img10.jpg', 2),
('Harry Potter e a Pedra Filosofal', 'J.K.', 'Rowling', '9780439554930', '1997-06-26', 18, 'img11.jpg', 1),
('O Código Da Vinci', 'Dan', 'Brown', '9780307474278', '2003-03-18', 9, 'img13.jpg', 6),
('A Culpa é das Estrelas', 'John', 'Green', '9780142424179', '2012-01-10', 7, 'img14.jpg', 3),
('O Hobbit', 'J.R.R.', 'Tolkien', '9780547928227', '1937-09-21', 11, 'img16.jpg', 1),
('Moby Dick', 'Herman', 'Melville', '9780142437247', '1851-10-18', 5, 'img18.jpg', 7),
('Drácula', 'Bram', 'Stoker', '9780141439846', '1897-05-26', 8, 'img19.jpg', 4),
('Frankenstein', 'Mary', 'Shelley', '9780143131847', '1818-01-01', 6, 'img20.jpg', 4),
('As Crônicas de Nárnia', 'C.S.', 'Lewis', '9780066238500', '1950-10-16', 10, 'img21.jpg', 1),
('A Menina que Roubava Livros', 'Markus', 'Zusak', '9780375842207', '2005-09-01', 12, 'img23.jpg', 3),
('O Nome do Vento', 'Patrick', 'Rothfuss', '9780756404741', '2007-03-27', 7, 'img24.jpg', 1),
('Jogos Vorazes', 'Suzanne', 'Collins', '9780439023481', '2008-09-14', 20, 'img26.jpg', 6),
('Os Miseráveis', 'Victor', 'Hugo', '9780451419439', '1862-04-03', 9, 'img27.jpg', 7),
('O Conto da Aia', 'Margaret', 'Atwood', '9780385490818', '1985-09-01', 11, 'img29.jpg', 8);


INSERT INTO Membro (Primeiro_Nome, Sobrenome, Data_Nascimento, Rua, Numero, Cidade, Estado, CEP, Telefone, Email, Data_Cadastro, Status) VALUES 
('Maria', 'Silva', '1990-05-10', 'Rua A', '123', 'São Paulo', 'SP', '01000-000', '111111111', 'maria@example.com', '2022-01-15', 'Ativo'),
('João', 'Pereira', '1985-03-20', 'Rua B', '456', 'Rio de Janeiro', 'RJ', '02000-000', '222222222', 'joao@example.com', '2022-02-20', 'Ativo'),
('Ana', 'Souza', '1992-07-30', 'Rua C', '789', 'Belo Horizonte', 'MG', '03000-000', '333333333', 'ana@example.com', '2022-03-10', 'Ativo'),
('Pedro', 'Oliveira', '1988-11-15', 'Rua D', '101', 'Curitiba', 'PR', '04000-000', '444444444', 'pedro@example.com', '2022-04-05', 'Inativo'),
('Carla', 'Santos', '1995-09-25', 'Rua E', '202', 'Salvador', 'BA', '05000-000', '555555555', 'carla@example.com', '2022-05-25', 'Ativo'),
('Lucas', 'Ferreira', '1998-12-05', 'Rua F', '303', 'Porto Alegre', 'RS', '06000-000', '666666666', 'lucas@example.com', '2022-06-15', 'Ativo'),
('Mariana', 'Silveira', '1993-08-15', 'Rua G', '404', 'Fortaleza', 'CE', '07000-000', '777777777', 'mariana@example.com', '2022-07-20', 'Inativo'),
('Gabriel', 'Ramos', '1987-04-30', 'Rua H', '505', 'Recife', 'PE', '08000-000', '888888888', 'gabriel@example.com', '2022-08-05', 'Ativo'),
('Larissa', 'Oliveira', '1996-10-20', 'Rua I', '606', 'Brasília', 'DF', '09000-000', '999999999', 'larissa@example.com', '2022-09-10', 'Ativo'),
('Diego', 'Santana', '1991-02-25', 'Rua J', '707', 'Natal', 'RN', '10000-000', '1010101010', 'diego@example.com', '2022-10-15', 'Inativo'),
('Camila', 'Gonçalves', '1989-11-10', 'Rua K', '808', 'Manaus', 'AM', '11000-000', '1111111111', 'camila@example.com', '2022-11-20', 'Ativo'),
('Thiago', 'Albuquerque', '1994-07-05', 'Rua L', '909', 'Belém', 'PA', '12000-000', '1212121212', 'thiago@example.com', '2022-12-25', 'Inativo'),
('Amanda', 'Barbosa', '1997-03-15', 'Rua M', '1010', 'Florianópolis', 'SC', '13000-000', '1313131313', 'amanda@example.com', '2023-01-05', 'Ativo'),
('Marcelo', 'Sousa', '1990-09-05', 'Rua N', '1111', 'João Pessoa', 'PB', '14000-000', '1414141414', 'marcelo@example.com', '2023-02-10', 'Ativo'),
('Juliana', 'Carvalho', '1988-01-20', 'Rua O', '1212', 'Maceió', 'AL', '15000-000', '1515151515', 'juliana@example.com', '2023-03-15', 'Inativo'),
('Luciana', 'Martins', '1993-05-30', 'Rua P', '1313', 'Vitória', 'ES', '16000-000', '1616161616', 'luciana@example.com', '2023-04-20', 'Ativo'),
('Renato', 'Garcia', '1995-11-25', 'Rua Q', '1414', 'Porto Velho', 'RO', '17000-000', '1717171717', 'renato@example.com', '2023-05-25', 'Inativo'),
('Fernanda', 'Silva', '1992-08-10', 'Rua R', '1515', 'Cuiabá', 'MT', '18000-000', '1818181818', 'fernanda@example.com', '2023-06-30', 'Ativo'),
('Ricardo', 'Santos', '1996-04-15', 'Rua S', '1616', 'Teresina', 'PI', '19000-000', '1919191919', 'ricardo@example.com', '2023-07-05', 'Inativo'),
('Laura', 'Lima', '1991-10-05', 'Rua T', '1717', 'Goiânia', 'GO', '20000-000', '2020202020', 'laura@example.com', '2023-08-10', 'Ativo');

INSERT INTO Funcionario (Primeiro_Nome, Sobrenome, Data_Contratacao, Cargo, Salario, Supervisor_ID) VALUES 
('Carlos', 'Almeida', '2020-01-15', 'Bibliotecário', 3000.00, NULL),
('Fernanda', 'Gomes', '2019-03-20', 'Assistente', 2000.00, 1),
('Rafael', 'Moraes', '2018-07-10', 'Técnico', 2500.00, 1),
('Juliana', 'Fernandes', '2021-05-05', 'Bibliotecária', 3200.00, NULL),
('Mariana', 'Rocha', '2020-11-25', 'Auxiliar', 1800.00, 2),
('Lucas', 'Santana', '2017-12-30', 'Coordenador', 4000.00, NULL),
('Amanda', 'Costa', '2016-09-18', 'Analista', 2800.00, 6),
('Gustavo', 'Oliveira', '2015-06-10', 'Gerente', 5000.00, NULL),
('Isabela', 'Martins', '2023-03-15', 'Estagiário', 1500.00, 3),
('Roberto', 'Silveira', '2014-04-05', 'Supervisor', 3500.00, 8),
('Vanessa', 'Pereira', '2022-08-20', 'Assistente', 2000.00, 7),
('Rodrigo', 'Fernando', '2021-11-12', 'Técnico', 2300.00, 3),
('Patricia', 'Souza', '2020-02-25', 'Bibliotecária', 3200.00, NULL),
('Diego', 'Costa', '2019-07-08', 'Auxiliar', 1800.00, 12),
('Carolina', 'Lima', '2018-10-30', 'Coordenador', 4000.00, NULL),
('Alexandre', 'Martins', '2017-04-15', 'Analista', 2800.00, 10),
('Cristina', 'Oliveira', '2022-05-20', 'Estagiário', 1500.00, 14),
('Marcos', 'Silva', '2021-02-10', 'Supervisor', 3500.00, 16),
('Tatiane', 'Pereira', '2020-09-05', 'Assistente', 2000.00, 15),
('Pedro', 'Fernandes', '2019-12-28', 'Técnico', 2300.00, 17);


INSERT INTO Emprestimo (Data_Emprestimo, Data_Devolucao, Status, Livro_ID, Membro_ID, Funcionario_ID) VALUES 
('2023-01-15', '2023-01-30', 'Devolvido', 1, 1, 1),
('2023-02-20', '2023-03-05', 'Devolvido', 2, 2, 2),
('2023-03-10', '2023-03-25', 'Devolvido', 3, 3, 3),
('2023-04-05', '2023-04-20', 'Devolvido', 4, 4, 4),
('2023-05-25', '2023-06-09', 'Devolvido', 5, 5, 5),
('2023-06-15', '2023-06-30', 'Devolvido', 6, 6, 6),
('2023-07-20', '2023-08-04', 'Devolvido', 7, 7, 7),
('2023-08-10', '2023-08-25', 'Devolvido', 8, 8, 8),
('2023-09-05', '2023-09-20', 'Devolvido', 9, 9, 9),
('2023-10-25', '2023-11-09', 'Devolvido', 10, 10, 10),
('2023-11-15', '2023-11-30', 'Devolvido', 11, 11, 11),
('2023-12-20', '2024-01-04', 'Devolvido', 12, 12, 12),
('2024-01-15', '2024-01-30', 'Devolvido', 13, 13, 13),
('2024-02-10', '2024-02-25', 'Devolvido', 14, 14, 14),
('2024-03-05', '2024-03-20', 'Devolvido', 15, 15, 15),
('2024-04-25', '2024-05-10', 'Devolvido', 16, 16, 16),
('2024-05-15', '2024-05-30', 'Devolvido', 17, 17, 17),
('2024-06-10', '2024-06-25', 'Devolvido', 18, 18, 18),
('2024-07-05', '2024-07-20', 'Devolvido', 19, 19, 19),
('2024-08-15', '2024-08-30', 'Devolvido', 20, 20, 20);
```

# 6 - CRUD
Criação (Create):
```sql
INSERT INTO Membro (Primeiro_Nome, Sobrenome, Data_Nascimento, Rua, Numero, Cidade, Estado, CEP, Telefone, Email, Data_Cadastro, Status) VALUES 
('Lucas', 'Martins', '1993-02-10', 'Rua F', '303', 'Porto Alegre', 'RS', '06000-000', '666666666', 'lucas@example.com', '2022-06-15', 'Ativo');
```
![criação](https://github.com/joaop-dev/Modelagem-de-Banco-de-Dados-Completa/blob/main/img/CRUD%20(criação-create).png)


Leitura (Read):

```sql
SELECT * FROM Livro;

SELECT * FROM Membro;
```
![leitura](https://github.com/joaop-dev/Modelagem-de-Banco-de-Dados-Completa/blob/main/img/CRUD%20(leitura-read).png)


Atualização (Update):

```sql
UPDATE Membro
SET Status = 'Inativo'
WHERE ID_Membro = 1;
```
![update](https://github.com/joaop-dev/Modelagem-de-Banco-de-Dados-Completa/blob/main/img/CRUD%20(atualizacao-update).png)


Deleção (Delet):

```sql
DELETE FROM Emprestimo
WHERE ID_Emprestimo = 1;
```
![delet](https://github.com/joaop-dev/Modelagem-de-Banco-de-Dados-Completa/blob/main/img/CRUD%20(deleção-delet).png)

# 7 - Relatórios:

1 - Listar todos os livros com suas categorias:

```sql
SELECT Livro.Título, Categoria.Nome AS Categoria
FROM Livro
JOIN Categoria ON Livro.Categoria_ID = Categoria.ID_Categoria;
```
![categorias](https://github.com/joaop-dev/Modelagem-de-Banco-de-Dados-Completa/blob/main/img/relatorio01.png)

2 - Listar todos os membros ativos:

```sql
SELECT * FROM Membro
WHERE Status = 'Ativo';
```
![membros](https://github.com/joaop-dev/Modelagem-de-Banco-de-Dados-Completa/blob/main/img/relatorio02.png)

3 - Listar todos os empréstimos pendentes:

```sql
SELECT * FROM Emprestimo
WHERE Status = 'Pendente';
```
![emprestimo](https://github.com/joaop-dev/Modelagem-de-Banco-de-Dados-Completa/blob/main/img/relatorio03.png)

4 - Listar todos os funcionários com seus supervisores:

```sql
SELECT F1.Primeiro_Nome AS Funcionario, F2.Primeiro_Nome AS Supervisor
FROM Funcionario F1
LEFT JOIN Funcionario F2 ON F1.Supervisor_ID = F2.ID_Funcionario;
```
![funcionarios](https://github.com/joaop-dev/Modelagem-de-Banco-de-Dados-Completa/blob/main/img/relatorio04.png)

5 - Listar os livros mais populares (mais emprestados):

```sql
SELECT Livro.Titulo, COUNT(Emprestimo.ID_Emprestimo) AS Total_Emprestimos
FROM Livro
JOIN Emprestimo ON Livro.ID_Livro = Emprestimo.Livro_ID
GROUP BY Livro.Titulo
ORDER BY Total_Emprestimos DESC;
```
![populares](https://github.com/joaop-dev/Modelagem-de-Banco-de-Dados-Completa/blob/main/img/relatorio05.png)

6 - Listar os membros que mais emprestaram livros:

```sql
SELECT Membro.Primeiro_Nome, COUNT(Emprestimo.ID_Emprestimo) AS Total_Emprestimos
FROM Membro
JOIN Emprestimo ON Membro.ID_Membro = Emprestimo.Membro_ID
GROUP BY Membro.Primeiro_Nome
ORDER BY Total_Emprestimos DESC;
```
![membrosemprestimo](https://github.com/joaop-dev/Modelagem-de-Banco-de-Dados-Completa/blob/main/img/relatorio06.png)

7 - Listar todos os livros de uma categoria específica:

```sql
SELECT Livro.Titulo
FROM Livro
WHERE Categoria_ID = (SELECT ID_Categoria FROM Categoria WHERE Nome = 'Ficção');
```
![categoriaespecifica](https://github.com/joaop-dev/Modelagem-de-Banco-de-Dados-Completa/blob/main/img/relatorio07.png)

8 - Listar todos os empréstimos feitos por um funcionário específico:

```sql
SELECT Emprestimo.*
FROM Emprestimo
WHERE Funcionario_ID = (SELECT ID_Funcionario FROM Funcionario WHERE Primeiro_Nome = 'Carlos');
```
![emprestimofuncionario](https://github.com/joaop-dev/Modelagem-de-Banco-de-Dados-Completa/blob/main/img/relatorio08.png)

9 - Listar todos os membros e quantos livros cada um emprestou:

```sql
SELECT Membro.Primeiro_Nome, COUNT(Emprestimo.ID_Emprestimo) AS Total_Emprestimos
FROM Membro
LEFT JOIN Emprestimo ON Membro.ID_Membro = Emprestimo.Membro_ID
GROUP BY Membro.Primeiro_Nome;
```
![emprestimototal](https://github.com/joaop-dev/Modelagem-de-Banco-de-Dados-Completa/blob/main/img/relatorio09.png)

10 - Listar os livros de um autor específico:

```sql
SELECT Titulo
FROM Livro
WHERE Autor_Nome = 'George' AND Autor_Sobrenome = 'Orwell';                                   
```
![autor](https://github.com/joaop-dev/Modelagem-de-Banco-de-Dados-Completa/blob/main/img/relatorio10.png)




