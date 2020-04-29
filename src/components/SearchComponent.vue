<template>
  <div>
    <div class="row searchDiv">
      <input
        class="form-control"
        type="text"
        placeholder="Search..."
        v-model="search"
        @keyup="
          {
            loadSearchValue(search);
          }
        "
      />
    </div>
    <div class="row">
      <div class="col">
        <span class="hint">Click on note to edit</span>
      </div>
      <div class="dropdown col">
        <p
          class="dropdown-toggle"
          id="dropdownMenuButton"
          data-toggle="dropdown"
          aria-haspopup="true"
          aria-expanded="false"
        >Categories</p>
        <div class="dropdown-menu" aria-labelledby="dropdownMenuButton">
          <a class="dropdown-item" href="#">Action</a>
          <a class="dropdown-item" href="#">Another action</a>
          <a class="dropdown-item" href="#">Something else here</a>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "SearchComponent",
  data() {
    return {
      search: ""
    };
  },
  methods: {
    loadSearchValue(word) {
      //console.log(word);
      this.$emit("load-search", word);
    }
  }
};
</script>

<style>
.hint {
  padding-top: 5px;
  font-size: 12px;
  color: grey;
  display: flex;
}
#dropdownMenuButton {
  font-size: 14px;
  color: grey;
  padding-top: 5px;
}
.dropdown {
  text-align: right;
}
.dropdown p:hover {
  cursor: pointer;
  color: black !important;
}

.searchDiv {
  padding-left: 15px;

  padding-right: 15px;
}
</style>
