<script setup>
import AppUserCard from '@/components/AppUserCard.vue'
import AppSpinner from '@/components/AppSpinner.vue'
</script>

<template>
  <AppUserCard>
    <template #userCard="{ users }">
      <div class="flix">
        <h1>About Esteemed Customers</h1>
      </div>
      <div class="container">
        <div v-for="user in users" :key="user.email" class="card">
          <div class="card-head">
            <div class="user-image">
              <img :src="user.picture.large" alt="{{`${user.name.first} ${user.name.last}`}}" />
            </div>
          </div>
          <div class="grid">
            <span>{{ user.name.first }}</span>
            <span>{{ user.cell }}</span>
          </div>
        </div>
      </div>
      <div class="flex">
        <router-link :to="{ name: 'home' }" class="button">Home</router-link>
      </div>
    </template>

    <template #loading>
      <AppSpinner />
    </template>
  </AppUserCard>
</template>

<style lang="css" scoped>
.flix h1 {
  color: #fff;
}
.flix {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 10rem;
}
.card {
  max-width: 250px;
  background-color: rgb(245, 216, 176);
}
.card-head {
  position: relative;
  height: 130px;
  display: flex;
  justify-content: center;
  align-items: center;
}
.user-image {
  width: 100%;
  height: 100%;
}
.margin {
  font-weight: bolder;
  font-size: 1.5rem;
  margin-top: 5rem;
}
</style>
