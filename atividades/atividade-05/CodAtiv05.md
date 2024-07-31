import sqlite3

conn = sqlite3.connect("tasks.db")
cursor = conn.cursor()

def create_table():
    cursor.execute("""
        CREATE TABLE IF NOT EXISTS tasks (
            id INTEGER PRIMARY KEY,
            description TEXT,
            completed INTEGER
        );
    """)
    conn.commit()

def create_task(description):
    cursor.execute("INSERT INTO tasks (description, completed) VALUES (?, 0)", (description,))
    conn.commit()

def list_tasks():
    cursor.execute("SELECT id, description, completed FROM tasks")
    tasks = cursor.fetchall()
    for task in tasks:
        print(f"ID: {task[0]}, Description: {task[1]}, Completed: {'Yes' if task[2] else 'No'}")

def mark_completed(task_id):
    cursor.execute("UPDATE tasks SET completed = 1 WHERE id = ?", (task_id,))
    conn.commit()

create_table()

description = input("Digite a descrição da tarefa: ")
create_task(description)

print("\nTarefas:")
list_tasks()

task_id = int(input("\nDigite o ID da tarefa a ser marcada como concluída: "))
mark_completed(task_id)

print("\nTarefas após marcar como concluída:")
list_tasks()

conn.close()
