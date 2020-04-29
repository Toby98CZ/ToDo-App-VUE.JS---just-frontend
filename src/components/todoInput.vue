<template>
  <div class="col">
    <button class="btn btn-warning add-todo" data-toggle="modal" data-target="#addTodoModal">
      <i class="fa fa-plus"></i>
    </button>
  </div>
</template>

<script>
export default {
  name: "todoInput"
};
</script>

<style>
.add-todo {
  border-radius: 100%;
  width: 45px;
  height: 45px;
}

.add-todo:hover {
  color: #ffc107;
  background: #212529;
  border: 1px solid #212529;
}
</style>
