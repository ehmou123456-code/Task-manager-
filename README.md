# Task-manager-
 📝 Task Manager CLI A lightweight command-line app to manage daily tasks.   Add, list, and mark tasks as done — all stored in a simple JSON file.  
import json
import os

FILE = "tasks.json"

def load_tasks():
    if os.path.exists(FILE):
        with open(FILE, "r") as f:
            return json.load(f)
    return []

def save_tasks(tasks):
    with open(FILE, "w") as f:
        json.dump(tasks, f, indent=4)

def add_task(title):
    tasks = load_tasks()
    tasks.append({"title": title, "done": False})
    save_tasks(tasks)
    print(f"✅ وظیفه '{title}' اضافه شد.")

def list_tasks():
    tasks = load_tasks()
    for i, task in enumerate(tasks, 1):
        status = "✔️" if task["done"] else "❌"
        print(f"{i}. {task['title']} [{status}]")

def mark_done(index):
    tasks = load_tasks()
    if 0 <= index-1 < len(tasks):
        tasks[index-1]["done"] = True
        save_tasks(tasks)
        print(f"🎉 وظیفه '{tasks[index-1]['title']}' انجام شد.")

# نمونه استفاده
if __name__ == "__main__":
    add_task("نوشتن README برای پروژه دوم")
    list_tasks()
    mark_done(1)
