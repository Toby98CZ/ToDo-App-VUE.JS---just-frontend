<template>
  <div class="card todo-item shadow" @click="passDataFromTodo(todo)">
    <div class="card-body pt-4">
      <h6 class="card-title font-weight-bold d-inline-block">{{ todo.title }}</h6>

      <i class="fa fa-times delete-todo" @click="deleteTodo(todo.id)"></i>

      <hr />
      <p class="card-text">{{ todo.detail }}</p>
      <p class="date">Created {{ todo.date }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "todo",
  props: {
    /*title: {
      type: String,
      required: true
    },
    details: {
      type: String,
      required: true
    },
    date: {
      type: String,
      required: true
    },*/
    index: {
      type: Number,
      required: true
    },
    todo: {
      type: Object,
      required: true
    }
  },
  methods: {
    deleteTodo(id) {
      //console.log(index);
      //this.isDeleted = true;
      this.$emit("delete-todo", id);
    },
    passDataFromTodo(todo) {
      //console.log(todo);
      this.$emit("edit-data", todo);
    }
  },
  mounted() {
    document
      .querySelector(".delete-todo")
      .addEventListener("click", function(e) {
        e.stopPropagation();
        e.preventDefault();
      });
  }
};
</script>

<style></style>
