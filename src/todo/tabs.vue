<template>
  <div class="helper">
    <span class="left">{{unFinishedTodoLength}} items left</span>
    <span class="tabs">
      <span v-for="state in states" :key="state" :class="[state,filter === state ? 'active' : '']" @click="toggleFilter(state)">{{state}}</span>
    </span>
    <span class="clear" @click="clearAllCompleted">Clear completed</span>
  </div>
</template>
<script>
export default {
  props: {
    filter: {
      type: String,
      required : true
    },
    todos: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      state: ['all','active','completed']
    }
  },
  computed: {
    unFinishedTodoLength() {
      return this.todos.filter( todo => !todo.completed).length
    }
  },
  methods: {
    clearAllCompleted() {
      this.$emit('clearAllCompleted')
    },
    toggleFilter(state) {
      this.$emit('toggle',state)
    }
  }
}
</script>