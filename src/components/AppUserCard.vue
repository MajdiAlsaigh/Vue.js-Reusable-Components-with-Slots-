<script setup>
import { onMounted, ref } from 'vue'

// to remove  Card of user
const remove = (user) => {
  users.value = users.value.filter((intry) => intry.email !== user.email)
}

// Define states
const states = {
  idle: 'idle',
  loading: 'loading',
  loaded: 'loaded',
  failed: 'failed'
}

// Define reactive variables for state, data, and error
const state = ref(states.idle)
const users = ref([])
const error = ref(undefined)

const load = async () => {
  // Set state to 'loading', data to undefined, and error to undefined
  state.value = states.loading
  error.value = undefined // Reset error before fetching

  setTimeout(async () => {
    try {
      const response = await fetch('https://randomuser.me/api/?results=3')
      const responseData = await response.json()
      users.value = responseData.results
      state.value = states.loaded
    } catch (error) {
      error.value = error.message // Assigning the error message to the error ref
      state.value = states.failed
    }
  }, 1000)
}

// Call the load function when the component is mounted
onMounted(() => {
  load()
})
</script>

<template>
  <main>
    <div v-if="state === states.loaded">
        <slot name="userCard" :users="users" :remove="remove"></slot>
    </div>

    <slot v-else-if="state === states.loading" name="loading" />

    <slot v-else-if="state === states.failed" name="error">
      <div class="grid-container">
        <div class="">
          <img
            src="https://cdni.iconscout.com/illustration/premium/thumb/something-went-wrong-4344457-3613885.png"
            alt=""
          />
        </div>
        <h2>Oops! Something Went Wrong!</h2>
        <p>We're sorry, but something unexpected happened. Please try again later.</p>
      </div>
    </slot>
  </main>
</template>

<style lang="css">
.grid-container {
  display: grid;
  grid-template-columns: 1fr;
  gap: 1rem;
  place-items: center;
  margin-top: -20rem;
}
.grid-container h2,
.grid-container p {
  color: #fff;
}
.grid-container p {
  padding: 0.5rem;
  border-top: 2px solid #fff;
}
</style>
