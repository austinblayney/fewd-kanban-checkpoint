<template>
    <div class="task card">
        <div class="card-body">
            <h4>{{task.title}}</h4>
            <select @change="moveTask">
                <option v-for="list in lists" :value="list._id" :selected="task.listId == list._id">{{list.title}}</option>
            </select>
        </div>
        <div class="card-footer">
            <p>{{task.createdAt}}</p>
        </div>
    </div>
</template>

<script>
export default {
   name: "task",
   props: ['task'],
   data() {
      return {}
   },
   computed: {
       lists() {
           return this.$store.state.lists
       }
   },
   methods: {
       moveTask(e) {
           let listId = e.target.value
           this.$store.dispatch('moveTask', {taskId: this.task._id, listId})
       }
   },
   components: {}
}
</script>