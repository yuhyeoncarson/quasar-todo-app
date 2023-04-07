<template>
  <q-page>
    <!-- Input -->
    <div class="q-pa-sm bg-grey-12">
      <q-input
        @keyup.enter="addTask"
        bottom-slots
        v-model="newTask"
        placeholder="Add Task"
        :dense="dense"
      >
        <template v-slot:append>
          <q-btn flat icon="add" @click="addTask" />
        </template>
      </q-input>
    </div>
    <!-- List -->
    <q-list>
      <q-item v-for="task in tasks" :key="task.whatToDo">
        <q-item-section side>
          <q-checkbox v-model="task.isDone" />
        </q-item-section>
        <q-item-section>
          <q-item-label class="done">{{ task.whatToDo }}</q-item-label>
        </q-item-section>
        <q-item-section side v-if="task.isDone">
          <q-btn flat icon="delete" @click="deleteTask(task)" />
        </q-item-section>
      </q-item>
    </q-list>
    <!-- No Tasks -->
    <div v-if="!tasks.length" class="absolute-center text-h6 text-primary">
      Nothing To Do Today <q-icon name="mood" color="primary" />
    </div>
  </q-page>
</template>

<script>
export default {
  data() {
    return {
      newTask: "",
      tasks: [],
    };
  },

  methods: {
    addTask() {
      this.tasks.push({
        whatToDo: this.newTask,
        isDone: false,
      });
      this.newTask = "";
    },

    deleteTask(task) {
      this.tasks = this.tasks.filter((t) => t !== task);
    },
  },
};
</script>

<style lang="scss">
.isDone {
  text-decoration: line-through;
  color: lightgrey;
}
</style>
