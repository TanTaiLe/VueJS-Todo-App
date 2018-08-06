<template>
  <div class="">
    <b-form inline class="mt-3" @submit.prevent>
      <label class="sr-only" for="newTodo-input"></label>
      <b-input-group class="w-100">
        <b-form-input v-model="newTodo" class="" id="newTodo-input" placeholder="Làm, học, ...."></b-form-input>

        <b-button @keyup.enter="addNewContent" @click="addNewContent" variant="primary" slot="append">Thêm</b-button>
      </b-input-group>
    </b-form>
  </div>
</template>

<script>
  export default {
    name: 'TodoAdd',
    props: {
      todoList: Array,
      newTodo: String,
    },
    methods: {
      /**
       * Add new todo
       */
      addNewContent: function() {
        if(this.newTodo != "") {
          this.todoList.push({id: this.todoList.length+1, content: this.newTodo, completed: false, edit: false});
          this.newTodo = "";
        } else {
          alert("Không được để trống công việc!");
        }
      },

    }
  }
</script>