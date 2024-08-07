# bd-info-241
Repositório proposto para a disciplina de Banco de Dados.
---------------------------------
Turma: P4 Informática 2024.1
Aluno: José Maia Cavalcante Neto
---------------------------------
## Atividade_06
Desenvolver um Backend Python que usa FASTAPI 

Como um programador Python, crie uma aplicação backend que usa o framework FASTAPI seguindo os seguintes passos:
1) Crie um banco de dados SQLITE3 com o nome dbalunos.db.

2) Crie uma entidade aluno que será persistida em uma tabela TB_ALUNO com os seguintes campos:
id chave primária do tipo inteiro com autoincremento;
aluno_nome do tipo string com tamanho 50;
endereço       do tipo string com tamanho 100;

3) Crie os seguintes endpoints FASTAPI abaixo descritos:
   
a) criar_aluno grava dados de um objeto aluno na tabela TB_ALUNO;

b) listar_alunos ler todos os registros da tabela TB_ALUNO; 

c) listar_um_aluno ler um registro da tabela TB_ALUNO a partir do campo id; 

d) atualizar_aluno atualiza um registro da tabela TB_ALUNO a partir de um campo id e dos dados de uma entidade aluno; 

e) excluir_aluno exclui um registro da tabela TB_ALUNO a partir de um campo id e dos dados de uma entidade aluno;

## Como usar:
Baixe:

pip install fastapi

pip install pydantic

pip install uvicorn

## Interagir:

uvicorn main:app --host 0.0.0.0 --port 8000
(Substitua main pelo nome do arquivo principal)

## Criar Aluno:

curl -X POST \
  http://localhost:8000/alunos/ \
  -H 'Content-Type: application/json' \
  -d '{"aluno_nome": "João Silva", "endereco": "Rua dos Alunos, 123"}'

## Listar todos os alunos:

curl -X GET \
  http://localhost:8000/alunos/

## Listar um aluno:

curl -X GET \
  http://localhost:8000/alunos/1

## Atualizar um aluno:

curl -X PUT \
  http://localhost:8000/alunos/1 \
  -H 'Content-Type: application/json' \
  -d '{"aluno_nome": "João Silva Updated", "endereco": "Rua dos Alunos, 123 Updated"}'

  ## Deletar um aluno:

curl -X DELETE \
  http://localhost:8000/alunos/1


