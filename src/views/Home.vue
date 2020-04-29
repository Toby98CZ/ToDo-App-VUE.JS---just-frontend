<template>
  <div class="home container" id="main">
    <modal modalType="add" @add-todo="addTodo"></modal>

    <modal
      modalType="edit"
      @edit-todo="editTodo"
      :todoProp="currentlyEditedTodo"
      :index="editedIndex"
      @delete-todo="deleteTodo"
    ></modal>
    <!--<img alt="Vue logo" src="../assets/logo.png" class="logo" />-->
    <div class="row mainblock">
      <HelloWorld msg="To-Dos" class="title" />

      <todoInput class="titleBtn"></todoInput>
    </div>
    <SearchComponent class="search" @load-search="searchTodo"></SearchComponent>
    <todos
      :todos="todosList"
      @delete-todo="deleteTodo"
      :search="search"
      @edit-data="passedEditData"
    ></todos>
  </div>
</template>
<script>
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";
import todoInput from "@/components/todoInput.vue";
import SearchComponent from "@/components/SearchComponent.vue";
import modal from "@/components/modal.vue";
import todos from "@/components/todos.vue";

export default {
  name: "Home",
  components: {
    HelloWorld,
    todoInput,
    SearchComponent,
    modal,
    todos
  },
  methods: {
    addTodo(attrs) {
      var dateF = new Date().toLocaleString().slice(0, 11);
      /* var currentDateWithFormat = new Date()
        .toJSON()
        .slice(0, 10)
        .replace(/-/g, ".");
*/
      console.log(attrs);
      var newTodo = {
        id: Math.floor(Math.random() * (9999999 - 1000000 + 1)),
        title: attrs.title,
        detail: attrs.details,
        date: dateF
      };
      this.todosList.push(newTodo);
    },
    editTodo(edited) {
      this.todosList[edited.index].title = edited.title;
      this.todosList[edited.index].detail = edited.detail;

      //console.log(this.todosList[edited.index].title);
      console.log(edited.index);
    },
    passedEditData(todo) {
      this.editedIndex = this.todosList.findIndex(x => x.id === todo.id);
      this.currentlyEditedTodo = todo;
      this.$emit("edit-helper");
    },
    deleteTodo(id) {
      var delIndex = this.todosList.findIndex(x => x.id === id);
      this.todosList.splice(delIndex, 1);
    },
    searchTodo(word) {
      this.search = word;
    }
  },
  data() {
    return {
      todosList: [
        {
          id: 5287,
          title: "Task #01",
          detail:
            "Some quick example text to write on the todo detail and make up the bulk of the card's content.",
          date: "17.3.2019"
        },
        {
          id: 4568,
          title: "Todo title",
          detail:
            "Some quick example text to write on the todo detail and make up the bulk of the card's content.",
          date: "12.3.2020"
        }
      ],
      search: "",
      currentlyEditedTodo: {},
      editedIndex: null
    };
  }
};
</script>

<style>
.logo {
  max-width: 100px;
  padding: 20px;
}
.title {
  display: flex;
  align-items: center;
}
.titleBtn {
  text-align: right;
}
.mainblock {
  padding-top: 35px;
  position: sticky;
  top: 0;
  z-index: 99;
  background: #f3f3f3;
  padding-bottom: 10px;
}
.home {
  max-width: 500px;
}
.search input {
  margin-top: 20px;
  background: #e8e8e8;
  border: 0px;
}
</style>
