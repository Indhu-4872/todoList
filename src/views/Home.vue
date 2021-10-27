<template>
<div class="container">
  <div class="flexbox1">
    <Card v-for="todo in todos" :key="todo.id" :todo='todo' @onDeletebtn="onDeleteButton(todo.id)" @onEditbtn="onEditButton(todo.id)" />
  </div>

  <!-- <div class="container2"> -->
    <div class="flexbox2" >
        <input class="todobox" type="text" placeholder="Enter your todos" v-model="needto">
        <button class="addbtn" v-if="!toupdate" @click="addTodosButton">Add</button>
        <button class="addbtn" v-else-if="toupdate" @click="updateButton" >Update</button>
    <!-- </div> -->
  </div>
</div>
</template>

<script>
import Card from '../components/Card.vue'
import axios from 'axios'
export default {
  name: 'Home',
  components: {
    Card
  },
  data () {
    return {
      toupdate: false,
      todos: '',
      needto: '',
      idU: ''
    }
  },
  created () {
    this.todoslists()
  },
  methods: {
    todoslists () {
      const self = this
      axios.get('http://localhost:3000/todos')
        .then(function (response) {
          console.log('response')
          console.log(response.data)
          self.todos = response.data
        })
    },
    onDeleteButton (id) {
      const self = this
      axios.delete('http://localhost:3000/todos/' + id)
        .then(function () {
          console.log('delete todo')
          self.todoslists()
        })
    },
    onEditButton (id) {
      const self = this
      axios.get('http://localhost:3000/todos/' + id)
        .then(function (response) {
          console.log(response.data)
          self.needto = response.data.needto
          self.toupdate = true
          self.idU = response.data.id
          console.log(response.data.id)
        })
    },
    updateButton () {
      const self = this
      console.log('updateeeee')
      axios.put('http://localhost:3000/todos/' + this.idU, {
        needto: this.needto
      })
        .then(function (response) {
          console.log('update is being processing')
          console.log(response.data)
          self.todoslists()
          self.needto = ''
          self.toupdate = false
        })
    },
    addTodosButton () {
      const self = this
      axios.post('http://localhost:3000/todos', {
        needto: this.needto
        // neddto: 'trgfv trgfbv 56tygrf 6ytrgf '
      })
        .then(function (response) {
          console.log('add Todos')
          console.log(response.data)
          self.todoslists()
          self.needto = ''
        })
    }
  }
}
</script>

<style>
.container{
  display: flex;
  flex-direction: column;
}
.flexbox1{
  /* background-color: green; */
  display: flex;
  align-items: center;
  /* margin: 100px; */
  justify-content: center;
  flex-direction: column;
}
.displaybox{
  padding: 15px;
  margin: 10px;
  border-radius: 5px;
  width: 700px;
}
.flexbox2{
  background-color: rgb(135, 135, 209);
  display: flex;
  align-items: center;
  /* margin: 100px; */
  justify-content: center;
  position: inherit;
}
.todobox{
  padding: 15px;
  margin: 10px;
  /* margin-left: 80px; */
  /* border: none; */
  border-radius: 5px;
  width: 750px;

}
.addbtn{
  padding: 10px;
  margin: 10px;
  border-radius: 5px;
  cursor: pointer;
  font-weight: bold;
  height:40px;
  width:100px;
}
</style>
