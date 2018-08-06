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
            

            <!-- Việc mới sau khi thêm sẽ được hiển thị ở đây -->
            <TodoItems :todoList="items" :todo="item" :doneList="doneItems"/>
              

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
  import TodoItems from './components/Todo-items.vue'
  import TodoAdd from './components/Todo-add.vue'
  import Vue from 'vue'
  import BootstrapVue from "bootstrap-vue"
  import "bootstrap/dist/css/bootstrap.min.css"
  import "bootstrap-vue/dist/bootstrap-vue.css"
  import VueLocalStorage from 'vue-localstorage'

  Vue.use(BootstrapVue)
  Vue.use(VueLocalStorage, {
    name: 'ls',
    bind: true
  })

  export default {
    name: 'app',
    components: {
      TodoItems,
      TodoAdd,
    },
    data() {
      return {
        items: [],
        doneItems: [],
        newItem: "",
      }
    },
    mounted() {
      if(localStorage.getItem('items')) {
        try {
          this.items = JSON.parse(localStorage.getItem('items'));
        } catch(e) {
          localStorage.removeItem('items');
        }
      }

      if(localStorage.getItem('doneItems')) {
        try {
          this.doneItems = JSON.parse(localStorage.getItem('doneItems'));
        } catch(e) {
          localStorage.removeItem('doneItems');
        }
      }
    },
    methods: {
      
      /**
       * Remove all todo
       */
      removeAllContent: function() {
        this.items = [];
        this.doneItems = [];
        let savedItems = JSON.stringify(this.items);
        localStorage.setItem('items', savedItems);
        let savedDoneItems = JSON.stringify(this.doneItems);
        localStorage.setItem('doneItems', savedDoneItems);
      },

    }
  }
</script>


<style lang="scss">
  @import './assets/scss/index.scss';
</style>