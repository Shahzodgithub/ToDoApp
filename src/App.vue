<template>
  <div id="app">
    <h2>
      Plan your tasks
    </h2>
    <div class="tasks-dashboard">
      <Tasks :title="tasks[0]" :selected="selected" />
      <Tasks :title="tasks[1]" :selected="selected"/>
      <Tasks :title="tasks[2]" :selected="selected"/>
      <Tasks :title="tasks[3]" :selected="selected"/>
    </div>
    <router-view />
  </div>
</template>



<script>
import Tasks from "./components/Tasks.vue";
export default {
  data() {
    return {
      tasks: ["To Do", "In Progress", "Testing", "Complete"],
    };
  },
  components: { Tasks },
  methods: {
    selected() {
      this.tasks.forEach((value, index) => {
        return index;
      })
    }
  },
};
</script>

<style>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.tasks-dashboard {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
}

h2 {
  color: #42b983;
  margin-bottom: 60px;
  margin-top: 50px;
}
</style>
