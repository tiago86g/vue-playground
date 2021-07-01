<template>
  <div class="container">
    <h2>My Vue todo App</h2>

    <div class="todo-input">
      <input type="text" name="todo input" placeholder="insert you task here">
      <button type="submit">Submit</button>
      <v-icon name="oh-Vvue-icon" scale="2"/>
    </div>

    <ul class="todo-list">
      <li>
        <p>Task</p>
        <div class="status">Status</div>
        <div class="edit">Edit</div>
        <div class="delete">Delete</div>
      </li>
    </ul>
  </div>

</template>

<script lang="ts">
import { FaAngleDoubleRight } from 'oh-vue-icons/icons';

export default {
  name: 'TodoContainer',
  props: {
    msg: String,
  },
  components: {
    'v-icon': FaAngleDoubleRight,
  },
};
</script>

<style scoped lang="scss">
.container{
  display: flex;
  flex-direction: column;
  align-items: center;
  height: 100vh;
  background: rgb(255, 199, 136);
}

.todo-list{
  width: 40rem;
  max-width: 90vw;
  background: rgb(233, 255, 255);
  border-radius: 2rem;
  padding: 0.5rem 1rem;
  margin-top: 1rem;

  ul{
    width: 100%;
  }

  li{
    display: flex;
    align-items: center;
    height: 2rem;

    p{
      width: 70%;
      text-align: left;
    }
  }
}

</style>
