<script setup lang="ts">
import {defineComponent, ref, onMounted} from "vue";

const message = ref('');
const activeFilter = ref(1);
const tasks = ref([

]);

const addTask = () => {
  console.log('addTask()')
  tasks.value.push({
    text: message.value,
    done: false,
  });
  message.value = '';
}

const completedTasks = () => {
  return tasks.value.filter(task => task.done)
};

const unCompletedTasks = () => {
  return tasks.value.filter(task => !task.done)
}

</script>

<template>
  <div class="container">
    <div class="row">
      <div class="col-md-12">
        <div class="card card-white">
          <div class="card-body">
            <form action="#">
              <input v-model="message" type="text" class="form-control add-task" placeholder="Новая задача..." style="margin-bottom: 10px;">
              <input type="submit" class="form-control" @click.prevent="addTask()">
            </form>
            <ul class="nav nav-pills todo-nav">
              <li @click="activeFilter = 1" role="presentation" class="nav-item all-task active"><a href="#" class="nav-link">Все</a></li>
              <li @click="activeFilter = 2" role="presentation" class="nav-item active-task"><a href="#" class="nav-link">Активные</a></li>
              <li @click="activeFilter = 3" role="presentation" class="nav-item completed-task"><a href="#" class="nav-link">Завершенные</a></li>
            </ul>
            <div v-if="activeFilter == 1" class="todo-list">
              <label class="todo-item" v-for="(task, index) in tasks" :key="index" :class="{complete: task.done}">
                <span>
                  <div class="checker">
                    <input v-model="task.done" type="checkbox">
                  </div>
                  <span>{{ task.text }}</span>
                </span>
                <a href="#" class="float-right" @click.prevent="tasks.splice(index, 1)">
                  <svg width="20px" height="20px" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path d="M10 11V17" stroke="#000000" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                    <path d="M14 11V17" stroke="#000000" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                    <path d="M4 7H20" stroke="#000000" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                    <path d="M6 7H12H18V18C18 19.6569 16.6569 21 15 21H9C7.34315 21 6 19.6569 6 18V7Z" stroke="#000000" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                    <path d="M9 5C9 3.89543 9.89543 3 11 3H13C14.1046 3 15 3.89543 15 5V7H9V5Z" stroke="#000000" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                  </svg>
                </a>
              </label>
            </div>
            <div v-else-if="activeFilter == 2" class="todo-list">
              <label class="todo-item" v-for="(task, index) in unCompletedTasks()" :key="index" :class="{complete: task.done}">
                <span>
                  <div class="checker">
                    <input v-model="task.done" type="checkbox">
                  </div>
                  <span>{{ task.text }}</span>
                </span>
                <a href="#" class="float-right" @click.prevent="tasks.splice(index, 1)">
                  <svg width="20px" height="20px" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path d="M10 11V17" stroke="#000000" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                    <path d="M14 11V17" stroke="#000000" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                    <path d="M4 7H20" stroke="#000000" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                    <path d="M6 7H12H18V18C18 19.6569 16.6569 21 15 21H9C7.34315 21 6 19.6569 6 18V7Z" stroke="#000000" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                    <path d="M9 5C9 3.89543 9.89543 3 11 3H13C14.1046 3 15 3.89543 15 5V7H9V5Z" stroke="#000000" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                  </svg>
                </a>
              </label>
            </div>
            <div v-else class="todo-list">
              <label class="todo-item" v-for="(task, index) in completedTasks()" :key="index" :class="{complete: task.done}">
                <span>
                  <div class="checker">
                    <input v-model="task.done" type="checkbox">
                  </div>
                  <span>{{ task.text }}</span>
                </span>
                <a href="#" class="float-right" @click.prevent="tasks.splice(index, 1)">
                  <svg width="20px" height="20px" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path d="M10 11V17" stroke="#000000" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                    <path d="M14 11V17" stroke="#000000" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                    <path d="M4 7H20" stroke="#000000" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                    <path d="M6 7H12H18V18C18 19.6569 16.6569 21 15 21H9C7.34315 21 6 19.6569 6 18V7Z" stroke="#000000" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                    <path d="M9 5C9 3.89543 9.89543 3 11 3H13C14.1046 3 15 3.89543 15 5V7H9V5Z" stroke="#000000" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                  </svg>
                </a>
              </label>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">
body{
  margin-top:20px;
  background: #f8f8f8;
}

.todo-nav {
  margin-top: 10px
}

.todo-list {
  margin: 10px 0
}

.todo-list .todo-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  text-align: left;
  padding: 15px;
  margin: 5px 0;
  border-radius: 0;
  background: #f7f7f7;

  span {
    display: flex;
    align-items: center;
    gap: 5px;
  }
}

.todo-list.only-active .todo-item.complete {
  display: none
}

.todo-list.only-active .todo-item:not(.complete) {
  display: block
}

.todo-list.only-complete .todo-item:not(.complete) {
  display: none
}

.todo-list.only-complete .todo-item.complete {
  display: block
}

.todo-list .todo-item.complete span {
  text-decoration: line-through
}

.remove-todo-item {
  color: #ccc;
  visibility: hidden
}

.remove-todo-item:hover {
  color: #5f5f5f
}

.todo-item:hover .remove-todo-item {
  visibility: visible
}

div.checker {
  width: 18px;
  height: 18px
}

div.checker input,
div.checker span {
  width: 18px;
  height: 18px
}

div.checker span {
  display: -moz-inline-box;
  display: inline-block;
  zoom: 1;
  text-align: center;
  background-position: 0 -260px;
}

div.checker, div.checker input, div.checker span {
  width: 19px;
  height: 19px;
}

div.checker, div.radio, div.uploader {
  position: relative;
}

div.button, div.button *, div.checker, div.checker *, div.radio, div.radio *, div.selector, div.selector *, div.uploader, div.uploader * {
  margin: 0;
  padding: 0;
}

div.button, div.checker, div.radio, div.selector, div.uploader {
  display: -moz-inline-box;
  display: inline-block;
  zoom: 1;
  vertical-align: middle;
}

.card {
  padding: 25px;
  margin-bottom: 20px;
  border: initial;
  background: #fff;
  border-radius: calc(.15rem - 1px);
  box-shadow: 0 1px 15px rgba(0,0,0,0.04), 0 1px 6px rgba(0,0,0,0.04);
}
</style>
