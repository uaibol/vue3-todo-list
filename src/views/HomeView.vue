<template>
  
  <div class="container">
    
    <div class="card" style="width: 18rem;">
      <div class="card-body">
        <h5 class="card-title">Todo list</h5>
        <table class="table">
          <tbody>
            <tr v-for="todo of todos" :key="todo.id">
              <td>{{ todo.title }}</td>
              <td style="text-align: right;"><a href="#"><i class="bi bi-pencil-square"></i></a></td>
              <td style="text-algin:right;width: 10px;"><a href="#"><i class="bi bi-trash"></i></a></td>
            </tr>
          </tbody>
        </table>
      </div>
      <div class="card-footer bg-transparent">
        <div class="input-group mb-3">
          
      <input v-model="todoTitle" @keyup.enter="addTodo" type="text" class="form-control" placeholder="Enter your todo list" autofocus/>
      <button @click="addTodo()" class="btn btn-primary">Add</button>
      
      </div>
      </div>
    </div>

    
  </div>
</template>

<script>
// @ is an alias to /src
import axios from 'axios';
//import HelloWorld from '@/components/HelloWorld.vue';
const baseURL = "http://localhost:8081/todos"

export default {
  name: 'HomeView',
  components: {
    //HelloWorld,
  },
  data(){
    return {
      todos: [],
      todoTitle: "",
    
    };
  },
  async created() {
    await this.getTodos();
  },
  methods: {
    async addTodo() {
      await axios.post(baseURL, { title: this.todoTitle });
      //this.todos = [...this.todos, this.todoTitle];
      await this.getTodos();
      this.todoTitle = "";
      //console.log(res);

    },
    async getTodos() {
      try {
      const res = await axios.get(baseURL);
      this.todos =res.data;
      console.log(res);
    }catch (e){
      console.error(e);
    }
    }
  }
};
</script>
