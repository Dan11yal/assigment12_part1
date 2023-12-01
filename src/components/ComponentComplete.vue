<template>
    <div class="oo">
      <h4>Completed Tasks</h4>
      <div v-for="(list, index) in completedLists" :key="index">
        <div >{{ list.title }}</div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      completedLists: {
        type: Array,
        required: true,
      },
    },
  };
  </script>
  
  <style>
   .oo{
    color:white;
   }
  </style>