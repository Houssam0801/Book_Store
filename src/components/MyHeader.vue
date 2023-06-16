<template>
  <div class="header">
    <nav class="navbar p-0">
      <div class="container-fluid">
        <img
          src="../assets/16596F40-8ADC-404C-9B51-1AB8C2538956_4_5005_c.jpeg"
        />
        <div class="d-flex">
          <input
            class="form-control me-1"
            type="search"
            placeholder="Search title"
            v-model="filterText"
          />
          <button class="btn btn-outline-warning" @click="inputdata">
            <i class="bi bi-search-heart"></i>
          </button>
        </div>
      </div>
    </nav>
  </div>
</template>

<script>
export default {
  data() {
    return { filterText: "" };
  },

  methods: {
    inputdata() {
      this.$emit("handledata", this.filterText);
      this.filterText = "";
    },
  },

  name: "MyHeader",
};
</script>

<style scoped>
nav {
  background-color: #141414;
}
a {
  color: aliceblue;
}
a:hover {
  color: #eae430e0;
}
img {
  width: 150px;
}
#search {
  height: 35px;
}
</style>
