
<template>
  <div class="px-3 py-10 md:px-10">
    <div class="w-full sm:w-1/2 lg:w-1/3 mx-auto">
      <TodoSpinner v-if="loading"></TodoSpinner>
      <template v-else>
        <TodoFormAdd></TodoFormAdd>

        <TodoItems v-if="$store.state.todos.length"></TodoItems>
        <TodoEmpty v-else></TodoEmpty>
      </template>
    </div>
  </div>
</template>

<script>
import TodoSpinner from './components/TodoSpinner.vue';
import TodoFormAdd from './components/TodoFormAdd.vue';
import TodoItems from './components/TodoItems.vue';
import TodoEmpty from './components/TodoEmpty.vue';
import axios from 'axios';

export default {
  components: {
    TodoSpinner,
    TodoFormAdd,
    TodoItems,
    TodoEmpty
  },
  data() {
    return {
      loading: false
    }
  },
  created() {
    this.loading = true;

    this.$store.dispatch('getTodos')
      .finally(() => {
        this.loading = false;
      })
  }
}
</script>