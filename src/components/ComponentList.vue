<template>
    <div class="tasks">
      <ul>
        <li v-for="(list, index) in lists" :key="index">
          <div :class="{ completed: list.completed }">{{ list.title }}</div>
          <div class="s">
            <label for="select">completed</label>
            <input @click="update(index)" type="checkbox" value="completed" id="select" :checked="list.completed">
            <button @click="dropPost(index)">Delete</button>
          </div>
        </li>
      </ul>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      lists: {
        type: Array,
        required: true,
      },
    },
    methods: {
      update(index) {
        this.$emit('update-task', index);
      },
      dropPost(index) {
        this.$emit('drop-post', index);
      },
    },
  };
  </script>
  
  <style>
  .completed {
    text-decoration: line-through;
  }
  .tasks li{
    list-style: none;
    display: flex;
    justify-content: space-between;
    margin: 15px 0;
    font-size: 20px;
    background-color: rgb(100,149,237,0.2);
    color:bisque;
  }
  .tasks button{
    border: none;
    outline: none;
    background-color: crimson;
    padding: 10px;
    border-radius: 10px;
  }
  .s input{

  }
  </style>