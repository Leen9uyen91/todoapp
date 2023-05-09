<template>
   <div id="app">
      <h1>TodoApp</h1>
      <div class="top">
         <input type="text" placeholder="Enter here..." v-model="task">
         <button class="add-btn" @click="SubmitTask">ADD</button>
      </div>
      <div class="bottom">
         <input type="text" v-model="key">
         <button class="add-btn" @click="SearchTask">Tìm</button>
      </div>
    <!-- table -->
    <table border={3}>
        <thead>
            <tr>
                <th>ID</th>
                <th>Task</th>
                <th>Delete</th>
                <th>Edit</th>

            </tr>
        </thead>
        <tbody>
            <tr v-for="(task,index) in tasks" :key="index">
                <td>{{ task.id }}</td>
                <td>{{ task.name }}</td>

                <td>
                    <button class="del-btn" @click="deleteTask(index)">Delete</button>
                </td>
                <td>
                    <button class="edit-btn" @click="EditTask(index)">Edit</button>
                </td>
            </tr>

        </tbody>
    </table>
   </div>
</template>

<script>
import {v4 as uuidv4} from 'uuid'

export default {
  name: 'TodoApp',
  data() {
    return {
      key: "",
      task: "",
      editTask: null,
      tasks: [
        {
          name: 'React JS',
          id: uuidv4()
        },
        {
          name: 'Vue JS',
          id: uuidv4()
        },
        {
          name: 'Node JS',
          id: uuidv4()
        }
      ]
    }
    },
    
    methods: {

    // Delete task
    deleteTask(index) {
      console.log(index)
      this.tasks.splice(index, 1)
    },

    // Edit task
    EditTask(index) {
      console.log(index)
      this.task = this.tasks[index].name,
      this.editTask = index
    },

    // Add Task
    SubmitTask() {
      if(this.task.length === 0) {
        return;
      }
      if(this.editTask !=null) {
        this.tasks[this.editTask].name = this.task;
        this.editTask = null
      } else {
        this.tasks.push({
          name: this.task,
          id: uuidv4()
        })
      }
    },

    // Search Task
    SearchTask() {  

      this.tasks = this.tasks.filter((item) => this.key.indexOf(item.name) !== -1)
     
    }
  }

}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  max-width: 600px;
  margin: 0 auto;
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
input[type="text"] {
    height: 25px;
    border: 1px solid #3333;
    padding-left: 15px;
}

.top {
    margin-bottom: 10px;
}
</style>
