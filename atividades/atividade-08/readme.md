# bd-info-241
Repositório proposto para a disciplina de Banco de Dados.
---------------------------------
Turma: P4 Informática 2024.1
Aluno: José Maia Cavalcante Neto
---------------------------------
# Atividade 08
Usar o tutorial em https://www.youtube.com/watch?v=feGY977Tp-4
para instalar o LAMP no Docker.

OBS: (Atividade resolvida em sala pelo professor usando outros métodos.)

Exemplo do arquivo "docker-compose.yml"

```

version: '3.8'

services:
  mysql:
    image: mysql:8.0
    container_name: mysql_container
    environment:
      MYSQL_ROOT_PASSWORD: rootpassword
      MYSQL_DATABASE: mydatabase
      MYSQL_USER: myuser
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

# Modificações

  MYSQL_DATABASE: mydbjosemaia
  
  MYSQL_USER: myjosemaia

# Observações

Usando o Play With Docker, use "docker login" para rodar o comando "docker-compose up -d" por causa da limitação dada.
os comandos no docker:

"vi docker-compose.yml" (criar o arquivo docker-compose)

"wq" (gravar e sair do arquivo docker-compose)

"docker-compose -v" (Verificar Versão)

"docker-compose up -d" (Criar os contêineres)

Código para as tabelas:

```

CREATE TABLE TB_ALUNOS (
    id INT AUTO_INCREMENT NOT NULL,
    nome TEXT,
    PRIMARY KEY (id)
);

```

```

INSERT INTO TB_ALUNOS (nome) VALUES ("José Maia");

```
