<script setup lang="ts">
let users = ref([]);

async function fetchUsers<T>(): Promise<T[]> {
  let { data } = await useFetch<T>("https://randomuser.me/api?results=20");
  if (!data.value) return (users.value = []);
  return (users.value = data.value?.results);
}

fetchUsers();
</script>
<template>
  <div class="h-[calc(100vh-3.5rem)]">
    <div class="grid lg:grid-cols-5 h-full">
      <div class="col-span-1 px-6 py-6 max-h-full overflow-y-auto side-bar">
        <div class="flex items-center box">
          <div class="h-16 w-16 p-0.5 rounded-full border-2 border-yellow-400">
            <img
              src="https://xsgames.co/randomusers/avatar.php?g=male"
              loading="lazy"
              alt="profile_picture"
              class="w-full h-full object-cover rounded-full"
            />
          </div>
          <div class="ml-4">
            <h3 class="font-medium">Mohamad Amin</h3>
            <span class="text-sm text-slate-400 block">My Account</span>
          </div>
        </div>
        <div v-if="users.length" class="">
          <div class="py-6">
            <Online :onlineUsers="users" />
          </div>
          <div class="py-4">
            <Messages :users="users" />
          </div>
        </div>
      </div>
      <div class="col-span-4 py-6 px-6"><slot /></div>
    </div>
    <footer class="bg-slate-100 py-4">
      <p class="text-slate-500 text-sm text-center">
        © All Rights Reserved by
        <a
          href="https://www.linkedin.com/in/farzadfarzanehnya/"
          class="border-b border-slate-600 border-dashed"
          >Farzad Farzanehnya</a
        >
      </p>
    </footer>
  </div>
</template>

<style scoped>
.side-bar::-webkit-scrollbar {
  display: none;
}
.side-bar {
  -ms-overflow-style: none; /* IE and Edge */
  scrollbar-width: none; /* Firefox */
}
</style>
