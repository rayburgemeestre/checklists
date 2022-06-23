<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8" md="6">
      <v-card>
        <v-card-title class="headline">
          Checklists
        </v-card-title>
        <v-card-text>
          <input type="text" @keyup.enter="addTodo" placeholder="What needs to be done?">
        </v-card-text>
        <v-container>
          <ul>
            <li v-for="todo in todos" :key="todo.id">
              <input :checked="todo.done" @change="toggle(todo)" type="checkbox" :id="todo.id">
              <label :class="{ done: todo.done }" :for="todo.id">{{ todo.text }}</label>
              <button @click="removeTodo(todo)">remove</button>
            </li>
          </ul>
        </v-container>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
import { mapMutations } from 'vuex'

export default {
  name: 'InspirePage',

  computed: {
    todos () {
      return this.$store.state.todos.list
    }
  },
  methods: {
    addTodo (event) {
      this.$store.commit('todos/add', event.target.value)
      event.target.value = ''
    },
    ...mapMutations({
      toggle: 'todos/toggle'
    }),
    removeTodo (todo){
      this.$store.commit('todos/remove', todo)
    }
  }
}
</script>

<style scoped>
div {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

ul {
  display: inline-flex;
  flex-direction: column;
  align-items: flex-start;
}

li {
  display: flex;
  align-items: center;
  margin-bottom: 0.5rem;
}

input[type="checkbox"] {
  margin: 0.5rem;
}

button {
  padding: 0.5rem 1rem;
  font-size: 1rem;
}

.done {
  text-decoration: line-through;
}
</style>
