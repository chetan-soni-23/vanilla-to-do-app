# 📝 Simple Todo List (Vanilla JavaScript)

A clean and responsive **Todo List** application built with **HTML, CSS, and Vanilla JavaScript**.  
This app helps you stay organized, track your tasks, and monitor progress — without any frameworks.

---

## ✨ Features

- ➕ **Add new tasks** with a single click or pressing Enter  
- ✅ **Mark tasks as completed** or uncheck to reactivate  
- ✏️ **Edit tasks inline** with instant updates  
- 🗑️ **Delete tasks** with a confirmation modal  
- 🧹 **Clear all completed tasks** at once  
- 🔎 **Filter tasks**: All, Active, Completed  
- 📊 **Progress tracker** with percentage and progress bar  
- 💾 **LocalStorage support** – your tasks persist even after refreshing  
- 📱 **Responsive design** – works on mobile, tablet, and desktop  

## 🛠️ Technologies Used

- **HTML5** – semantic structure  
- **CSS3** – modern styling with responsive design  
- **JavaScript (ES6+)** – functionality, localStorage, DOM manipulation  

## 🔑 Main Functions

This Todo app is powered by a few key functions inside the `TodoApp` class:

---

### ➕ Add a Task 

📌 Creates a new task, saves it in localStorage, and re-renders the UI.
```js
addTask() {
    const text = this.taskInput.value.trim();
    if (!text) return;

    const task = {
        id: this.taskIdCounter++,
        text: text,
        completed: false,
        createdAt: new Date().toISOString(),
        updatedAt: new Date().toISOString()
    };

    this.tasks.push(task);
    this.taskInput.value = '';
    this.addBtn.disabled = true;

    this.saveTasks();
    this.render();
}
 ```
✅ Toggle Task Completion

📌 Marks a task as completed or active.
```js
toggleTask(id) {
    const task = this.tasks.find(t => t.id === id);
    if (task) {
        task.completed = !task.completed;
        task.updatedAt = new Date().toISOString();
        this.saveTasks();
        this.render();
    }
}
```

✏️ Edit a Task

📌 Allows inline editing of tasks and saves instantly.
```js
saveEdit(id, newText) {
    const task = this.tasks.find(t => t.id === id);
    if (task && newText.trim()) {
        task.text = newText.trim();
        task.updatedAt = new Date().toISOString();
        this.saveTasks();
    }
    this.currentEditId = null;
    this.render();
}
```

🗑️ Delete a Task

📌 Deletes a task after confirmation via modal.
```js
confirmDelete() {
    if (this.taskToDelete) {
        this.tasks = this.tasks.filter(t => t.id !== this.taskToDelete);
        this.saveTasks();
        this.render();
    }
    this.hideModal();
}
```
🧹 Clear Completed Tasks

📌 Clears all completed tasks with one click.
```js
clearCompletedTasks() {
    this.tasks = this.tasks.filter(t => !t.completed);
    this.saveTasks();
    this.render();
}
```
📊 Task Stats & Progress

📌 Calculates task statistics and updates the progress bar.
```js
getStats() {
    const total = this.tasks.length;
    const completed = this.tasks.filter(t => t.completed).length;
    const active = total - completed;
    const progressPercent = total > 0 ? Math.round((completed / total) * 100) : 0;

    return { total, completed, active, progressPercent };
}
```



