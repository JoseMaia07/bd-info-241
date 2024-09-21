# bd-info-241
Repositório proposto para a disciplina de Banco de Dados.
---------------------------------
Turma: P4 Informática 2024.1
Aluno: José Maia Cavalcante Neto
---------------------------------
# Avaliação Prática para N2

Terminar a avaliação-10 fazer consultas a tabela Matricula.

Criar scripts sql para para prova Prática

1) Listar todos os aluno reprovados. Nome do Aluno, Nome da Disciplina, Nome do Professor, N1,N2,Média,Faltas, Status da reprovação("Reprovado por Média", "Reprovado por Falta")
   
2) Listar todos os alunos aprovados. Nome Aluno, Nome da Disciplina, Nome do Professor, N1,N2,Média,Faltas, Status da reprovação("Aprovado por Média");
   
3) Listar a Quantidade de alunos aprovados;
   
4) Listar a Quantidade de alunos reprovados;

# Resolução usando o Play With Docker

## Primeiros passos

Utilize o comando a seguir para logar no docker evitando limite de pulls

```
docker login

```

Instale o mysql connector

```

pip install mysql-connector-python

```

## Crie o arquivo .yml com o comando 'vi' para abrir as portas e utilizar o MyPHP Admin

```

vi docker-compose.yml

```

Coloque alterando os dados necessários:

``` yaml

version: '3.8'

services:
  mysql:
    image: mysql:8.0
    container_name: mysql_container
    environment:
      MYSQL_ROOT_PASSWORD: rootpassword
      MYSQL_DATABASE: mydbjosemaia
      MYSQL_USER: myjosemaia
      MYSQL_PASSWORD: mypassword
    volumes:
      - mysql_data:/var/lib/mysql
    ports:
      - "3306:3306"

  phpmyadmin:
    image: phpmyadmin/phpmyadmin
    container_name: phpmyadmin_container
    environment:
      PMA_HOST: mysql
      PMA_PORT: 3306
      PMA_USER: root
      PMA_PASSWORD: rootpassword
    ports:
      - "8080:80"
    depends_on:
      - mysql

volumes:
  mysql_data:


```


## Criação do arquivo em python

Utilize o comando 'vi' para criar

```

vi main.py

```

Coloque alterando os dados necessários:


```

Falta

```

## Rodando

Utilize o comando python {nome do arquivo}.py

```

python main.py

```

