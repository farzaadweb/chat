<script setup lang="ts">
import { RouterLink } from "vue-router";

const { onlineUsers } = defineProps(["onlineUsers"]);
</script>

<template>
  <div class="box">
    <div
      class="bg-yellow-100 border border-slate-500 px-4 py-0.5 rounded-2xl flex justify-between items-center"
    >
      <span class="font-medium text-slate-600">Online now</span>
      <NuxtLink
        to="/online-users"
        class="text-yellow-500 text-sm transition-all"
        >show all</NuxtLink
      >
    </div>
    <div
      class="mt-2 grid grid-cols-5 gap-3 border border-slate-500 rounded-2xl px-4 py-3"
    >
      <RouterLink
        class="relative z-50 profile"
        v-for="(user, index) in onlineUsers.slice(0, 5)"
        :key="index"
        :to="`/chat/${user.login.uuid}`"
      >
        <img
          :src="user.picture.medium"
          loading="lazy"
          alt="profile_picture"
          class="rounded-2xl shadow-lg"
      /></RouterLink>
    </div>
  </div>
</template>

<style scoped>
.profile::before {
  content: "";
  width: 1rem;
  height: 1rem;
  background-color: #15803d;
  border-radius: 999px;
  position: absolute;
  right: -5px;
  bottom: 1px;
  border: 2px solid white;
}
.profile::after {
  content: "";
  position: absolute;
  left: 0;
  bottom: 0;
  z-index: -10;
  width: 100%;
  height: 100%;
  border-bottom: 5px solid #eab308;
  border-left: 5px solid #99f6e4;
  border-radius: 1rem;
  background-color: #fef9c3;
  transition: all 0.1s;
}
.profile:hover::after {
  left: -4px;
  bottom: -4px;
}
</style>
