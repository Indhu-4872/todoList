<template>
<div class="card">
    <div class="cardcontent">
        <div class="todolist">{{todo.needto}}</div>
    </div>
     <div class="btn">
        <!-- <font-awesome-icon icon="user-secret" /> -->
        <font-awesome-icon class="icon" :icon="['fas', 'trash-alt']" @click="deleteClick"/>
        <!-- <i class="fas fa-trash-alt"></i> -->
    </div>
    <div class="editbtn">
        <font-awesome-icon class="icon" :icon="['fas', 'edit']" @click="editClick"/>
    </div>
</div>
</template>

<script>

import { library } from '@fortawesome/fontawesome-svg-core'
import { faTrashAlt, faEdit } from '@fortawesome/free-solid-svg-icons'
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'

library.add(faTrashAlt, faEdit)

export default {
  todo: 'Card',
  props: {
    todo: Object
  },
  components: {
    FontAwesomeIcon
  },
  methods: {
    deleteClick () {
      console.log('Deletebtn')
      this.$emit('onDeletebtn')
    },
    editClick () {
      console.log('EditBtn is clicked')
      this.$emit('onEditbtn')
    }
  }
}
</script>

<style scoped>
.card{
    display: flex;
    align-items: center;
    border-radius: 5px;
}
.cardcontent{
    width:750px;
}
.todolist{
    display: flex;
    flex-direction: column;
    background-color:white;
    padding: 20px;
    border-radius:5px;
    margin:20px;
    box-shadow: 5px 5px 15px rgb(0,0,0,.1)
}

.btn{
    padding: 8px 15px;
    border-radius:5px;
    margin: 20px;
    height: 30px;
    width: 50px;
    display: flex;
    justify-content: center;
    background-color: white;
    cursor: pointer;
    box-shadow: 5px 5px 15px rgb(0,0,0,.1);
}
.editbtn{
    padding: 8px 15px;
    border-radius:5px;
    margin: 20px;
    height: 30px;
    width: 50px;
    display: flex;
    justify-content: center;
    background-color: white;
    cursor: pointer;
    box-shadow: 5px 5px 15px rgb(0,0,0,.1);
}
.icon{
    color:rgb(190, 190, 229);
    font-size: 30px;
    /* cursor: pointer; */
}
</style>
