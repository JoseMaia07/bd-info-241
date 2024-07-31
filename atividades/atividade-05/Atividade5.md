# bd-info-241
Repositório proposto para a disciplina de Banco de Dados.
---------------------------------
Turma: P4 Informática 2024.1
Aluno: José Maia Cavalcante Neto
---------------------------------
Atividade-05
Executar o programa em Python demonstrado na aula em 29-07-2024. 

Evidenciar a execução printando a saída e postando no Google Classroom.

Incluir o texto do programa no Github e ´postar do Google Classroom o caminho do Github.

---------------------------------
código utilizado:
import sqlite3

# Conexão com o Banco de Dados
conn = sqlite3.connect("tasks.db")
cursor = conn.cursor()

# Função para criar a tabela tasks
def create_table():
    cursor.execute("""
        CREATE TABLE IF NOT EXISTS tasks (
            id INTEGER PRIMARY KEY,
            description TEXT,
            completed INTEGER
        );
    """)
    conn.commit()

# Função para criar uma nova tarefa
def create_task(description):
    cursor.execute("INSERT INTO tasks (description, completed) VALUES (?, 0)", (description,))
    conn.commit()

# Função para listar todas as tarefas
def list_tasks():
    cursor.execute("SELECT id, description, completed FROM tasks")
    tasks = cursor.fetchall()
    for task in tasks:
        print(f"ID: {task[0]}, Description: {task[1]}, Completed: {'Yes' if task[2] else 'No'}")

# Função para marcar uma tarefa como concluída
def mark_completed(task_id):
    cursor.execute("UPDATE tasks SET completed = 1 WHERE id = ?", (task_id,))
    conn.commit()

# Crie a tabela tasks se ela não existir
create_table()

# Criar uma nova tarefa
description = input("Digite a descrição da tarefa: ")
create_task(description)

# Listar todas as tarefas
print("\nTarefas:")
list_tasks()

# Marcar uma tarefa como concluída
task_id = int(input("\nDigite o ID da tarefa a ser marcada como concluída: "))
mark_completed(task_id)

# Listar todas as tarefas novamente
print("\nTarefas após marcar como concluída:")
list_tasks()

# Fechar a conexão com o banco de dados
conn.close()
