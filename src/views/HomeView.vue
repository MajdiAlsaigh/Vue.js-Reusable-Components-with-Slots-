<script setup>
import AppUserCard from '@/components/AppUserCard.vue'
import AppSpinner from '@/components/AppSpinner.vue'
import AppButton from '@/components/AppButton.vue'
import AppIcon from '@/components/AppIcon.vue'
</script>

<template>
  <AppUserCard>
    <template #userCard="{ users, remove }">
      <div class="flix">
        <h1>Esteemed Customers</h1>
      </div>

      <div class="container">
        <div v-for="user in users" :key="user.email" class="card">
          <div class="card-head">
            <a href="#"><i class="fas fa-envelope"></i>{{ user.email }}</a>
            <div class="user-image">
              <img :src="user.picture.large" alt="{{`${user.name.first} ${user.name.last}`}}" />
            </div>
          </div>
          <div class="card-body">
            <div class="user-post-address">
              <div>
                <span>{{ user.location.street.number }}</span
                ><span>Street Address</span>
              </div>
              <div>
                <span>{{ user.location.postcode }}</span
                ><span>Postcode</span>
              </div>
              <div>
                <span>{{ user.location.street.name }}</span
                ><span>Street Name</span>
              </div>
            </div>
            <div class="user-name">
              <span class="user-name-title">{{ user.name.title }}.</span>
              <span class="user-name-full">{{ user.name.first }} {{ user.name.last }}</span>
              <span class="user-age">&nbsp;{{ user.dob.age }}</span>
            </div>
            <div class="user-location-address">
              <span
                >{{ user.location.state }}, {{ user.location.city }},
                {{ user.location.country }}</span
              >
            </div>
          </div>
          <div class="card-foot">
            <div class="user-contact-info">
              <span> <i class="fas fa-phone"></i>&nbsp;{{ user.phone }}</span>
              <span> <i class="fa-solid fa-mobile-button"></i>&nbsp;{{ user.cell }}</span>
            </div>
          </div>
          <!-- @click="log" -->
          <AppButton @click="remove(user)">
            <AppIcon>&hearts;</AppIcon>
            Remove
            <AppIcon>&hearts;</AppIcon>
          </AppButton>
        </div>
      </div>

      <div class="flex">
        <router-link :to="{ name: 'about' }" class="button">About</router-link>
      </div>
    </template>

    <template #loading>
      <AppSpinner />
    </template>
  </AppUserCard>
</template>

<style lang="css" scoped>
.container p {
  color: #fff;
}
.card {
  background-color: rgb(253, 247, 238);
}
.flix h1 {
  color: #fff;
}
.flix {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 10rem;
}
</style>
