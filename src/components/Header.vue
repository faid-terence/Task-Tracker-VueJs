<template>
  <!-- Header section with title and button to toggle adding tasks -->
  <header>
    <!-- Display the title passed as a prop -->
    <h1>{{ title }}</h1>
    <!-- Button component with dynamic text and color -->
    <Button @btn-click="$emit('toggle-add-task')" :text="showAddTask ? 'Close' : 'Add Task'" :color="showAddTask ? 'red' : 'green'" />
  </header>
</template>

<script>
// Import the Button component from './Button.vue'
import Button from './Button.vue'

export default {
  // Component name
  name: "Header",
  // Define props for the component
  props: {
    title: String,      // Title prop as a string
    showAddTask: Boolean // showAddTask prop as a boolean
  },
  components: {
    Button, // Register the Button component for use in the template
  }
};
</script>

<style scoped>
/* Scoped CSS for the header component */
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}
</style>
