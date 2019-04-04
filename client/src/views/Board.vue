<template>
  <div class="board container-fluid">
    {{board.title}}
    <div class="row">
      <list v-for="list in lists" :listData='list'></list>
      <form class="col-6 col-md-3 card" @submit.prevent="addList">
        <input v-model="newList.title" type="text" required placeholder="List Title">
        <button type="submit">Submit</button>
      </form>
    </div>
  </div>
</template>

<script>
  import List from '@/components/List.vue'
  export default {
    name: "board",
    props: ["boardId"],
    mounted() {
      this.$store.dispatch('getLists', this.boardId)
      this.$store.dispatch('getTasks', this.boardId)
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
    background-image: url("https://lh3.googleusercontent.com/_F7EsZp7K7FNaJQU_BZhzoFYbrlB7jRVChPgwkU1n096C6bhIE0EAwBrrD4n8rBotxph_qyUwLOHCunUSrZYen7ZNgyPUHO8j94NLjeNvdrmqEL3sPJxLfhl7scGiUvSyjgFkYPXZNRmG4ANSIWhr4VrY7aOtkAwLmoQ5r4oKPqBQ8jmfnCebqmKxSI6Eb-Psqiu4_FpV3cGl8UFHoV1wIXRAmvCMtaaTQqDurCTD-jGtElLIP8rmLEpIrqwEi7wmO1NgzbeplXMUhK5E78UC_VbRlRfNMTQlmySRSGCUtivLW36cBC96_WIrLQI9TBWWAE2w1cn9xEDKMCDnz9lyHtDd8DxPxI09apaKE5p458Pef4ScQOAyrlYFkGHGx1Z8n5fCd8SdzshOIGO4epIkOmQzKhkejWZXWsKGtdnOBCuM4qJTY8N4Mq6_Vi6d6uDwEbnNC56AnEaRTk4SviJmaXMuS-97kTMTsAr1qKAjvVyouDk2PySs-am0a5l7j4U77uU8SPN5QfVDnV8fIC6Lp1-WtcMdxqrhioRix41SRSO52qM6cG3S_m9vxpOZZ3z8BB29xGfViGrLtH620w3i05H3K7Fe-xHGSBUmNv6d64mh5Y5epZG8gE31QBxFAYqgODcawXowZAMVSOfZIAAeZcuOEvgWw=w497-h579-no");
    background-size: cover;
    background-repeat: no-repeat;
    min-height: 80vh;
    background-position: center;
  }
</style>