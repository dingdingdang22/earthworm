<template>
  <div
    class="flex w-full items-center justify-between rounded-lg bg-purple-600 px-4 py-1 text-white"
    v-if="showNotice"
  >
    <span class="font-bold"
      >【邀请函】加入 Earthworm 创始会员 与我们一起成就更好的英语学习平台</span
    >
    <div class="flex space-x-4">
      <button
        class="text-black"
        @click="dismissNotice"
      >
        不感兴趣
      </button>
      <button
        class="rounded-lg bg-white px-4 font-bold text-purple-600"
        @click="handleShowDetails"
      >
        查看详情
      </button>
    </div>
  </div>
</template>

<script setup lang="ts">
import { onMounted, ref } from "vue";

const showNotice = ref(true);

onMounted(() => {
  showNotice.value = shouldShowNotice();
});

function dismissNotice() {
  setNoticeDismissed();
  showNotice.value = false;
}

function handleShowDetails() {
  window.open("https://earthworm-docs.cuixueshe.com/get-started/founding-member.html", "_blank");
  showNotice.value = false;
}

function setNoticeDismissed(): void {
  const expirationTime = Date.now() + 48 * 60 * 60 * 1000; // 48小时后的时间戳
  localStorage.setItem("noticeDismissed", expirationTime.toString());
}

function shouldShowNotice(): boolean {
  const dismissedTime = localStorage.getItem("noticeDismissed");
  if (!dismissedTime) return true;

  const currentTime = Date.now();
  return currentTime > parseInt(dismissedTime);
}
</script>

<style scoped></style>
