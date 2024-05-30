<script setup>
//defineProps({
//  msg: {
//    type: String,
//    required: true
//  }
//})
</script>

<template>
  <div class="bug-form">
    <h2>Report a Bug</h2>
    <form @submit.prevent="submitBug">
      <div>
        <label for="title">Title:</label>
        <input type="text" v-model="title" id="title" required />
      </div>
      <div>
        <label for="description">Description:</label>
        <textarea v-model="description" id="description" required></textarea>
      </div>
      <button type="submit">Submit</button>
    </form>
  </div>
</template>

<style scoped>
/* Add your styles here */
.bug-form {
  max-width: 600px;
  margin: 0 auto;
  padding: 2em;
  border: 1px solid #ddd;
  border-radius: 4px;
  background-color: #f9f9f9;
}

.bug-form form {
  display: flex;
  flex-direction: column;
}

.bug-form form div {
  margin-bottom: 1em;
}

.bug-form label {
  margin-bottom: 0.5em;
  font-weight: bold;
}

.bug-form input, .bug-form textarea {
  padding: 0.5em;
  font-size: 1em;
  width: 100%;
  box-sizing: border-box;
}

.bug-form button {
  padding: 0.75em;
  font-size: 1em;
  color: #fff;
  background-color: #007BFF;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.bug-form button:hover {
  background-color: #0056b3;
}
</style>
