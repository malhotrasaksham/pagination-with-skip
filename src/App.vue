<template>
  <div id="app">
    <div :key="item" v-for="item in currentSet">{{item}}</div>
    <span v-if="currentPage >= pageSize" @click="currentPage -=(pageSize - 1)">[[</span>
    <template v-for="pageNumber in pageCount">
      <span
        @click="UpdatePage(pageNumber)"
        class="pageNumber"
        :key="pageNumber"
        v-if="pageNumber > currentPage-(pageSize - 1) && pageNumber < currentPage+(pageSize-1)"
        :class="{active: currentPage === pageNumber}"
      >{{pageNumber}}</span>
    </template>
    <span v-if="currentPage < pageCount - 1" @click="currentPage +=(pageSize - 1)">]]</span>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      items: [
        "1",
        "2",
        "3",
        "4",
        "5",
        "6",
        "7",
        "8",
        "9",
        "10",
        "11",
        "12",
        "13",
        "14",
        "15",
        "16",
        "17",
        "18",
        "19",
        "20",
        "21",
        "22",
        "23",
        "24",
        "25",
        "26",
        "27",
        "28",
        "29",
        "30",
        "31"
      ],
      pageSize: 3,
      currentPage: 1,
      currentSet: undefined
    };
  },
  computed: {
    pageCount() {
      return Math.ceil(this.items.length / this.pageSize);
    }
  },
  mounted() {
    this.PopulateGrid();
  },
  methods: {
    PopulateGrid() {
      this.currentSet = this.items.slice(
        (this.currentPage - 1) * this.pageSize,
        this.currentPage * this.pageSize
      );
    },
    UpdatePage(pageNumber) {
      this.currentPage = pageNumber;
      this.PopulateGrid();
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
<style scoped>
.pageNumber {
  padding: 5px;
  display: inline-block;
  cursor: pointer;
}
.pageNumber.active {
  font-weight: bold;
}
</style>
