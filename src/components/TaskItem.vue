<script setup>
import { computed } from 'vue';

const props = defineProps({
  task: {
    type: Object,
    required: true,
    validator: (value) => ['id', 'text', 'done'].every(key => key in value)
  }
});

const emit = defineEmits(['remove']);

const removeTask = () => {
  emit('remove', props.task.id);
};

const taskClasses = computed(() => [
  'task-item',
  { 'task-done': props.task.done }
]);
</script>

<template>
  <div :class="taskClasses">
    <input type="checkbox" v-model="task.done" class="task-checkbox" />
    
    <span class="task-text">{{ task.text }}</span>
    
    <button @click="removeTask" class="remove-btn">
      Remover
    </button>
  </div>
</template>

<style scoped>

.task-item {
  display: flex;
  align-items: center;
  padding: 12px 15px;
  margin-bottom: 8px;
  border-radius: 6px;
  background-color: #ffffff;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.05);
  transition: all 0.2s ease-in-out;
}

.task-done {
  background-color: #f0fff4; 
  color: #888;
  border-left: 5px solid #48bb78; 
}

.task-checkbox {
  margin-right: 15px;
  min-width: 18px;
  min-height: 18px;
}

.task-text {

  flex-grow: 1;
  font-size: 1.1em;
  color: #8d99aa
}

.task-done .task-text {
  text-decoration: line-through;
  color: #5a636e;
}

.remove-btn {
  background-color: #f56565;
  color: white;
  border: none;
  padding: 6px 12px;
  border-radius: 4px;
  cursor: pointer;
  margin-left: 20px;
  transition: background-color 0.2s;
}

.remove-btn:hover {
  background-color: #e53e3e;
}
</style>
