<template>
  <div class="caintaner">
    <h1 class="text-center">Todo App</h1>
    <div>
      <input type="text" v-model="task" placeholder="Enter here.." />
      <button class="add-btn" @click="SubmitTask">ADD</button>
    </div>
    <table border="{3}">
      <thead>
        <tr>
          <th>ID</th>
          <th>Task</th>
          <th>Edit</th>
          <th>Delete</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task, index) in tasks" :key="index">
          <td>{{ task.id }}</td>
          <td>{{ task.name }}</td>
          <td>
            <button class="edit-btn" @click="EditTask(index)">Edit</button>
          </td>
          <td>
            <button class="del-btn" @click="deleteTask(index)">Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "TodoApp",
  props: {
    msg: String,
  },
  data() {
    return {
      task: "",
      editTask: null,
      tasks: [],
    };
  },
  methods: {
    SubmitTask() {
      if (this.task.length === 0) {
        return;
      }
      if (this.editTask != null) {
        this.tasks[this.editTask].name = this.task;
        this.editTask = null;
      } else {
        this.tasks.push({
          name: this.task,
          id: this.task.length,
        });
      }
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },

    EditTask(index) {
      (this.task = this.tasks[index].name), (this.editTask = index);
    },
  },
};
</script>

<style scoped>
.caintaner {
  width: 600px;
  margin: auto;
}

table {
  font-family: arial, sans-serif;
  border-collapse: collapse;
  width: 100%;
  margin-top: 20px;
}

td,
th {
  border: 1px solid #dddddd;
  text-align: center;
  padding: 8px;
}

tr:nth-child(even) {
  background-color: #dddddd;
}

.add-btn {
  border: none;
  width: 100px;
  height: 30px;
  padding: 2px;
  background-color: teal;
  color: white;
}

.del-btn {
  border: none;
  background-color: red;
  color: white;
}

.edit-btn {
  border: none;
  background-color: #77b631;
  color: white;
}
</style>
