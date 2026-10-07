## Atividade prática 11 - Relacionamento entre tabelas

### Parte 1:

1- Criamos a tabela Alunos:
```sql
CREATE TABLE alunos(
    id SERIAL PRIMARY KEY,
    nome VARCHAR(50) NOT NULL
);
```
2- Criamos a tabela Emprestimos:
```sql
CREATE TABLE emprestimos(
    id SERIAL PRIMARY KEY,
    livro VARCHAR(50) NOT NULL,
    id_aluno INT REFERENCES alunos(id)
);
```

3- Inserindo 15 alunos 
```sql
INSERT INTO alunos (id, nome) VALUES
(1, 'João'),
(2, 'Maria'),
(3, 'Pedro'),
(4, 'Ana'),
(5, 'Lucas'),
(6, 'Julia'),
(7, 'Gabriel'),
(8, 'Beatriz'),
(9, 'Rafael'),
(10, 'Larissa'),
(11, 'Carlos'),
(12, 'Mariana'),
(13, 'Felipe'),
(14, 'Camila'),
(15, 'Bruno');
```

4- Inserindo os 10 Livros:
```sql
INSERT INTO emprestimos (id, livro, id_aluno) VALUES
(1, 'Harry Potter', 1),
(2, 'O Pequeno Príncipe', 2),
(3, 'Turma da Mônica', 3),
(4, 'Dom Casmurro', 4),
(5, 'O Hobbit', 5),
(6, 'Percy Jackson', 6),
(7, 'Diário de um Banana', 7),
(8, 'A Culpa é das Estrelas', 8),
(9, 'As Crônicas de Nárnia', 9),
(10, 'Extraordinário', 10);
```

### Parte 2:

1- Mostre todos os dados de cada tabela (uma consulta para cada).
```sql
SELECT * FROM alunos;
SELECT * FROM emprestimos;
```

2- Usando INNER JOIN, mostre o nome do aluno e o livro que ele pegou.
   Responda: quais alunos NÃO apareceram? Por quê?
   ```sql
   SELECT alunos.nome, emprestimos.livro
FROM alunos
INNER JOIN emprestimos
ON alunos.id = emprestimos.id_aluno;

Os alunos 11, 12, 13, 14 e 15 não apareceram porque eles não possuem nenhum empréstimo registrado.
```

3- Usando LEFT JOIN, mostre TODOS os alunos e o livro de cada um.
   Responda: o que apareceu na coluna livro para quem não pegou nenhum livro?
   ```sql
   SELECT alunos.nome, emprestimos.livro
FROM alunos
LEFT JOIN emprestimos
ON alunos.id = emprestimos.id_aluno;

Para quem não pegou nenhum livro, apareceu NULL na coluna livro.
```
4- A bibliotecária quer saber quem NUNCA pegou livro.
   Escreva a consulta que mostra só esses alunos.
   ```sql
   SELECT alunos.nome
FROM alunos
LEFT JOIN emprestimos
ON alunos.id = emprestimos.id_aluno
WHERE emprestimos.id IS NULL;
```

5- Tente registrar um empréstimo para o aluno 50:
   INSERT INTO emprestimos (livro, id_aluno) VALUES ('Turma da Mônica', 50);
   Responda: o que aconteceu? Por quê?
   ```sql
   INSERT INTO emprestimos (livro, id_aluno)
VALUES ('Turma da Mônica', 50);

O banco dará erro porque o aluno 50 não existe na tabela alunos. Isso acontece porque id_aluno é uma chave estrangeira (FOREIGN KEY) que deve corresponder a um id existente em alunos.
```