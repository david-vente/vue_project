<template>
    <div class="add-task-container">
        <h1>Añadir Tarea</h1>
        <div class="input-group">
            <input 
                v-model="newTask" 
                @keyup.enter="addTask" 
                placeholder="Añadir nueva tarea" 
                class="task-input"
            />
            <button @click="addTask" class="add-button">Añadir</button>
        </div>
        <div v-if="tasks.length > 0" class="task-list">
            <!-- Usando el componente TodoItem para cada tarea -->
            <TodoItem
                v-for="task in tasks"
                :key="task.id"
                :title="task.todo"
                :completed="task.completed"
                @toggle-completion="toggleTaskCompletion(task)"
                @delTodo="deleteTask(task)"
            />
        </div>
    </div>
</template>


<script>
import TodoItem from '@/components/TodoItem.vue';

export default {
    name: "TaskList",
    components: {
        TodoItem,
    },
    data() {
        return {
            tasks: [], // Almacenamiento local de las tareas traídas de la API
            newTask: "", // Campo para ingresar la nueva tarea
        };
    },
    methods: {
        // Llamada para obtener las tareas desde la API externa
        async fetchTasks() {
            try {
                const response = await fetch('https://dummyjson.com/todos');
                const data = await response.json();
                this.tasks = data.todos;
            } catch (error) {
                console.error("Error al obtener las tareas:", error);
            }
        },

        // Agregar una nueva tarea
        addTask() {
            if (this.newTask.trim() === "") return; // Verifica si el campo no está vacío

            // Crear la nueva tarea
            const newTask = {
                id: Date.now(), // Genera un ID único basado en la hora actual
                todo: this.newTask,
                completed: false,
            };

            // Añadir la nueva tarea a la lista
            this.tasks.unshift(newTask);

            // Limpiar el campo de entrada
            this.newTask = "";
        },

        // Cambiar el estado de una tarea (completada/no completada)
        toggleTaskCompletion(task) {
            task.completed = !task.completed;
        },

        // Eliminar la tarea seleccionada
        deleteTask(task) {
            this.tasks = this.tasks.filter((t) => t.id !== task.id);
        },
    },
    created() {
        // Cargar tareas automáticamente cuando el componente se monta
        this.fetchTasks();
    },
};
</script>

<style scoped>
.add-task-container {
    display: flex;
    flex-direction: column;
    align-items: center; /* Centra el contenido en el eje transversal (horizontal) */
    justify-content: flex-start; /* Alinea los elementos al principio en el eje principal (vertical) */
    padding: 20px;
    margin-top: 20px;
}

.input-group {
    display: flex;
    margin-bottom: 20px;
    justify-content: center;
}

.task-input {
    padding: 8px;
    margin-right: 10px;
    border: 1px solid #ccc;
    border-radius: 4px;
}

.add-button {
    padding: 8px 12px;
    border: none;
    border-radius: 4px;
    background-color: #007bff;
    color: white;
    cursor: pointer;
}

.add-button:hover {
    background-color: #0056b3;
}

/* Estilos para las tareas */
.completed {
    text-decoration: line-through;
    color: gray;
}
</style>
