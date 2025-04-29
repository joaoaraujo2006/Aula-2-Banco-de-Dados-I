Nome: João Pedro Gonçalves Corrêa Araujo

DROP TABLE matriculas;
DROP TABLE alunos;
DROP TABLE cursos;

CREATE TABLE alunos (
  id SERIAL PRIMARY KEY,
  nome TEXT NOT NULL,
  turma TEXT NOT NULL,
  curso TEXT NOT NULL,
  data_nascimento DATE
);

CREATE TABLE cursos (
  id SERIAL PRIMARY KEY,
  nome TEXT NOT NULL,
  duracao_anos INT
);

CREATE TABLE matriculas (
  id SERIAL PRIMARY KEY,
  aluno_id INT REFERENCES alunos(id) ON DELETE CASCADE,
  curso_id INT REFERENCES cursos(id) ON DELETE CASCADE,
  data_matricula DATE DEFAULT CURRENT_DATE
);

INSERT INTO alunos (nome, turma, curso, data_nascimento)
VALUES ('João Pedro', 'T18', 'Engenharia de Software', '2002-05-10'),
       ('Carlos', 'T18', 'Engenharia da Computação', '2003-08-15'),
       ('Pedro Jorge', 'T18', 'ADM Tech', '2003-08-15'),
       ('Mirela', 'T18', 'Engenharia da Software', '2003-08-15'),
       ('Danilo', 'T18', 'Engenharia da Software', '2003-08-15'),
       ('Enzo', 'T18', 'Ciência da Computação', '2003-08-15'),
       ('Sophia', 'T18', 'Engenharia de Software', '2003-08-15'),
       ('Victor', 'T18', 'Ciência da Computação', '2003-08-15'),
       ('Gabriel Leon', 'T18', 'ADM Tech', '2003-08-15'),
       ('Maria Vitória', 'T18', 'Engenharia da Computação', '2003-08-15');

INSERT INTO cursos (nome, duracao_anos)
VALUES ('Engenharia de Computação', 4),
       ('ADM Tech', 4),
       ('Engenharia de Software', 4),
       ('Ciência da Computação', 4);

INSERT INTO matriculas (aluno_id, curso_id)
VALUES (1, 3),
       (2, 1),
       (3, 2),
       (4, 3),
       (5, 3),
       (6, 4),
       (7, 3),
       (8, 4),
       (9, 2),
       (10, 1);

SELECT * FROM alunos;
SELECT * FROM cursos;
SELECT a.nome AS aluno, c.nome AS curso, m.data_matricula
FROM matriculas m
JOIN alunos a ON m.aluno_id = a.id
JOIN cursos c ON m.curso_id = c.id;

ALTER TABLE alunos
ADD COLUMN faltas INT;

UPDATE alunos
SET faltas = CASE id
    WHEN 1 THEN 10
    WHEN 2 THEN 7
    WHEN 3 THEN 25
    WHEN 4 THEN 1
    WHEN 5 THEN 3
    WHEN 6 THEN 8
    WHEN 7 THEN 2
    WHEN 8 THEN 11
    WHEN 9 THEN 5
    WHEN 10 THEN 9
END
WHERE id IN (1, 2, 3, 4, 5, 6, 7, 8, 9, 10);