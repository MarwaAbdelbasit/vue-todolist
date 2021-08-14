<template lang="html">
  <div class="main row">
    <div class="list col">
      <b-list-group>
        <b-list-group-item v-for="item in list" :key="item" class="d-flex justify-content-between align-items-center" v-bind:class="{done:isDone}">
          {{item}}

          <ul class="controls">
            <li>
              <span @click="deleteItem(item)">
                <fa :icon="['fas', 'times-circle']"/>
              </span>
            </li>
          </ul>

        </b-list-group-item>
        <b-list-group-item v-if="newItem">{{newItem}}</b-list-group-item>
      </b-list-group>

      <b-alert :show="showAlert" variant="primary">No tasks to show, you can add a new task below!</b-alert>

      <div class="insert">
        <b-form-input class="inputTask" v-model="newItem" placeholder="Enter new task"></b-form-input>
        <b-button @click="addItem" variant="danger">Add</b-button>
      </div>

      <div class="delFin">
        <b-button @click="markAllDone" variant="danger">Finish All <fa :icon="['fas', 'check-circle']"/></b-button>
        <b-button @click="deleteAll" variant="danger">Delete All <fa :icon="['fas', 'times-circle']"/></b-button>
      </div>
    </div>
    <div class="image col">
      <img src="../assets/todolist.svg" width="350" height="500" class="img-responsive">
    </div>
  </div>
</template>

<script>
export default {
  name: 'Todolist',
  data() {
    return {
      list: [
          'todo1',
          'todo2',
          'todo3',
      ],
      newItem: '',
      showAlert: false,
      isDone: false,
    }
  },
  methods: {
    deleteItem(item) {
      var index = this.list.indexOf(item),
          taskCount = this.list.length;
      this.list.splice(index, 1);
      taskCount--;
      if(taskCount == 0) {
        this.showAlert = true;
      }
    },
    addItem() {
      this.list.push(this.newItem);
      this.newItem = '';
      this.showAlert = false;
    },
    deleteAll() {
      this.list = [];
      this.showAlert = true;
    },
    markAllDone() {
      this.isDone = !this.isDone;
    }
  }
}
</script>

<style lang="css" scoped>
.main {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  margin: auto;
  width: 80%;
  padding: 1.5rem 1rem;
  box-shadow: 0 1px 4px rgba(146, 161, 176, .15);
  background-color: #fff;
  border-radius: 1rem;
  overflow: hidden;
}

.main:hover {
  box-shadow: 0 30px 41px rgb(56 56 56 / 15%);
}

.insert {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  margin-top: 1rem;
}

.insert .inputTask {
  margin-right: 1rem;
}

.delFin {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  margin-top: 1rem;
}

.done {
  text-decoration: line-through;
}

.image {
  width: 100%;
}

.controls {
  list-style: none;
  display: flex;
}

span {
  color: #007bff;
  margin-right: 0.5rem;
  font-size: 1.5rem;
  cursor: pointer;
}
</style>
