<template>
  <div class="container">
    <h2>To-do List</h2>

    <form @submit.prevent="onSubmit">
      <div class="d-flex">
        <div class="flex-grow-1 mr-2">
          <input
            class="form-control"
            type="text"
            v-model="todo"
            placeholder="Type new to-do"
          />
        </div>
        <div>
          <button type="submit" class="btn btn-primary">
            Add
          </button>
        </div>
      </div>
      <div v-if="hasError">This field cannot be empty</div>
    </form>

    <div v-for="todo in todos" :key="todo.id" class="card mt-2">
      <div class="card-body p-2">
        {{ todo.subject }}
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";

export default {
  setup() {
    const toggle = ref(false);
    const todo = ref("");
    const todos = ref([]);
    const hasError = ref(false);

    const onSubmit = () => {
      if (todo.value === "") {
        hasError.value = true;
      } else {
        todos.value.push({
          id: Date.now(),
          subject: todo.value,
        });
      }
    };

    const onToggle = () => {
      toggle.value = !toggle.value;
    };

    return {
      todo,
      todos,
      onSubmit,
      toggle,
      onToggle,
      hasError,
    };
  },
};
</script>

<style>
.todo {
  color: blueviolet;
}
</style>
