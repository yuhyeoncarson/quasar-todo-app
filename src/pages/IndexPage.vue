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
          <q-btn round dense flat icon="add" @click="addTask" />
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
          <q-item-label>{{ task.whatToDo }}</q-item-label>
        </q-item-section>
      </q-item>
    </q-list>
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
  },
};
</script>
