<script setup>
import { ref } from 'vue';
import TaskList from './components/TaskList.vue';

const newTaskText = ref('');

const tasks = ref([
  { id: 1, text: 'Tarefa 1', done: true },
  { id: 2, text: 'Tarefa 2', done: false },
  { id: 3, text: 'Tarefa 3', done: false }
]);

const addTask = () => {
  if (newTaskText.value.trim() === '') {
    alert('A tarefa não pode ser vazia!');
    return;
  }

  const newId = tasks.value.length > 0
    ? Math.max(...tasks.value.map(t => t.id)) + 1
    : 1;

  tasks.value.push({
    id: newId,
    text: newTaskText.value.trim(),
    done: false
  });

  newTaskText.value = ''; 
};


const removeTask = (taskId) => {
  tasks.value = tasks.value.filter(task => task.id !== taskId);
};
</script>

<template>
  <div id="todo-app-wrapper">
    <header class="app-header">
      <h1>Lista de Tarefas</h1>
      <h5>(To-Do List)</h5>
    </header>

    <div class="task-form-section">
      <input
        type="text"
        v-model="newTaskText"
        placeholder="Adicione uma nova tarefa (Ex: Comprar pão)"
        @keyup.enter="addTask"
        class="task-input"
      />
     <button @click="addTask" class="add-button">
        Adicionar Tarefa
      </button>
    </div>

    <TaskList :tasks="tasks" @remove-task="removeTask" />
  </div>
</template>

<style scoped>
#todo-app-wrapper {
  
  max-width: 700px;
  margin: 50px auto;
  padding: 30px;
  border-radius: 12px;
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.1);
  background-color: #f7fafc;
  font-family: 'Arial', sans-serif;
  color: black;
  
}

.app-header {
  text-align: center;
  margin-bottom: 30px;
}

.app-header h1 {
  color: #2d3748;
  font-size: 2.2em;
  border-bottom: 2px solid #48bb78;
  display: flex;
  justify-content: center;
}
.app-header h5 {
  color: grey;
  font-size: 1em;
  display: flex;
  justify-content: center;
}


.task-form-section {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}

.task-input {
  flex-grow: 1;
  padding: 12px;
  border: 2px solid #e2e8f0;
  border-radius: 6px;
  font-size: 1em;
  transition: border-color 0.2s;
}

.task-input:focus {
  border-color: #48bb78;
  outline: none;
}

.add-button {
  padding: 12px 20px;
  background-color: #48bb78; /* Verde */
  color: white;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  font-weight: bold;
  transition: background-color 0.2s, transform 0.1s;
}

.add-button:hover {
  background-color: #256945;
}

.add-button:active {
  transform: scale(0.98);
}
</style>
