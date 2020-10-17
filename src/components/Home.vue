<template>
<v-container>
  <h1>TodoList</h1>
  <p>
    <span>전체 할일: {{ todoList.length }}</span><br>
    <span>남은 할일: {{ countDone }}</span><br>
    <span>완료한 할일: {{ todoList.length - countDone }}</span>
  </p>
  <v-layout row wrap>
    <v-flex xs6>
      <List
        :todoList="todoList"
        @statusControl="statusControl"
        @listDelete="listDelete"
      />
    </v-flex>
    <v-flex xs6>
      <ListAdd 
        @listAdd="listAdd"
        @listEdit="listEdit"
      />
    </v-flex>
  </v-layout>
</v-container>
</template>

<script>
import List from './List'
import ListAdd from './ListAdd'
export default {
  components: {
    List,
    ListAdd
  },
  data(){
    return{
      todoList: []
    }
  },
  computed: {
    countDone(){
      let count = 0
      this.todoList.forEach(list => {
        if(list.status === 'done') count++;
      })
      return count;
    }
  },
  methods: {
    listAdd(memo, status){
       this.todoList.push({
         memo: memo,
         status: 'created'
      })
    },
    statusControl(index, status){
      this.todoList[index].status = status
    },
    listDelete(index){
      this.todoList.splice(index, 1)
    },
    listEdit(memo, index){
      this.todoList[index].memo = memo
    }
  }
}
</script>