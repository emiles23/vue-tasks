<template>
  <div class="pt-20">
    <div class="flex justify-center">
      <button
        @click="addTask()"
        class="
          p-1
          px-10
          border-2 border-blue-900
          bg-blue-800
          hover:bg-blue-600
          text-white
        "
      >
        Agregar Tarea
      </button>

      <input
        v-model="inputName"
        placeholder="Buscar tarea. Ingrese el nombre"
        class="w-1/4 pl-4 ml-20 focus:outline-none border-2 border-green-700"
        type="search"
        aria-label="Search"
      />
    </div>
    <table class="w-screen text-center border-2">
      <tr class="bg-green-600 text-white">
        <td class="py-3">Estado</td>
        <td>Nombre</td>
        <td>Opciones</td>
      </tr>

      <tr v-for="(task, index) in filteredTasks" :key="index">
        <td>
          <input type="checkbox" v-model="task.status" />
        </td>

        <td>
          <input
            v-if="isTaskBeingUpdated(index)"
            v-model="task.name"
            class="focus:outline-none border-b-2 border-green-700"
            type="text"
          />

          <span v-else @dblclick="updateTask(index)">
            {{ task.name }}
          </span>
        </td>
        <td>
          <button
            v-if="isTaskBeingUpdated(index)"
            @click="saveTask(index)"
            class="
              p-1
              px-4
              border-2 border-blue-900
              bg-blue-800
              hover:bg-blue-600
              text-white
            "
          >
            Guardar
          </button>
          <button
            v-else
            @click="updateTask(index)"
            class="
              p-1
              px-6
              border-2 border-green-900
              bg-green-800
              hover:bg-green-600
              text-white
            "
          >
            Editar
          </button>
          <button
            @click="deleteTask(index)"
            class="
              p-1
              px-6
              border-2 border-red-900
              bg-red-800
              hover:bg-red-600
              text-white
            "
          >
            Eiminar
          </button>
        </td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      currentUpdatingTaskIndex: null,
      inputName: "",
      tasks: [
        {
          name: "aprender vue",
          status: true,
        },
        {
          name: "ir a merida",
          status: false,
        },
        {
          name: "comprar diccionario",
          status: false,
        },
      ],
    };
  },

  computed: {
    filteredTasks() {
      let filteredTasks = this.tasks;
      if (this.isATaskBeingUpdated()) return filteredTasks
      filteredTasks = filteredTasks.filter((task) =>
        task.name.includes(this.inputName)
      );
      return filteredTasks.sort((taskA, taskB) => {
        if (taskA.name > taskB.name) {
          return 1;
        }

        if (taskA.name < taskB.name) {
          return -1;
        }
        return 0;
      });
    },

  },

  methods: {
    addTask() {
      if (this.isATaskBeingUpdated()) return;
      this.tasks = [{ name: "", status: false }, ...this.tasks];
      this.currentUpdatingTaskIndex = 0;
    },

    saveTask() {
      if (this.tasks[this.currentUpdatingTaskIndex].name == "") return;
      this.currentUpdatingTaskIndex = null;
    },

    updateTask(index) {
      if (this.isATaskBeingUpdated()) return;
      this.currentUpdatingTaskIndex = index;
    },

    deleteTask(index) {
      this.currentUpdatingTaskIndex = null;
      this.tasks = [
        ...this.tasks.slice(0, index),
        ...this.tasks.slice(index + 1),
      ];
    },

    isATaskBeingUpdated() {
      return this.currentUpdatingTaskIndex !== null;
    },

    isTaskBeingUpdated(index) {
      return this.currentUpdatingTaskIndex === index;
    },
  },
};
</script>