# codeway_do-list_application
import tkinter as tk
from tkinter import messagebox

class TodoListApp:
    def __init__(self, master):
        self.master = master
        self.master.title("To-Do List Application")
        self.master.geometry("400x300")

        self.tasks = []

        self.task_entry = tk.Entry(master, width=40)
        self.task_entry.grid(row=0, column=0, padx=10, pady=10)

        self.add_button = tk.Button(master, text="Add Task", command=self.add_task)
        self.add_button.grid(row=0, column=1, padx=5, pady=10)

        self.task_listbox = tk.Listbox(master, width=50, height=15)
        self.task_listbox.grid(row=1, column=0, columnspan=2, padx=10, pady=5)

        self.delete_button = tk.Button(master, text="Delete Task", command=self.delete_task)
        self.delete_button.grid(row=2, column=0, padx=5, pady=10)

        self.clear_button = tk.Button(master, text="Clear All", command=self.clear_all_tasks)
        self.clear_button.grid(row=2, column=1, padx=5, pady=10)

    def add_task(self):
        task = self.task_entry.get().strip()
        if task:
            self.tasks.append(task)
            self.update_task_listbox()
            self.task_entry.delete(0, tk.END)
        else:
            messagebox.showwarning("Warning", "Please enter a task!")

    def update_task_listbox(self):
        self.task_listbox.delete(0, tk.END)
        for task in self.tasks:
            self.task_listbox.insert(tk.END, task)

    def delete_task(self):
        try:
            index = self.task_listbox.curselection()[0]
            self.tasks.pop(index)
            self.update_task_listbox()
        except IndexError:
            messagebox.showwarning("Warning", "Please select a task to delete!")

    def clear_all_tasks(self):
        if messagebox.askyesno("Confirmation", "Are you sure you want to clear all tasks?"):
            self.tasks.clear()
            self.update_task_listbox()


root = tk.Tk()
app = TodoListApp(root)
root.mainloop()
