<script setup lang="ts"></script>

<template>
  <div class="h-10 px-6 flex items-center gap-3">
    <div class="h-10 w-10">
      <img
        src="https://xsgames.co/randomusers/avatar.php?g=male"
        loading="lazy"
        alt="profile_picture"
        class="w-full h-full object-cover rounded-full"
      />
    </div>
    <input
      type="text"
      placeholder="Your Message ..."
      class="text-slate-500 placeholder:text-slate-500 bg-transparent outline-none flex-1"
    />
    <button><img src="~assets/icons/mic.svg" alt="" /></button>
    <button><img src="~assets/icons/attachment.svg" alt="" /></button>
    <button><img src="~assets/icons/send.svg" alt="" /></button>
  </div>
</template>
