import json

class ToDoList:
    def __init__(self, filename='todo_list.json'):
        self.filename = filename
        self.tasks = self.load_tasks()

    def load_tasks(self):
        try:
            with open(self.filename, 'r') as file:
                return json.load(file)
        except FileNotFoundError:
            return []

    def save_tasks(self):
        with open(self.filename, 'w') as file:
            json.dump(self.tasks, file, indent=4)

    def add_task(self, task):
        self.tasks.append({'task': task, 'completed': False})
        self.save_tasks()

    def update_task(self, index, new_task):
        self.tasks[index]['task'] = new_task
        self.save_tasks()

    def complete_task(self, index):
        self.tasks[index]['completed'] = True
        self.save_tasks()

    def delete_task(self, index):
        del self.tasks[index]
        self.save_tasks()

    def display_tasks(self):
        for i, task in enumerate(self.tasks):
            status = "Done" if task['completed'] else "Not Done"
            print(f"{i + 1}. {task['task']} - {status}")

def main():
    todo_list = ToDoList()

    while True:
        print("\nTo-Do List:")
        todo_list.display_tasks()
        print("\nOptions:")
        print("1. Add Task")
        print("2. Update Task")
        print("3. Complete Task")
        print("4. Delete Task")
        print("5. Exit")

        choice = input("Choose an option: ")

        if choice == '1':
            task = input("Enter the task: ")
            todo_list.add_task(task)
        elif choice == '2':
            index = int(input("Enter task number to update: ")) - 1
            new_task = input("Enter new task: ")
            todo_list.update_task(index, new_task)
        elif choice == '3':
            index = int(input("Enter task number to complete: ")) - 1
            todo_list.complete_task(index)
        elif choice == '4':
            index = int(input("Enter task number to delete: ")) - 1
            todo_list.delete_task(index)
        elif choice == '5':
            break
        else:
            print("Invalid option. Please try again.")

if __name__ == "__main__":
    main()
To-Do List:

Options:
1. Add Task
2. Update Task
3. Complete Task
4. Delete Task
5. Exit
Invalid option. Please try again.
