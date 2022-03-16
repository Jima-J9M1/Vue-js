<template>
<div class="container">
  <h1 class="text-center mt-5">TODO List</h1>
  <div class="d-flex">
    <input v-model="task" type="text" class="form-control" placeholder="task-todo">
    <button @click="submitTodo" class="btn btn-warning">Submit</button>
  </div>
  <table class="table table-bordered">
  <thead>
    <tr>
      <th scope="col">task</th>
      <th scope="col">status</th>
      <th scope="col">#</th>
      <th scope="col">#</th>
    </tr>
  </thead>
  <tbody>
    <tr  v-for="(task,index) in tasks" :key="index">
      <td>
        <span :class="{'finished': task.status === 'finished'}">{{task.name}}</span>
        </td>
      <td style="width:120px">
        <span class="pointer width=120px" @click="changeStatus(index)" 
        :class="{'text-danger': task.status === 'to-do',
        'text-warning': task.status === 'in-order',
        'text-success': task.status === 'finished'
        }">
        {{  firstCharUpper(task.status) }}
        </span></td>
      <td>
        <div class="text-center" @click="editTask(index)">
          <span class="fa fa-pen"></span> 
        </div>
      </td>
      <td>
        <div class="text-center" @click="deleteTask(index)">
          <span class="fa fa-trash"></span> 
        </div>
      </td>
    
    </tr>
  </tbody>
</table>
</div>
</template>

<script>
export default {
  name: 'TodoApp',
  props: {
    msg: String
  },
  data(){
    return {
    task:'',
    editedTask : null,
    availableStatus : ['to-do','in-order','finished'],
    tasks:[
      {
        name: "Meet with matiyas",
        status: "in-order"
      },
      {
        name:"Go to sport",
        status:"finished"
      }
    ]
    }
  },
  methods : {
    submitTodo() {
      if(this.task.length === 0) return;
      if(this.editedTask == null) {
      this.tasks.push({
        name:this.task,
        status:'To-do'
      })
      }else{
       this.tasks[this.editedTask].name = this.task
      }
    },
    deleteTask(index) {
    this.tasks.splice(index,1);
    },
     editTask(index) {
    this.task = this.tasks[index].name,
    this.editedTask = index
  },
  changeStatus(index) {
    let newIndex = this.availableStatus.indexOf(this.tasks[index].status);
    if (++newIndex > 2) newIndex = 0;
    this.tasks[index].status = this.availableStatus[newIndex];
  },
  firstCharUpper(str) {
    return str.charAt(0).toUpperCase() + str.slice(1);
  }
  }
}
</script>
<style scoped>
.pointer{
  cursor:pointer;
}
.finished{
  text-decoration: line-through;
}
</style>
<!-- Add "scoped" attribute to limit CSS to this component only -->
