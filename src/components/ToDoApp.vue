<template>
  <div class="container">
    <h1 class="header text-center">My vue to do list</h1>
    <div class="d-flex">
      <input
        v-model="task"
        type="text"
        placeholder="Enter your task"
        class="form-control"
      />
      <button @click="submitTask()" class="btn btn-warning rounded-0">SUBMIT</button>
    </div>
    <div>
      <table  class="table table-bordered mt-4">
        <thead>
          <tr>
            <th scope="col -4">Task</th>
            <th scope="col">Status</th>
            <th scope="col">#</th>
            <th scope="col">#</th>
          </tr>
        </thead>
        <tbody >
          <tr  v-for="(task, index) in tasks" :key="index">
            <td> <span :class="{'finished':task.status==='finished'}"> {{ task.name }}</span> </td>
            <td>
              <span @click="changeStatus(index)" class="status">{{task.status}}</span>
            </td>
            <td @click="updateTask(index)" class="update">update</td>
            <td @click="deleteTask(index)" class="delete">delete</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
  <!--task table-->
</template>

<script>
export default {
  name: "ToDoAPP",
  props: {
    msg: String,
  },
  data() {
    return {
      task: "",
      updatedTask: null,
      availableStatus: ["to-do", "in-prograss", "finished"],
      tasks: [
        {
          name: "go to gym",
          status: "to-do",
        },
        {
          name: "plat football",
          status: "in-prograss",
        },
      ],
    };
  },

  methods: {
    // this function for add task
    submitTask() {
      if (this.task.length === 0) return;
      if (this.updatedTask === null) {
        this.tasks.push({
          name: this.task,
          status: "to-do",
        });
      } else {
        this.tasks[this.updatedTask].name = this.task;
        this.updatedTask = null;
      }
      this.task = "";
      //=====================================
    },
    // this function for update task with
    updateTask(index) {
      this.task = this.tasks[index].name;
      this.updatedTask = index;
    },
    //=======================================
    // this function for delete task with
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },
    //=======================================
    // this function for change status
    changeStatus(index) {
      let newIndex = this.availableStatus.indexOf(this.tasks[index].status);
      if (++newIndex > 2) newIndex = 0;
      this.tasks[index].status=this.availableStatus[newIndex];
    },
    //=======================================
  },
};
</script>
.
<style scoped lang="scss">
.update,
.status {
  cursor: pointer;
}

.delete {
  cursor: pointer;
}

.finished{
  text-decoration: line-through;
}
</style>
