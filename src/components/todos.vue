<template>
  <div class="todoItems">
    <div v-show="todos.length == 0">
      <p class="noTodosLeft">No todos left :-(</p>
    </div>
    <todo
      v-for="(todo, index) in filteredList.slice().reverse()"
      :key="todo.id"
      :todo="todo"
      :index="index"
      @delete-todo="deleteTodo"
      @edit-data="passDataFromTodo"
      data-toggle="modal"
      data-target="#editTodoModal"
    ></todo>

    <p class="hint end">End of todos /></p>
  </div>
</template>
<script>
import todo from "@/components/todo.vue";
export default {
  name: "todos",
  props: {
    todos: {
      type: Array,
      required: true
    },
    search: {
      type: String,
      required: false
    }
  },
  data() {
    return {
      isDeleted: false,
      eindex: null
    };
  },
  methods: {
    deleteTodo(id) {
      console.log(id);
      //this.isDeleted = true;
      this.$emit("delete-todo", id);
    },
    passDataFromTodo(todo) {
      //console.log(todo);
      this.$emit("edit-data", todo);
    }
  },
  computed: {
    filteredList() {
      return this.todos.filter(todo => {
        return todo.title.toLowerCase().includes(this.search.toLowerCase());
      });
    }
  },
  components: {
    todo
  }
};
</script>

<style>
.noTodosLeft {
  color: #d5d5d5;
  font-size: 25px;
}
.end {
  text-align: center;
  padding-top: 15px;
  justify-content: center;
}
.date {
  font-size: 14px;
  color: grey;
  display: flex;
  padding: 0;
  margin: 0;
}
.delete-todo {
  right: 0;
  position: absolute;
  padding-right: 20px;
  color: grey;
}
.delete-todo:hover {
  color: red;
  cursor: pointer;
}
.todo-item {
  width: 100% !important;
  text-align: left;
  border: 0px;
  border-radius: 10px;
  margin-top: 25px;
}
.todo-item:hover {
  box-shadow: 0 0.5rem 1rem rgba(0, 0, 0, 0.15) !important;
  cursor: pointer;
  background: rgb(255, 245, 227);
}
.todoItems {
  margin-top: 10px;
  width: 100%;
}
.shadow {
  box-shadow: 0 0.5rem 1rem rgba(0, 0, 0, 0.08) !important;
}

div.removedItem {
  animation: removedItem-animation 0.8s cubic-bezier(0.65, -0.02, 0.72, 0.29);
}

@keyframes removedItem-animation {
  0% {
    opacity: 1;
    transform: translateX(0);
  }

  30% {
    opacity: 1;
    transform: translateX(50px);
  }

  80% {
    opacity: 1;
    transform: translateX(-800px);
  }

  100% {
    opacity: 0;
    transform: translateX(-800px);
  }
}
</style>
