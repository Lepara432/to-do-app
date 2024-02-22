<template>
  <section>
    <div id="header">
      <div class="text">
        <h1>Manage your to do list</h1>
        <p>Click on checkbox to drag and drop to done</p>
      </div>
      <div class="photo">
        <img src="./assets/todo.jpg" alt="Todo img" />
      </div>
    </div>

    <div id="main-container">
      <div class="left-container">
        <div class="top-container">
          <h2 class="to-do">
            <input type="text" v-model="task" placeholder="Enter task" />
          </h2>
          <button @click="submitTask">Submit</button>
        </div>

        <div
          draggable="true"
          v-for="(task, index) in todoList"
          :key="index"
          class="task"
        >
          <input
            type="checkbox"
            v-model="task.done"
            @change="toggleDone(task)"
          />
          <span>{{ task.label }} </span>
          <button @click="editTask(index)">Edit</button>
          <button @click="deleteTaskfromtodoList(index)">Remove</button>
        </div>
      </div>

      <div class="right-container">
        <div class="top-container">
          <h2>Done</h2>
          <button @click="deleteAll(index)">Delete All</button>
        </div>

        <div
          draggable="true"
          v-for="(task, index) in doneList"
          :key="index"
          class="task"
        >
          <input
            type="checkbox"
            v-model="task.done"
            @change="toggleDone(task)"
          />

          <span>{{ task.label }}</span>
          <button @click="deleteTaskfromdoneList(index)">Remove</button>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import draggable from "vuedraggable";

export default {
  components: {
    draggable,
  },
  data() {
    return {
      task: "",
      todoList: [],
      doneList: [],
    };
  },
  methods: {
    submitTask() {
      if (this.task.length === 0) return;
      if (this.editedTask != null) {
        this.todoList[this.editedTask].label = this.task;
        this.editedTask = null;
      } else {
        this.todoList.push({
          label: this.task,
          done: false,
        });
      }
      this.task = "";
    },

    toggleDone(task) {
      if (task.done) {
        this.doneList.push(task);
        this.todoList = this.todoList.filter((param) => param !== task);
      } else {
        this.todoList.push(task);
        this.doneList = this.doneList.filter((param) => param !== task);
      }
    },
    deleteTaskfromtodoList(index) {
      this.todoList.splice(index, 1);
    },
    deleteTaskfromdoneList(index) {
      this.doneList.splice(index, 1);
    },
    editTask(index) {
      this.task = this.todoList[index].label;
      this.editedTask = index;
    },
    deleteAll(index) {
      this.doneList.splice(this.deleteAll);
    },
  },
};
</script>

<style>
#header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin: 0 100px;
}

img {
  width: 200px;
}
#main-container {
  display: flex;
  justify-content: space-around;
}
.left-container,
.right-container {
  width: 550px;
  height: fit-content;
}
.top-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-bottom: 2px solid black;
}
.bottom-container span {
  width: fit-content;
}

.task {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin: 5px;
  padding: 5px;
  border-radius: 3px;
  cursor: pointer;
}
.done {
  color: gray;
}
h2 {
  margin-left: 10px;
}
button {
  margin-right: 20px;
  width: 100px;
  height: fit-content;
  border-radius: 30px;
}
button:hover {
  cursor: pointer;
  background: black;
  color: white;
}
.to-do input {
  font-size: 20px;
  width: fit-content;
  height: fit-content;
}
</style>
