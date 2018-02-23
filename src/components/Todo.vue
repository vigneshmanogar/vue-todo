<template>
  <div class="todo-container">
    <section class="add-todo">
      <h4>Add Item</h4>
      <input v-model="addTodo" placeholder="Add item" v-on:keyup.13="addItem"/><button v-on:click="addItem">Add</button>
    </section>    
    <section>
        <h4>To Do</h4>
        <div v-if="pendingItems.length != 0" >
          <list-item v-for="item in pendingItems" 
          v-bind:key="item.id" 
          v-bind:item="item"></list-item>
        </div>
        <div v-else>
          <span class="info-text">No pending items</span>
        </div>
    </section>
    <section>
        <h4>Completed</h4>
        <div v-if="completedItems.length !== 0">
          <list-item v-for="item in completedItems" 
          v-bind:key="item.id" 
          v-bind:item="item"></list-item>
        </div>        
        <div v-else>
          <span class="info-text">No completed items</span>
        </div>
    </section>
  </div>
</template>

<script>
import ListItem from '@/components/ListItem.vue'

export default {
  name: "Todo",
  data() {
    return {
      items: [],
      addTodo: ""
    }
  },
  computed: {
    pendingItems: function() {
      var _this = this;
      var pendingItems = _this.items.filter(function(item) {
          return (item.completed === false);
      });

      return pendingItems;
    },
    completedItems: function() {
      var _this = this;
      var completedItems = _this.items.filter(function(item) {
          return (item.completed === true);
      });

      return completedItems;
    }
  },
  created: function() {
    var _this = this;
    _this.$on('updateList', _this.updateItem);
    _this.$on('deleteList', _this.deleteItem);
  },
  methods: {
    addItem: function() {
      var _this = this;
      var item = {
          id: Math.floor(Math.random()*16).toString(16).toUpperCase(),
          text: _this.addTodo,
          completed: false
      }

      _this.addTodo = "";
      _this.items.unshift(item);
    },
    updateItem: function(id, updatedText) {
      var _this = this;
      var list = _this.items.filter(function(item) {
          return (item.id === id);
      });

      list[0].text = updatedText;
    },
    deleteItem: function(id) {
      var _this = this;
      var index = _this.items.map(function(item) { return item.id; }).indexOf(id);
      _this.items.splice(index, 1);
    }
  },
  components: {
    ListItem
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.todo-container {
  position: relative;
  margin: 0 auto;
  max-width: 550px;
  margin-top: 60px;
  padding: 25px 40px;
}

.todo-container section {
  display: inline-block;
  width: 100%;
  margin-bottom: 25px;
}

.todo-container section h4 {
  display: inline-block;
  width: 100%;
  font-weight: 400;
  line-height: 36px;
  border-bottom: 2px solid #333;

  text-transform: uppercase;
}

.todo-container section.add-todo input {
  font-family: 'Merriweather', serif;
  display: inline-block;
  width: calc(100% - 70px);
  line-height: 30px;
  padding: 0px 8px;
}

.todo-container section.add-todo input:focus {
  outline: none;
}

span.info-text {
  size: 12px;
  color: #AAA;
}

</style>
