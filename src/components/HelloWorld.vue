<template>
  <div class="col-md-12">
    <div class="col-md-6 col-md-offset-3 wow fadeInDown" align="center" data-wow-delay="0.3s">
      <div class="col-md-12 card-header">
        <input v-model="input" type="text" placeholder="Add Task and Press ENTER" />
        <button @click="addTask" class="btn btn-primary" id="btn-add">
          Add
        </button>
      </div>
    </div>
    <div class="col-md-6 col-md-offset-3">
      <div class="col-md-12 card list-div wow fadeInUp" align="left" data-wow-delay="0.6s">
        <ul v-if="tasks.length == 0" id="list" class="wow fadeIn" data-wow-delay="0.8s">
          <li>
            <button class="mark-done" id="0">Done</button>Add a task and press
            enter.
          </li>
          <li class="strike">
            <button class="mark-done completed" id="1">Done</button>Default
            items will be removed.
          </li>
        </ul>
        <p v-if="tasks.length == 0" class="no-ul-message" id="message">
          <span class="fa fa-hand-peace-o"></span>&nbsp;&nbsp;Wohoo! All tasks
          are cleared!!
        </p>

        <ul v-else id="list" class="wow fadeIn" data-wow-delay="0.8s" style="
            visibility: visible;
            animation-delay: 0.8s;
            animation-name: fadeIn;
          ">
          <li v-for="(item, index) in tasks" :class="{ strike: item.done }" class="wow flash"
            style="visibility: visible; animation-name: flash">
            <button class="mark-done" :class="{ completed: true }" :id="index" @click="completeTask(index)">
              Done</button>{{ item.message }}
          </li>
        </ul>
      </div>
      <div class="col-md-12 card-footer hvr-sweep-to-right">
        <div class="col-md-6" align="left">
          <button @click="deleteAllDoneTasks" class="btn btn-clear-task" id="btn-clear-task">
            <span class="fa fa-refresh"></span>&nbsp;&nbsp;Clear Completed Tasks
          </button>
        </div>
        <div class="col-md-6 markdone-div" align="right">
          <button class="btn btn-clear-task" id="btn-mark-done">
            <span class="fa fa-check-square"></span>&nbsp;&nbsp;<span id="mark-all">Mark All as Done</span>
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, reactive, onMounted } from "vue";

let tasks = reactive([]);
let input = ref("");

const addTask = () => {
  tasks.push({ message: input.value, done: false });
  input.value = "";
  console.log(tasks);
};

const completeTask = (index) => {
  tasks.at(index).done = !tasks.at(index).done;
}

const deleteAllDoneTasks = () => {
  const filteredtasks = tasks.filter((task) => task.done != true);
  tasks.splice(0, tasks.length, ...reactive(filteredtasks))
}


</script>

<style scoped>
a:hover {
  text-decoration: none;
}

.card-header {
  display: flex;
  background: rgba(0, 0, 0, 0.3);
  padding: 30px;
}

.card {
  background: #fff;
  background: #fff;
  padding: 0;
  margin: 0;
  border-radius: 0px;
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.19), 0 6px 20px rgba(0, 0, 0, 0.23);
  margin-top: 20px;
  padding-top: 7px;
  height: 100%;
}

.card-footer {
  background: #e8f4ff;
  width: 100%;
}

.hvr-sweep-to-right:active,
.hvr-sweep-to-right:focus,
.hvr-sweep-to-right:hover {
  color: #fff;
  outline: 0;
}

input[type="text"] {
  padding: 10px 10px;
  width: 80%;
  border: none;
  border-radius: 0;
  font-weight: 100;
  font-size: 15px;
  background: transparent;
  border-bottom: 1px solid rgba(255, 255, 255, 0.5);
  outline: 0;
  transition: all 0.5s;
  margin-right: 10px;
  color: #fff;
}

input[type="text"]:focus {
  border-color: #fff;
}

