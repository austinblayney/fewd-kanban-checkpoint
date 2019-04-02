<template>
<div class="col-6 col-md-3">
   <div class="card">
     <div class="card-header d-flex">
       <h3>{{listData.title}}</h3>
       <button @click="deleteList">Delete</button>
     </div>
     <div class="card-body">
        <task v-for="task in tasks" :task="task"/>
        <form @submit.prevent="addTask">
          <input type="text" required v-model="newTask.title" placeholder="Add a task">
          <button type="submit">Submit</button>
        </form>
     </div>
   </div>
</div>  
</template>

<script>
import Task from '@/components/Task.vue'
export default {
  name: 'List',
  props: ['listData'],
  data() {
    return {
      newTask: {
        title: ''
      }
    }
  },
  computed: {
    tasks() {
      return this.$store.state.tasks[this.listData._id] || []
    }
  },
  methods: {
    deleteList() {
      this.$store.dispatch('deleteList', this.listData)
    },
    addTask() {
      //object destructuring, this is the same as with actions in the store
      let { boardId, _id: listId } = this.listData
      this.$store.dispatch('addTask', {
        ...this.newTask,
        boardId,
        listId
      })
      this.newTask.title = ''
    }
  },
  components: {
    Task
  }
}
</script>

<style scoped>
</style>
