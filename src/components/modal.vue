<template>
  <div class="customizableModal">
    <!-- Modal -->
    <div
      class="modal fade"
      id="addTodoModal"
      tabindex="-1"
      role="dialog"
      aria-labelledby="addTodoModalLabel"
      aria-hidden="true"
      v-if="modalType == 'add'"
    >
      <div class="modal-dialog" role="document">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="addTodoModalLabel">Add your To-Do</h5>
            <button type="button" class="close" data-dismiss="modal" aria-label="Close">
              <span aria-hidden="true">&times;</span>
            </button>
          </div>
          <div class="modal-body">
            <div class="form-group">
              <label for="todoTitle">Title</label>
              <input
                type="text"
                class="form-control"
                id="todoTitle"
                placeholder="Make the dishes..."
                v-model="title"
              />
            </div>
            <div class="form-group">
              <label for="todoDetail">Details</label>
              <textarea
                class="form-control"
                id="todoDetail"
                rows="3"
                placeholder="..."
                v-model="details"
              ></textarea>
            </div>
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-secondary" data-dismiss="modal" @click="clearTodo">
              <i class="fa fa-trash" aria-hidden="true"></i>
            </button>
            <button
              type="button"
              id="addTodoButton"
              class="btn btn-warning font-weight-bold"
              @click="addTodo"
              data-dismiss="modal"
              v-show="!isDisabled"
            >
              Add Todo
              <i class="fa fa-plus" aria-hidden="true"></i>
            </button>
            <!-- NOT WORKING BUTTON TO SHOW DISABLED WHEN NO TITLE -->
            <button
              type="button"
              id="addTodoButton"
              class="btn btn-warning font-weight-bold"
              :class="{ disabled: isDisabled }"
              v-show="isDisabled"
            >
              Add Todo
              <i class="fa fa-plus" aria-hidden="true"></i>
            </button>
          </div>
        </div>
      </div>
    </div>

    <div
      class="modal fade"
      id="editTodoModal"
      tabindex="-1"
      role="dialog"
      aria-labelledby="editTodoModalLabel"
      aria-hidden="true"
      v-observe-visibility="loadEditData"
      v-if="modalType == 'edit'"
    >
      <div class="modal-dialog" role="document">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="editTodoModalLabel">Edit your To-Do</h5>
            <button type="button" class="close" data-dismiss="modal" aria-label="Close">
              <span aria-hidden="true">&times;</span>
            </button>
          </div>
          <div class="modal-body">
            <div class="form-group">
              <label for="todoTitle">Title</label>
              <input
                type="text"
                class="form-control"
                id="todoTitle"
                placeholder="Make the dishes..."
                v-model="etitle"
              />
            </div>
            <div class="form-group">
              <label for="todoDetail">Details</label>
              <textarea
                class="form-control"
                id="todoDetail"
                rows="3"
                placeholder="..."
                v-model="edetails"
              ></textarea>
            </div>
          </div>
          <div class="modal-footer">
            <!--DELETE BUTTON-->
            <button
              type="button"
              class="btn btn-secondary"
              data-dismiss="modal"
              @click="deleteTodo(eindex)"
            >
              <i class="fa fa-trash" aria-hidden="true"></i>
            </button>
            <!--EDIT BUTTON-->
            <button
              type="button"
              id="editTodoButton"
              class="btn btn-warning font-weight-bold"
              @click="editTodo(eindex)"
              data-dismiss="modal"
              v-show="!isDisabled"
            >
              Edit Todo
              <i class="fa fa-plus" aria-hidden="true"></i>
            </button>
            <!-- NOT WORKING BUTTON TO SHOW DISABLED WHEN NO TITLE -->
            <button
              type="button"
              id="editTodoButton"
              class="btn btn-warning font-weight-bold"
              :class="{ disabled: isDisabled }"
              v-show="isDisabled"
            >
              Edit Todo
              <i class="fa fa-plus" aria-hidden="true"></i>
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "modal",
  props: {
    modalType: {
      type: String,
      required: true
    },
    index: {
      type: Number,
      required: false
    },
    todoProp: {
      type: Object,
      required: false
    }
  },
  computed: {
    isDisabled() {
      if (this.title == "" && this.etitle == "") {
        return true;
      } else {
        return false;
      }
    }
  },
  data() {
    return {
      title: "",
      details: "",
      etitle: "",
      edetails: "",
      eindex: null
    };
  },
  methods: {
    addTodo(title, details) {
      title = this.title;
      details = this.details;
      /*console.log(title);
      console.log(details);
*/
      this.$emit("add-todo", { title, details });
      this.clearTodo();
    },
    clearTodo() {
      this.title = "";
      this.details = "";
      this.etitle = "";
      this.edetails = "";
    },
    editTodo(index, detail, title) {
      detail = this.edetails;
      title = this.etitle;
      this.$emit("edit-todo", { index, detail, title });
      this.clearTodo();
    },
    loadEditData() {
      this.eindex = this.index;
      this.etitle = this.todoProp.title;
      this.edetails = this.todoProp.detail;
    },
    deleteTodo(index) {
      this.$emit("delete-todo", index);
    }
  }
};
</script>

<style>
.modal-body {
  text-align: left;
  font-weight: bold;
}

.form-control {
  background: #e8e8e8;
  border: 0px;
}
</style>
