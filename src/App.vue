<template>
  <div id="app">
    <div id="to-do-list">
      <h1>To Do List</h1>
      <button @click="showModal = true">Add New To-Do</button>
      <ul id="tab-titles" class="clearfix">
        <li id="all" @click="currentTab = 1" :class="{active : currentTab == 1}">Total ({{todos.length}})</li>
        <li id="unfinished" @click="currentTab = 2" :class="{active : currentTab == 2}">Pending ({{todos.filter(todo => todo.isDone == false).length}})</li>
        <li id="done" @click="currentTab = 3" :class="{active : currentTab == 3}">Success ({{todos.filter(todo => todo.isDone).length}})</li>
      </ul>
      <div id="tab-contents">
        <div id="all-content" 
             v-show="currentTab == 1"
             v-for="(todo, index1) in todos" :key="'total' + index1"
             :class="{done : todo.isDone}">
              <input type="checkbox" v-model="todo.isDone">
              <p onselectstart="return false" @click="todo.isDone = !todo.isDone">{{ todo.content }}</p>
              <button @click="todos.splice(index1, 1)">Delete</button>
        </div>
        <div id="unfinished-content" 
             v-show="currentTab == 2"
             v-for="(todo, index2) in todos.filter(todo => todo.isDone == false)" :key="'pending' +index2"> 
             {{ todo.content }} 
        </div>
        <div id="done-content" 
             v-show="currentTab == 3"
             v-for="(todo, index3) in todos.filter(todo => todo.isDone)" :key="'done' +index3"> 
             {{ todo.content }} 
        </div>
      </div>
    </div>
    <Modal :todos="todos" @changevalue="todos = $event" v-show="showModal" :showModal="showModal" @changeshow="showModal = $event"></Modal>
  </div>
</template>

<script>
import Modal from "./components/Modal.vue";
export default {
  name: 'App',
  data() {
    return {
      currentTab: 1,
      todos: [{
                content: 'Learn web development',
                isDone: false
              },
              {
                content: 'Get a Fresher job',
                isDone: false
              },
              {
                content: 'Become a senior web developer',
                isDone: false
              },
              {
                content: 'Learn mobile development',
                isDone: false
              },
              {
                content: 'Hack NASA',
                isDone: true
              }
             ],
      showModal: false
    }
  },
  components: {
    Modal
  }
}
</script>

<style lang="scss">
* {
  margin: 0px;
  padding: 0px;
  box-sizing: border-box;
}
.clearfix::after {
  content: ' ';
  clear: both;
  display: table;
}
.done {
  text-decoration: line-through;
}
.active {
  background-color: white;
  color: #50555A !important;
}
#app {
  position: relative;
  display: grid;
  place-items: center;
  height: 100vh;
  #to-do-list {
    width: 500px;
    height: 370px;
    background-color: #46A1DE;
    padding: 10px 10px;
    > h1 {
      text-transform: uppercase;
      text-align: center;
      margin-bottom: 10px;
      color: rgb(192, 71, 71);
      font-size: 30px;
    }
    > button {
      width: 110px;
      height: 30px;
      margin-left: calc(50% - 55px);
      background-color: rgb(16, 180, 10);
      border: none;
      cursor: pointer;
      border-radius: 10px;
      margin-bottom: 20px;
      color: white;
      &:hover {
        background-color: #2ECC71;
        color: #50555A;
      }
    }
    > ul {
      height: 30px;
      line-height: 30px;
      > li {
        float: left;
        list-style: none;
        width: calc(100%/3);
        text-align: center;
        border-radius: 5px 5px 0px 0px;
        color: white;
        &:hover {
          background-color: white;
          color: #50555A;
        }
      }
    }
    > #tab-contents {
        background-color: white;
        height: 224px;
        border-radius: 0px 0px 5px 5px;
        padding: 10px;
        overflow: auto;
        color: #50555A;
      > div {
        line-height: 30px;
      }
      > #all-content {
        position: relative;
        display: flex;
        align-items: center;
        > input {
          margin-right: 5px;
        }
        > button {
          position: absolute;
          right: 10px;
          color: #50555A;
        }
      }
    }
  }
}
</style>
