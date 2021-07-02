<template>
  <div class="container">
    <h2>My Vue todo App</h2>

    <div class="todo-input">
      <input v-model='task' type="text" name="todo input" placeholder="insert you task here">
      <button @click='submitTask'>Submit</button>
    </div>

    <ul class="todo-list" v-for="(task, index) in tasks" :key="index">
      <li>
        <p>{{task.name}}</p>
        <div class="pointer status" @click="changeStatus(index)">
          {{task.status}}
        </div>
        <div @click="editTask(index)" class="pointer">
          <span class="fa fa-pen"></span>
        </div>
        <div @click="deleteTask(index)" class="pointer">
          <span class="fa fa-trash"></span>
        </div>
      </li>
    </ul>
  </div>

</template>

<script lang="ts">
export default {
  name: 'TodoContainer',

  data() {
    return {
      task: '',
      editedTask: -1,
      taskStatusList: ['to do', 'in prgress', 'done'],
      tasks: [
        {
          name: 'Test 1',
          status: 'done',
        },
        {
          name: 'Test 3',
          status: 'in progress',
        },
      ],
    };
  },

  methods: {
    submitTask():void {
      if (this.task.length > 0 && this.editedTask === -1) {
        this.tasks.push({
          name: this.task,
          status: this.taskStatusList[0],
        });
      } else {
        this.tasks[this.editedTask].name = this.task;
        this.editedTask = -1;
      }
      this.task = '';
    },

    deleteTask(index: number):void {
      this.tasks.splice(index, 1);
    },

    editTask(index: number):void {
      this.task = this.tasks[index].name;
      this.editedTask = index;
    },

    changeStatus(index: number):void {
      let newIndex = this.taskStatusList.indexOf(this.tasks[index].status);
      // eslint-disable-next-line no-plusplus
      if (++newIndex > 2) newIndex = 0;
      this.tasks[index].status = this.taskStatusList[newIndex];
    },
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
    min-height: 3rem;

    p{
      width: 70%;
      text-align: left;
      padding: 0.5rem;
    }
    div{
      background: rgb(224, 223, 223);
      margin-left: 0.5rem;
      padding: 10px;
      border-radius: 24px;
      width: 48px;
    }
    .status{
      width: 8rem;
    }
    .pointer{
      cursor: pointer;
    }
  }
}

</style>
