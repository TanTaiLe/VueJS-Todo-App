<template>
  <div id="app">
    <b-container>
      <b-row class="my-5">
        <b-col cols="5" class="mx-auto">
          <b-card bg-variant="light">

            <h3 class="mb-4">Todo App.</h3>
            <h5 v-if="items.length > 0" class="d-flex justify-content-between align-items-center">
              Hoàn thành: {{doneItems.length}}/{{items.length}}.
              <b-button @click="removeAllContent()" variant="danger">
                Xóa hết
              </b-button>
            </h5>
            <h5 v-else class="d-flex justify-content-between align-items-center">
              Chưa có công việc nào.
            </h5>
            
            <b-list-group class="mt-3">

              <!-- Việc mới sau khi thêm sẽ được hiển thị ở đây -->
              <TodoItem :todoList="items" :todo="item" :doneList="doneItems"/>
              
            </b-list-group>

            <!-- Thêm việc mới ở đây -->
            <TodoAdd :todoList="items" :newTodo="newItem" />
            
          </b-card>
        </b-col>
      </b-row>
      
      Mảng chứa công việc: {{items}}
      <br><br>
      Mảng chứa công việc đã hoàn thành: {{doneItems}}
    </b-container>
  </div>
</template>

<script>
  import TodoItem from './components/Todo-item.vue'
  import TodoAdd from './components/Todo-add.vue'
  import Vue from 'vue'
  import BootstrapVue from "bootstrap-vue"
  import "bootstrap/dist/css/bootstrap.min.css"
  import "bootstrap-vue/dist/bootstrap-vue.css"

  Vue.use(BootstrapVue)

  export default {
    name: 'app',
    components: {
      TodoItem,
      TodoAdd,
    },
    data: function () {
      return {
        items: [],
        doneItems: [],
        newItem: "",
      }
    },
    methods: {
      
      /**
       * Remove all todo
       */
      removeAllContent: function() {
        this.items = [];
        this.doneItems = [];
      },

    }
  }
</script>


<style lang="scss">
  @import './assets/scss/index.scss';
</style>