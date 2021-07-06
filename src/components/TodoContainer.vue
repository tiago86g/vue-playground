<template>
  <div class="container">
    <h2>My Vue todo App</h2>

    <div class="todo-input">
      <input
      v-model='task'
      type="text"
      name="todo input"
      placeholder="insert you task here"
      >
      <button @click='submitTask'>Submit</button>
    </div>

    <ul
    class="todo-list"
    v-for="(task, index) in tasks" :key="index">
      <li>
        <p :class="{'done':task.status==='done'}">{{task.name}}</p>
        <div
        class="pointer status"
        :class="{
          'green':task.status==='done',
          'yellow':task.status==='in progress',
          'red':task.status==='to do'
          }"
          @click="changeStatus(index)">
          <p>{{task.status}}</p>
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

<script lang="js">
export default {
  name: 'TodoContainer',

  data() {
    return {
      task: '',
      editedTask: -1,
      taskStatusList: ['to do', 'in progress', 'done'],
      tasks: [
        {
          name: 'Test 1',
          status: 'done',
        },
        {
          name: 'Test 2',
          status: 'to do',
        },
        {
          name: 'Test 3',
          status: 'in progress',
        },
      ],
    };
  },

  methods: {
    submitTask() {
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

    deleteTask(index) {
      this.tasks.splice(index, 1);
    },

    editTask(index) {
      this.task = this.tasks[index].name;
      this.editedTask = index;
    },

    changeStatus(index) {
      let newIndex = this.taskStatusList.indexOf(this.tasks[index].status);
      // eslint-disable-next-line no-plusplus
      if (++newIndex > 2) newIndex = 0;
      this.tasks[index].status = this.taskStatusList[newIndex];
    },
  },
};
</script>

<style scoped lang="scss">
h2{
  padding: 3rem 0 4rem 0;
}
.container{
  display: flex;
  flex-direction: column;
  align-items: center;
  height: 100vh;
  background: rgb(255, 199, 136);

  div {
    width: 40rem;
    max-width: 90vw;

  }
  input{
    border:none;
    background-image:none;
    background-color:transparent;
    box-shadow: none;
    height:3rem;
    width:70%;
    border-bottom: 2px solid #eb6b39;
  }

  button{
    width: 30%;
    height: 3rem;
    background-color: #eb6b39;
    border: 0;
    border-radius: 3rem;
    padding: 0.5rem 1rem;

    &:hover{
      background-color: #ec4e0f;
    }
  }
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
      border-radius: 50%;
      height: 40px;
      max-width: 40px;

      &:hover{
        background: rgb(255, 199, 136);
      }
    }
    .status{
      border-radius: 3rem;
      min-width: 8rem;

      p{
        font-size: 1rem;
        line-height: 0.5rem;
        text-align: center;
        width: 100%;
        font-weight: 700;
      }
    }
    .pointer{
      cursor: pointer;
    }
    .done{
      color: rgb(146, 184, 184);
      text-decoration: line-through;
      }
    .green{
      color: rgb(6, 173, 6);
    }
    .yellow{
      color: rgb(212, 165, 10);
    }
    .red{
      color: rgb(252, 81, 81);
    }
  }
}

</style>
