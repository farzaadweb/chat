<script setup lang="ts">
import { RouterLink } from "vue-router";
import { ref, watch } from "vue";

const { users } = defineProps(["users"]);
let allUsers = users;
let serachText = ref("");

let handleSearch = (text: string) => {
  if (!text) return;
  return users.filter((u: any) => {
    let fullName = `${u.name.first} ${u.name.last}`;
    if (fullName.startsWith(text)) return u;
  });
};

watch(serachText, (n, o) => {
  if (!n) return (allUsers = users);
  allUsers = handleSearch(n);
});
</script>

<template>
  <div>
    <h3 class="text-lg font-medium">Messages</h3>
    <div
      class="mt-2 bg-yellow-100 flex items-center py-2.5 px-4 rounded-2xl border border-slate-500"
    >
      <img src="~assets/icons/search.svg" alt="" class="w-6" />
      <input
        type="text"
        class="bg-transparent ml-4 outline-none placeholder:text-sm text-sm text-slate-500"
        placeholder="search by name"
        v-model="serachText"
      />
    </div>
    <div class="mt-6 space-y-6">
      <NuxtLink
        :to="`/chat/${user.login.uuid}`"
        v-for="(user, index) in allUsers.slice(0, 10)"
        :key="user.login.uuid"
        class="flex items-center justify-between hover:shadow-md rounded-xl box"
      >
        <div class="flex items-center">
          <div class="h-14 w-14">
            <img
              :src="user.picture.medium"
              loading="lazy"
              alt="profile_picture"
              class="rounded-3xl shadow-lg"
            />
          </div>
          <div class="ml-3">
            <span class="font-medium block"
              >{{ user.name.first }} {{ user.name.last }}</span
            >
            <span class="text-sm"
              ><span class="text-slate-400">phone</span>
              <span class="text-slate-500 ml-2">+ {{ user.phone }}</span></span
            >
          </div>
        </div>
        <span
          v-if="index % 2 === 0"
          class="text-xs text-red-500 px-2 py-0.5 bg-red-100 border border-red-500 rounded-xl"
          >new</span
        >
      </NuxtLink>
    </div>
  </div>
</template>
