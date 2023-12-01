<template>
  <div class="main">
    <h1>Task Management App</h1>
    <div class="formApp">
    <form @submit.prevent>
      <label>Add Task</label>
      <input type="text" @input="title = $event.target.value" v-bind:value="title" placeholder="Write any data">
      <button @click="addItem">ADD</button>
    </form>
  </div>
    <component-list :lists="lists" @update-task="updateTask" @drop-post="dropPost"></component-list>
    <component-complete :completed-lists="completedLists"></component-complete>
  </div>
</template>

<script>
import ComponentList from "./components/ComponentList.vue";
import ComponentComplete from "./components/ComponentComplete.vue";

export default {
  components: {
    ComponentList,
    ComponentComplete,
  },
  data() {
    return {
      lists: [
        {
          title: 'Daniyal',
          completed: false
        }
      ],
      completedLists: [],
      title: '',
      completed:false
    };
  },
  methods: {
    addItem() {
      const item = { title: this.title, completed: false };
      if (this.title.trim() !== '') {
        this.lists.push(item);
        this.title = '';
      }
    },
    updateTask(index) {
      const updatedTask = this.lists[index];
      updatedTask.completed = !updatedTask.completed;

      if (updatedTask.completed) {
        this.completedLists.push(updatedTask);
      } else {
        const completedIndex = this.completedLists.findIndex(item => item.title === updatedTask.title);
        if (completedIndex !== -1) {
          this.completedLists.splice(completedIndex, 1);
        }
      }
    },
    dropPost(index) {
      this.lists.splice(index, 1);
    },
  },
};
</script>

<style>
*{
  background-color:cornflowerblue;
  padding: 0;
  margin: 0;
}
.main{
  display: grid;
  justify-content: center;
  align-items: center;
}
.main h1{
  color:#fff;
}
.formApp{
  margin: 20px 0;
  display: flex;
  justify-content: space-between;
}
.formApp input{
  outline: none;
  border: none;
  background-color: beige;
  border-radius: 5px;
  margin:0 15px;
  width: 400px;
  height: 30px;
  padding: 10px;
}
.formApp button{
  outline: none;
  border: none;
  background-color: crimson;
  padding: 15px;
  border-radius: 10px;
  color: #fff;
}
.formApp label{
  color: #fff;
  font-size: 20px;
  font-weight: 700;
}

</style>