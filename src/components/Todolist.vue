<template>
<div>
  <h1>Hello From {{msg}} </h1>
  <div class="todo-input">
    <div class="todo-inner-input">
        <input type="text" v-model="task">
        <button @click="submitTask">Submit</button>
    </div>
    </div>
   
    <div class="todo-output">
   
      <table>
        <thead>
          <tr>
            <th>Name</th>
            <th>Status</th>
            <th>Action</th>
          </tr>
        </thead>
        <tbody>
          <tr  v-for="(tasks,index) in tasks" :key="index">
            <td>
              {{tasks.name}}
            </td>
            <td>
              {{tasks.status}}
            </td>
            <td>
              <button @click="editItem(index)"><i class="fas fa-edit"></i></button>
              <button @click="deleteItem(index)"><i class="fas fa-trash-alt"></i></button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
</div>

  
</template>

<script>
export default {
  name: 'Todolist',
  actionstatus: null,
  props: {
    msg: String
  },
  data() {
    return {
      task:"",
      tasks:[

      ],
      
    };
},
methods:{
  submitTask(){
    if(this.task.length==0){return;}
    if(this.actionstatus == null){
      this.tasks.push({
      name:this.task,
      status:"todo"
    })
    this.task=""
    }else{
      this.tasks[this.actionstatus].name = this.task
      this.actionstatus=null
        this.task=""
    }
    
  },
  deleteItem(index){
    this.tasks.splice(index,1);
  },
  editItem(index){
    this.actionstatus = index
    this.task = this.tasks[index].name
  }
}
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

h1{
  margin-top: 10px;
  text-align: center;
  color: #386068;
  font-family:  sans-serif;

}
.todo-input{
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 20px;
  flex-direction: row;
  background-color: darkcyan;
  padding: 10px;
}
.todo-input input{
 
  font-size: 1.1rem;
}
.todo-input input:focus{
  outline: none;
}
.todo-input button{
 
  font-size: 14px;
  padding: 5px;
}
.todo-input button:focus{
  outline: none;
}
.todo-inner-input{
  display: flex;
}
.todo-output{
  display: flex;
  align-items: center;
  justify-content: center;
  margin-top: 15px;
}

table, th, td {
  border: 1px solid gray;
  border-collapse: collapse;
  padding: 10px;
}
td button{
  margin: 4px;
}

</style>
