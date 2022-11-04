<template>
  <div>
   <Todo/>
  </div>
</template>

<script>
// @ is an alias to /src
import Todo from '@/components/Todo.vue'

export default {
  name: 'HomeView',
  components: {
   Todo
  }
}
</script>
