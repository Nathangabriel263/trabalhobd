CREATE database Escola_bd
USE Escola;

CREATE TABLE cursos (
    id INT PRIMARY KEY,
    nome VARCHAR(100),
    tempo INT

CREATE TABLE professor (
    id INT PRIMARY KEY,
    nome VARCHAR(100),
    idade INT,
    telefone VARCHAR(50)
);


CREATE TABLE disciplina (
    id INT PRIMARY KEY,
    nome VARCHAR(100),
    tempo INT
);

CREATE TABLE alunos (
    id INT PRIMARY KEY,
    nome VARCHAR(100),
    cpf VARCHAR(11),
    idade INT,
    telefone VARCHAR(50)
    turma VARCHAR(50)
    );
# trabalhobd
-- =========================================
-- DCL - SEGURANÇA DO BANCO DE DADOS
-- =========================================

-- 1. Criar usuários
CREATE USER 'admin_db'@'localhost' IDENTIFIED BY 'admin123';
CREATE USER 'usuario_leitura'@'localhost' IDENTIFIED BY 'leitura123';
CREATE USER 'usuario_operacao'@'localhost' IDENTIFIED BY 'operacao123';

-- 2. Conceder permissões

-- Admin: todas as permissões no banco
GRANT ALL PRIVILEGES ON escola_db.* TO 'admin_db'@'localhost';

-- Usuário apenas leitura
GRANT SELECT ON escola_db.* TO 'usuario_leitura'@'localhost';

-- Usuário de operação (DML)
GRANT SELECT, INSERT, UPDATE, DELETE ON escola_db.* TO 'usuario_operacao'@'localhost';

-- Aplicar alterações
FLUSH PRIVILEGES;

-- 3. Revogação de permissões (exemplo)

-- Revogar DELETE do usuário de operação
REVOKE DELETE ON escola_db.* FROM 'usuario_operacao'@'localhost';

-- Aplicar novamente
FLUSH PRIVILEGES;

 INSERT INTO cursos (id, nome, tempo) VALUES
    (1, 'Informática', 24),
    (2, 'Administração', 18),
    (3, 'Eletrotécnica', 36);
  INSERT INTO professor (id, nome, idade, telefone) VALUES
(1, 'Marcos Oliveira', 40, '(11) 95555-1111'),
(2, 'Fernanda Lima', 35, '(11) 94444-2222'),
(3, 'Rafael Santos', 50, '(11) 93333-3333');
INSERT INTO disciplina (id, nome, tempo) VALUES
(1, 'Banco de Dados', 60),
(2, 'Programação', 80),
(3, 'Redes de Computadores', 50),
(4, 'Gestão Empresarial', 40);
INSERT INTO alunos (id, nome, cpf, idade, telefone) VALUES
(1, 'Ana Silva', '12345678901', 20, '(11) 99999-1111','A'),
(2, 'Bruno Costa', '23456789012', 22, '(11) 98888-2222','B'),
(3, 'Carla Souza', '34567890123', 19, '(11) 97777-3333','A'),
(4, 'Diego Pereira', '45678901234', 25, '(11) 96666-4444','B');

SELECT * FROM alunos;



UPDATE disciplina
SET tempo = 100
WHERE nome = 'Programação';


DELETE FROM alunos
WHERE turma = 'B';

SELECT 
    alunos.nome AS aluno,
    cursos.nome AS curso,
    disciplina.nome AS disciplina
FROM alunos
INNER JOIN cursos 
    ON alunos.id_curso = cursos.id
INNER JOIN disciplina
    ON disciplina.id_curso = cursos.id;

