<template>
  <MainLayout>
    <div class="form__group field">
      <input
        v-model="inputText"
        @keydown.enter="handleNewTodo"
        type="input"
        class="form__field"
        placeholder="Todo"
        name="Todo"
        id="name"
        required
      />
      <label for="name" class="form__label">Todo</label>
    </div>
    <TodosComponent :text="inputText" />
  </MainLayout>
</template>

<script>
import MainLayout from './layouts/MainLayout/index.vue';
import TodosComponent from './components/TodoList';

export default {
  name: 'App',
  data() {
    return {
      inputText: '',
    };
  },
  methods: {
    handleNewTodo() {
      console.log(this.inputText);
    },
  },

  components: { MainLayout, TodosComponent },
};
</script>

<style lang="scss" src="./assets/style/index.scss"></style>