::-webkit-input-placeholder {
  color: rgba(255, 255, 255, 0.7);
}

.btn-primary,
.btn-primary:focus {
  padding: 7px 20px;
  border: none;
  font-size: 13px;
  text-transform: uppercase;
  cursor: pointer;
  margin-bottom: -5px;
  outline: 0;
  border-radius: 1px;
  background: #fff;
  transition: all 0.5s;
  color: #6f1010;
}

.btn-primary:hover {
  background: #de5454;
  box-shadow: 2px 2px 5px rgba(0, 0, 0, 0.2);
  color: #fff;
}

hr {
  border: 1px solid #ddd;
}

input[type="checkbox"] {
  margin-right: 10px;
}

ul li {
  margin-left: -20px;
  padding: 16px 15px 16px 0px;
  list-style-type: none;
  color: #555;
  font-size: 15px;
  transition: all 0.5s;
}

.strike {
  text-decoration: line-through;
  color: #888;
  transition: all 0.5s;
}

.strike bottom {
  text-decoration: line-through;
  color: #888;
  transition: all 0.5s;
}

.strike button {
  background: #f34d71;
  color: #fff;
}

.mark-done {
  margin: 2px 15px 2px 10px;
  line-height: 15px;
  padding-top: 4px;
  font-size: 12px;
  background: #eee;
  color: #999;
  border-radius: 2px;
  border: none;
  cursor: pointer;
  transition: all 0.5s;
  outline: 0;
  text-transform: uppercase;
}

.mark-done:hover {
  background: #f34d71;
  color: #fff;
}

.btn-clear-task,
.btn-clear-task:focus {
  margin: 13px 15px;
  background: transparent;
  text-transform: uppercase;
  font-size: 13px;
  color: #ac2e48;
  transition: all 0.5s;
  outline: 0;
}

.btn-clear-task:hover {
  color: #277094 !important;
}

.hvr-sweep-to-right:active:before,
.hvr-sweep-to-right:focus:before,
.hvr-sweep-to-right:hover:before {
  -webkit-transform: scaleX(1);
  transform: scaleX(1);
}

.hvr-sweep-to-right:before {
  background: #c7e3ff;
}

.hvr-sweep-to-right:before {
  content: "";
  position: absolute;
  z-index: -1;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: #2098d1;
  -webkit-transform: scaleX(0);
  transform: scaleX(0);
  -webkit-transform-origin: 0 50%;
  transform-origin: 0 50%;
  -webkit-transition-property: transform;
  transition-property: transform;
  -webkit-transition-duration: 0.3s;
  transition-duration: 0.3s;
  -webkit-transition-timing-function: ease-out;
  transition-timing-function: ease-out;
}

:after,
:before {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}

.hvr-sweep-to-right:active,
.hvr-sweep-to-right:focus,
.hvr-sweep-to-right:hover {
  color: #fff;
}

.no-ul-message {
  color: #666;
  padding: 14px 25px 17px 25px;
  padding-bottom: 13px;
  font-family: Roboto;
  font-size: 15px;
  margin: 0;
}

.by-kn {
  position: absolute;
  bottom: 20px;
  right: 20px;
  color: rgba(255, 255, 255, 0.7);
  font-size: 16px;
  position: fixed;
}

.by-kn a {
  color: #fff;
  border-bottom: 1px dotted #fff;
  transition: all 0.5s;
}

.by-kn:hover a {
  color: #baddff;
  border-color: #baddff;
}

/* MAKING IT RESPONSIVE */
@media (max-width: 768px) {
  body {
    padding-top: 15%;
  }

  .card-header {
    padding: 10px;
    padding-bottom: 15px;
  }

  input[type="text"] {
    width: 70%;
  }

  .mark-done {
    padding-bottom: 6px;
    margin: 2px 15px 2px -2px;
  }

  .markdone-div {
    display: none;
    border: 1px solid forestgreen;
  }
}
</style>
