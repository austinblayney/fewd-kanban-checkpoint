<template>
  <div class="board">
    {{board.title}}
    <list v-for="list in lists" :listData='list'></list>
    <form @submit.prevent="addList">
      <input v-model="newList.title" type="text" required placeholder="List Title">
      <button type="submit">Submit</button>
    </form>
  </div>
</template>

<script>
  import List from '@/components/List.vue'
  export default {
    name: "board",
    props: ["boardId"],
    mounted() {
      this.$store.dispatch('getLists', this.boardId)
    },
    data() {
      return {
        newList: {
          title: ''
        }
      }
    },
    computed: {
      board() {
        return this.$store.state.boards.find(b => b._id == this.boardId) || { title: 'Loading...' }
      },
      lists() {
        return this.$store.state.lists
      }
    },
    methods: {
      addList() {
        let list = { ...this.newList, boardId: this.boardId }
        this.$store.dispatch('addList', list)
        this.newList = {
          title: ''
        }
      }
    },
    components: {
      List
    }
  };
</script>
<style>
  .board {
    background-image: url("https://scontent-sea1-1.xx.fbcdn.net/v/t1.0-9/1922177_587923481301426_1171404669_n.jpg?_nc_cat=102&_nc_ht=scontent-sea1-1.xx&oh=6c9193cdd728760efdd546b9218ed30f&oe=5D02439F");
    background-size: cover;
    background-repeat: no-repeat
  }
</style>