<template>
  <div class="">
    <b-list-group class="mt-3">
      <b-list-group-item v-for="(todo, index) in todoList" :key="index" class="d-flex justify-content-between align-todoList-center">

        <div :class="{ done: todo.completed }" class="d-flex justify-content-between align-items-center w-75">
          <b-form-checkbox :id="'chb'+index" name="todo-list" v-model="todo.completed" @change="checkDoneContent(todo)">
            <span class="index">{{index+1}}.</span>
          </b-form-checkbox>
          <p v-show="todo.edit == false" @dblclick="todo.edit = true" class="m-0 w-100" v-b-tooltip.hover title="Click 2 lần để chỉnh sửa">{{todo.content}}</p>
          <b-input v-show="todo.edit == true" @blur.native="todo.edit = false" @keyup.enter.native="todo.edit = false" v-model="todo.content"
            class="w-100" :value="todo.content" :id="'todo'+index+1" />
        </div>


        <b-button @click="removeContent(todo)" variant="danger">
          Xóa
        </b-button>

      </b-list-group-item>
    </b-list-group>
  </div>
</template>

<script>
  export default {
    name: 'TodoItems',
    props: {
      todo: Object,
      todoList: Array,
      doneList: Array,
    },
    methods: {
      
      /**
       * Remove todo from work's lists
       */
      removeContent: function(e) {
        this.todoList.splice(this.todoList.indexOf(e), 1);

        if(this.doneList.length > 0 && e.completed == true)
          this.doneList.splice(this.doneList.indexOf(e), 1);

          
        let parsed = JSON.stringify(this.todoList);
        localStorage.setItem('items', parsed);
      },

      /**
       * Check done todo
       */
      checkDoneContent: function(e) {
        if(e.completed == false)
          this.doneList.push({id: e.id, content: e.content});
        else
          this.doneList.splice(this.doneList.indexOf(e), 1);
      }
    }
  }
</script>