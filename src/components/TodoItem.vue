<template>
    <!-- Contenedor principal del ítem de tarea -->
    <div class="todo-item-container">
        <!-- Contenedor del título y el estado de la tarea -->
        <div class="task-header">
            <!-- Muestra el título de la tarea y aplica un estilo tachado si la tarea está completada -->
            <h5 :style="{ textDecoration: completed ? 'line-through' : 'none' }">
                {{ title }}
            </h5>

            <!-- Muestra si la tarea está Completada o Pendiente -->
            <span :class="{'pending': !completed, 'completed': completed}">
                {{ completed ? 'Completada' : 'Pendiente' }}
            </span>
        </div>

        <!-- Contenedor de botones de acción -->
        <div class="task-actions">
            <!-- Botón para marcar la tarea como completada o pendiente -->
            <!-- Usamos un check (✔) como ícono -->
            <button @click="$emit('toggle-completion')" class="check-button">
                ✔
            </button>

            <!-- Botón para eliminar la tarea de la lista -->
            <!-- Usamos el ícono de una papelera (🗑️) -->
            <button @click="$emit('delTodo')" class="delete-button">
                🗑️
            </button>
        </div>
    </div>
</template>

<script>
export default {
    name: 'TodoItem',
    props: {
        title: String,      // Título de la tarea
        completed: Boolean, // Estado de la tarea (completada o pendiente)
    }
}
</script>

<style scoped>
/* Contenedor principal de la tarea */
.todo-item-container {
    border: 2px solid #ccc; /* Borde alrededor del componente */
    padding: 10px;
    margin-bottom: 10px;
    border-radius: 8px; /* Bordes redondeados */
    display: flex;
    flex-direction: column;
    background-color: #fff;
}

/* Contenedor del encabezado de la tarea */
.task-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

/* Título de la tarea */
.task-header h5 {
    margin: 0;
    font-size: 16px;
}

/* Estilos para las etiquetas de pendiente y completada */
.pending {
    background-color: yellow;
    padding: 3px 8px;
    border-radius: 4px;
}

.completed {
    background-color: green;
    color: white;
    padding: 3px 8px;
    border-radius: 4px;
}

/* Contenedor de los botones de acción */
.task-actions {
    display: flex;
    justify-content: space-between;
    margin-top: 10px;
}

/* Estilos para los botones */
button {
    background: none;
    border: none;
    font-size: 20px;
    cursor: pointer;
}

/* Cambia el color del botón al pasar el ratón */
button:hover {
    color: #007bff;
}

/* Estilo del botón de check (✔) */
.check-button {
    font-size: 24px;
}

/* Estilo del botón de eliminar (🗑️) */
.delete-button {
    font-size: 24px;
}
</style>
