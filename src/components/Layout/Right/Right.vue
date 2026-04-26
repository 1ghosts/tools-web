<script setup lang="ts">
import { Tools } from '@element-plus/icons-vue'
import { useToolsStore } from '@/store/modules/tools'

// 右侧广告位已注释，避免硬编码外部广告资源。

//store
const toolsStore = useToolsStore()
</script>

<template>
  <div>
    <!-- 右侧广告轮播已注释 -->
    <!-- hot tools -->
    <div class="mt-3 border-solid rounded border-gray border p-3 c-xs:mr-3 c-xs:ml-3">
      <div class="text-xl text-gray-400 font-bold">随机推荐</div>
      <ul class="mt-3">
        <RouterLink :to="item.url" class="flex items-center hover:bg-gray-200 p-1 rounded" v-for="(item, index) in toolsStore.recommends" :key="index">
          <el-icon class="mr-1"><Tools /></el-icon>
          <div>{{ item.title }}</div>
        </RouterLink>
      </ul>
    </div>
  </div>
</template>

<style scoped>

</style>
