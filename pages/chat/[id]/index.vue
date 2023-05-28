<script setup lang="ts">
import { useRoute } from "vue-router";
import { ref } from "vue";

definePageMeta({
  layout: "chat-layout",
});

const route = useRoute();
let userDetail = ref<any>(null);

let fetchData = async (id: string | string[]) => {
  let { data } = await useFetch(`https://randomuser.me/api?uuid=${id}`);
  if (!data.value.results.length) return;
  return (userDetail.value = data.value.results[0]);
};
fetchData(route.params.id);
</script>

<template>
  <div
    class="h-full bg-slate-100/70 border border-slate-300 rounded-2xl overflow-hidden flex flex-col"
  >
    <div
      class="sticky top-0 left-0 h-20 px-6 flex justify-between items-center bg-white border-b border-teal-500"
    >
      <div class="flex items-center">
        <img
          :src="userDetail.picture.medium"
          :alt="`${userDetail.name.first} ${userDetail.name.last}`"
          class="w-14 rounded-3xl shadow-lg"
        />
        <div class="ml-3 flex flex-col">
          <span class="text-lg font-semibold"
            >{{ userDetail.name.first }} {{ userDetail.name.last }}</span
          >
          <a
            :href="`mailto:${userDetail.email}`"
            class="text-xs font-light text-slate-500 hover:text-slate-600 transition-all"
            >{{ userDetail.email }}</a
          >
        </div>
      </div>
      <div>
        <button>
          <img src="~assets/icons/call.svg" alt="" class="w-7" />
        </button>
        <button class="ml-3">
          <img src="~assets/icons/video.svg" alt="" class="w-7" />
        </button>
      </div>
    </div>
    <div class="flex-1 py-6 chat px-6">awd</div>
    <div
      class="sticky bottom-0 left-0 py-4 bg-slate-100 border-t border-yellow-500"
    >
      <ChatBar />
    </div>
  </div>
</template>
