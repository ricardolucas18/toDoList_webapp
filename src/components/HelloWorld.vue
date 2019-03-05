/* eslint-disable */
<template>
  <div class="hello">
    <h1>{{ pageTitle }}</h1>
    <div>
      <div>
        <div style="margin: 100px;">
          <b-card>
            <div class="row">
              <div class="col-md-12">
                <div class="well">
                  <h3>Create a New Todo</h3>
                  <form>
                    <div class="form-group">
                      <label for="todoitem">Todo Title</label>
                      <input
                        type="text"
                        v-model="title"
                        class="form-control"
                        id="todoitem"
                        placeholder="EX: My Homework"
                      >
                      <label for="todoitem">Todo Description</label>
                      <b-form-textarea
                        id="tododescription"
                        v-model="description"
                        placeholder="EX: I have to read page 34 and solve the exercises on page 35"
                        rows="3"
                        max-rows="6"
                      />
                    </div>

                    <b-button type="button" variant="success" v-on:click="add()">Create</b-button>
                  </form>
                </div>
              </div>
            </div>
          </b-card>
        </div>

        <!--<b-table :items="toDoList" :tbody-tr-class="rowClass" />-->
        <b-list-group>
          <div v-for="(item, index) in toDoList" style="margin: 20px;">
            <b-list-group-item
              href="#"
              class="flex-column align-items-start"
              :variant="item.status"
            >
              <div class="d-flex w-100 justify-content-between">
                <h3 class="mb-1">{{item.title}}</h3>
                <small>{{item.date}}</small>
              </div>

              <p class="mb-1">{{item.description}}</p>
              <div style="margin-top: 20px;">
                <b-button variant="danger" v-on:click="remove(index)">Remove</b-button>
                <b-button v-if="checkStatus(index)" variant="success" v-on:click="statusChange(index)">Done</b-button>
              </div>
            </b-list-group-item>
          </div>
        </b-list-group>
      </div>
    </div>
  </div>
</template>

<script>
import moment from "moment";

export default {
  name: "HelloWorld",
  data() {
    return {
      title: "",
      description: "",
      pageTitle: "Welcome to your todo list webapp!",
      toDoList: []
    }
  },
  methods: {
    add() {
      const tododate = moment().format("MM/DD/YYYY hh:mm");
      const todo = {
        title: this.title,
        description: this.description,
        date: tododate,
        status: "warning"
      }
      this.toDoList.push(todo)
      this.title = ""
      this.description = ""
      console.log("button")
    },
    remove(index) {
      console.log(index)
      this.toDoList.splice(index, 1);
    },
    statusChange(index) {
      const actualState = this.toDoList[index].status;

      switch (actualState) {
        case "warning":
          this.toDoList[index].status = "success"
          break

        case "success":
          this.toDoList[index].status = "warning"
          break
        default:
        // code block
      }
    },
    checkStatus(index) {
      const actualState = this.toDoList[index].status;

      switch (actualState) {
        case "warning":
          return true
          break

        case "success":
          return false
          break
        default:
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
