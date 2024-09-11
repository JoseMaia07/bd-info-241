# bd-info-241
Repositório proposto para a disciplina de Banco de Dados.
---------------------------------
Turma: P4 Informática 2024.1
Aluno: José Maia Cavalcante Neto
---------------------------------
# Atividade 09
Usar as informações definidas na Avaliação-08 e o prompt da aula do dia 09-09-2024.  Executar o programa Python no ambiente do Play with Docker incluindo a seguinte funcionalidade:
Ler todos os registros da tabela TB_ALUNOS e mostrar o status de Aprovação. Usando a seguinte lógica:

a) Se o numero de faltas for maior ou igual a 20 setar o atributo Aprovado_SN com FALSO (REPROVADO) ;

B) Se a média Aritmética de N1 e N2 for < 6.0   setar o atributo Aprovado_SN com FALSO (REPROVADO) ;

# É preciso logar inicialmente

```

docker login

```

# docker-compose.yml

Para abrir as portas

```

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

# executar o arquivo criado anteriormente

```

docker-compose up -d

```

# Crie o arquivo python para criar a tabela e inserir valores

```

import mysql.connector

mydb = mysql.connector.connect(
  host="localhost",
  user="myjosemaia",
  password="mypassword",
  database="mydbjosemaia"
)

mycursor = mydb.cursor()

mycursor.execute("""CREATE TABLE IF NOT EXISTS TB_ALUNOS (
  id INT AUTO_INCREMENT NOT NULL,
  nome TEXT,
  nota_N1 INT,
  nota_N2 INT,
  media FLOAT,
  faltas INT,
  Aprovado_SN BOOLEAN,
  PRIMARY KEY (id)
);""")

mycursor.executemany('INSERT INTO TB_ALUNOS (nome, nota_N1, nota_N2, faltas) VALUES (%s, %s, %s, %s);', [
    ("Leandro", 9, 10, 10),
    ("Ana Lívia", 0, 10, 0),
    ("José Maia", 10, 10, 1),
    ("Kelwin", 9, 6, 30)
])

mydb.commit()

mycursor.execute("SELECT * FROM TB_ALUNOS")
meuresultado = mycursor.fetchall()

for item in meuresultado:
    id, nome, nota_N1, nota_N2, media, faltas, aprovado_sn = item

    media_parcial = (2 * nota_N1 + 3 * nota_N2) / 5

    if media_parcial < 6.0 or faltas >= 20:
        aprovado_sn = False
    else:
        aprovado_sn = True

    mycursor.execute('UPDATE TB_ALUNOS SET Aprovado_SN = %s, media = %s WHERE id = %s;', (aprovado_sn, media_parcial, id))

mydb.commit()

mycursor.execute("SELECT * FROM TB_ALUNOS")
meuresultado = mycursor.fetchall()

for item in meuresultado:
    print(item)

mycursor.close()
mydb.close()


```

# importe o mysql connector

```

pip install mysql-connector-python

```

# execute o arquivo python

```

python docker-python.yml

```
