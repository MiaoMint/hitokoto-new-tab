<template>
  <div class="p-16 h-screen w-screen dark:text-white">
    <div
      @click="getHitokoto"
      :class="[
        'cursor-pointer transition-all duration-500',
        data ? 'opacity-100' : 'opacity-0',
      ]"
    >
      <h1
        :class="[
          'text-3xl mb-4 bg-black text-white p-3 inline-block hitokoto',
          'dark:bg-white dark:text-black',
        ]"
      >
        {{ data?.hitokoto }}
      </h1>
      <p class="text-sm border-l-4 pl-2 border-black dark:border-white">
        {{ data?.from }}
      </p>
    </div>
  </div>
</template>
<script setup lang="ts">
import { ref } from "vue";

interface Hitokoto {
  id: number;
  uuid: string;
  hitokoto: string;
  type: string;
  from: string;
  from_who: any;
  creator: string;
  creator_uid: number;
  reviewer: number;
  commit_from: string;
  created_at: string;
  length: number;
}

const data = ref<Hitokoto>();

async function getHitokoto() {
  const res = await (await fetch("https://v1.hitokoto.cn/?encode=json")).json();
  data.value = res;
}

getHitokoto();
</script>

<style>
@media (prefers-color-scheme: dark) {
  body {
    background-color: rgb(51, 51, 51);
  }
}
</style>
