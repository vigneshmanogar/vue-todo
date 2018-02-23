<template>
  <div class="list-item" v-bind:class="{completed: item.completed}">
    <input type="checkbox" v-model="item.completed" />
    <div v-if="edit">
        <input type="text" v-model="inputText" v-on:keyup.13="saveList"><button v-on:click="saveList">save</button>
    </div><div v-else>
        <div class="todo-list-text" v-text="item.text"></div><button v-on:click="editList(item.text)">edit</button>
    </div><button v-on:click="deleteList">delete</button>
  </div>
</template>

<script>
export default {
  name: "ListItem",
  props: ["item"],
  data: function() {
    return {
      edit: false,
      textBeforeSave: ""
    };
  },
  computed: {
    inputText: {
      get: function() {
        var _this = this;
        return _this.item.text;
      },
      set: function(text) {
        var _this = this;
        _this.textBeforeSave = text;
      }
    }
  },
  methods: {
    editList: function(text) {
      var _this = this;
      _this.textBeforeSave = text;
      _this.edit = true;
    },
    saveList: function() {
      var _this = this;
      _this.$parent.$emit("updateList", _this.item.id, _this.textBeforeSave);
      _this.edit = false;
    },
    deleteList: function() {
      var _this = this;
      _this.$parent.$emit("deleteList", _this.item.id);
    }
  }
};
</script>

<style scoped>
.list-item {
  display: inline-block;
  width: 100%;
}

.list-item > div {
  display: inline-block;
  width: calc(100% - 92px);
}

.list-item.completed > div > .todo-list-text {
  text-decoration: line-through;
  color: #AAA;  
}

.list-item > input[type="checkbox"] {
    display: inline-block;
    width: 10px;
    vertical-align: top;
    margin-top: 8px;
}

.list-item > div > input[type=text] {
  font-family: 'Merriweather', serif;
  display: inline-block;
  width: calc(100% - 70px);
  line-height: 30px;
  padding: 0px 8px;
}

.list-item > div > input[type=text]:focus {
  outline: none;
}

.list-item > div > .todo-list-text {
  display: inline-block;
  width: calc(100% - 70px);
  line-height: 30px;
  padding: 0px 8px;
}
</style>
