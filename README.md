CREATE DATABASE faculdade;
USE faculdade;

CREATE TABLE aluno(
id_aluno_matricula INT PRIMARY KEY NOT NULL UNIQUE AUTO_INCREMENT,
nome_aluno VARCHAR(50) NOT NULL,
rg VARCHAR(45) NOT NULL,
cpf VARCHAR(45) NOT NULL,
data_nascimento DATE NOT NULL);

CREATE TABLE telefone(
id_telefone INT PRIMARY KEY NOT NULL UNIQUE AUTO_INCREMENT,
telefone VARCHAR(45) NOT NULL,
fk_aluno_matricula INT);

ALTER TABLE telefone ADD CONSTRAINT FOREIGN KEY (fk_aluno_matricula) REFERENCES aluno (id_aluno_matricula);

CREATE TABLE email(
id_email INT PRIMARY KEY NOT NULL UNIQUE AUTO_INCREMENT,
email VARCHAR(255) NOT NULL,
fk_aluno_matricula INT);

ALTER TABLE email ADD CONSTRAINT FOREIGN KEY (fk_aluno_matricula) REFERENCES aluno (id_aluno_matricula);

CREATE TABLE endereco(
id_endereco INT PRIMARY KEY NOT NULL UNIQUE AUTO_INCREMENT,
logradouro VARCHAR(50) NOT NULL,
bairro VARCHAR(45) NOT NULL,
cep VARCHAR(45) NOT NULL,
cidade VARCHAR(45) NOT NULL,
estado VARCHAR(45) NOT NULL,
pais VARCHAR(45) NOT NULL,
fk_aluno_matricula INT);

ALTER TABLE endereco ADD CONSTRAINT FOREIGN KEY (fk_aluno_matricula) REFERENCES aluno (id_aluno_matricula);

 CREATE TABLE curso(
 id_curso INT PRIMARY KEY NOT NULL UNIQUE AUTO_INCREMENT,
 nome_curso VARCHAR(55) NOT NULL,
 duracao_semestres INT NOT NULL);
 
 CREATE TABLE professor(
 id_professor INT PRIMARY KEY NOT NULL UNIQUE AUTO_INCREMENT,
 nome_professor VARCHAR(50) NOT NULL,
 materia VARCHAR(50) NOT NULL);
 
 CREATE TABLE turma(
 id_turma INT PRIMARY KEY NOT NULL UNIQUE AUTO_INCREMENT,
 fk_aluno_matricula INT,
 fk_nome_aluno VARCHAR(50),
 fk_id_curso INT,
 fk_id_professor INT);
 
 ALTER TABLE turma ADD CONSTRAINT FOREIGN KEY (fk_aluno_matricula) REFERENCES aluno (id_aluno_matricula);
 ALTER TABLE turma ADD CONSTRAINT FOREIGN KEY (fk_id_curso) REFERENCES curso (id_curso);
 ALTER TABLE turma ADD CONSTRAINT FOREIGN KEY (fk_id_professor) REFERENCES professor (id_professor);
 ALTER TABLE turma DROP fk_nome_aluno;
 
 CREATE TABLE notas(
 id_nota INT PRIMARY KEY NOT NULL UNIQUE AUTO_INCREMENT,
 fk_aluno_matricula INT,
 fk_id_turma INT,
 fk_id_professor INT,
 fk_id_curso INT,
 nota_final DECIMAL NOT NULL,
 data_lancamento DATE NOT NULL);
 
  ALTER TABLE notas ADD CONSTRAINT FOREIGN KEY (fk_aluno_matricula) REFERENCES aluno (id_aluno_matricula);
  ALTER TABLE notas ADD CONSTRAINT FOREIGN KEY (fk_id_turma) REFERENCES turma (id_turma);
  ALTER TABLE notas ADD CONSTRAINT FOREIGN KEY (fk_id_professor) REFERENCES professor (id_professor);
  ALTER TABLE notas ADD COLUMN fk_id_curso INT;
  ALTER TABLE notas ADD CONSTRAINT FOREIGN KEY (fk_id_curso) REFERENCES curso (id_curso);
  
INSERT INTO aluno 
(nome_aluno, data_nascimento, rg, cpf)
 VALUES 
('Maria Souza', '2004-05-10', '123456789', '111.222.333-44'),
('João Oliveira', '2003-08-15', '987654321', '222.333.444-55'),
('Ana Silva', '2005-02-20', '555555555', '333.444.555-66'),
('Pedro Santos', '2004-11-01', '444444444', '444.555.666-77'),
('Bruna Lima', '2003-09-25', '777777777', '555.666.777-88'),
('Carlos Almeida', '2004-06-18', '666666666', '666.777.888-99'),
('Fernanda Costa', '2005-03-13', '999999999', '777.888.999-00'),
('Lucas Pereira', '2003-10-22', '222222222', '888.999.000-11'),
('Isabela Fernandes', '2004-07-30', '111111111', '999.000.111-22'),
('Gustavo Machado', '2003-04-14', '333333333', '000.111.222-33');
