<template>
  <div class="section is-small">
    <h1 class="subtitle">Your To-Do List</h1>
    <br />
    <div class="field has-addons">
      <div class="control">
        <input
          class="input is-rounded"
          type="text"
          placeholder="Add a task"
          v-model="task"
        />
      </div>
      <div class="control">
        <a class="button is-primary is-rounded" @click="addTask">
          <strong>+</strong>
        </a>
      </div>
    </div>

    <div class="buttons mt-6">
      <button
        class="button has-background-danger-light is-rounded"
        @click="isActive('todo')"
      >
        To Do
      </button>
      <button
        class="button has-background-success-light is-rounded"
        @click="isActive('completed')"
      >
        Completed
      </button>
    </div>

    <ul id="to-do-list" v-show="showToDo">
      <div v-if="toDoList.length == 0">
        <p class="has-text-grey-lighter">Nothing in To Do</p>
      </div>
      <div v-else>
        <li v-for="(t, index) in toDoList" :key="t.task">
          <div class="control is-size-5">
            <label class="radio has-text-danger-dark">
              <input
                type="radio"
                :id="t.task"
                :value="t.task"
                @change="addToCompleted(index)"
              />
              {{ t.task }}
              <small class="is-size-7 has-text-grey-lighter">
                (Added on {{ t.date }})</small
              >
            </label>
          </div>
        </li>
      </div>
    </ul>

    <ul id="completed list" v-show="showCompleted">
      <div v-if="completed.length == 0">
        <p class="has-text-grey-lighter">Nothing is completed</p>
      </div>
      <div v-else>
        <li v-for="t in completed" :key="t.date" class="has-text-success">
          - {{ t.task }} <small> is Completed</small>
        </li>
      </div>
    </ul>
  </div>
</template>

<script>
export default {
  name: "ToDo",
  data() {
    return {
      task: "",
      date: new Date().toDateString(),
      toDoList: [],
      completed: [],
      showToDo: true,
      showCompleted: false,
    };
  },
  methods: {

    /* when you click the + button to add task*/
    addTask() {
      const toDoData = {
        task: this.task,
        date: this.date,
      };
      if (this.task != "") {
        this.toDoList.push(toDoData);
      }
      this.task = "";
    },

   /* when you click the radio button on the task*/
    addToCompleted(index) {
      this.completed.push(this.toDoList[index]);
      if (index > -1) {
        this.toDoList.splice(index, 1);
      }
    },
    
    /* shows if to-do list is active or the completed list*/
    isActive(x) {
      if (x === "todo") {
        this.showToDo = true;
        this.showCompleted = false;
      }
      if (x === "completed") {
        this.showCompleted = true;
        this.showToDo = false;
      }
    },
  },
};
</script>

<style lang="scss" scoped>
</style>