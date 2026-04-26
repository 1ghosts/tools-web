<script setup lang="ts">
import {  ref } from 'vue';
const appDesc = ref(import.meta.env.VITE_APP_DESC || '')
const currentYear: number = new Date().getFullYear();
</script>

<template>
  <div class="w-full rounded-2xl z-10 p-5 text-center tech-footer">
    <el-text>{{ appDesc }} © {{ currentYear }}</el-text>
  </div>
</template>

<style scoped>
/* 简约页脚 */
.tech-footer {
  background: transparent;
  border: none;
  position: relative;
}
</style>
