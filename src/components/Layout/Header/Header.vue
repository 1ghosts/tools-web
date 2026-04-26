<script setup lang="ts">
import { ref, reactive, onMounted } from 'vue'
import { Search } from '@element-plus/icons-vue';
import { useToolsStore } from '@/store/modules/tools'
import { useComponentStore } from '@/store/modules/component'
import 'element-plus/theme-chalk/display.css'
import { ToolsInfo } from '@/components/Tools/tools.type.ts';

import router from '@/router';
// const isNavDrawer = ref(false)
const loading = ref(false)
const options = ref<ToolsInfo[]>([])
//store
const toolsStore = useToolsStore()
const componentStore = useComponentStore()
//查询参数
const searchParam = reactive({
  cateId: 0,
  title: '',
  route: '',
})

//search
// const search = async () => {
//   try {
//     await toolsStore.getTools(searchParam)
//     //关闭抽屉
//     isNavDrawer.value = false
//   } catch (error) {
//     console.log(error)
//   }
// }

//选择分类
// const chooseCate = (cateId: number) => {
//   searchParam.cateId = cateId
//   search()
// }

//搜索工具
const searchTools = async (query: string) => {
  loading.value = true
  options.value = []
  if (query) {
    searchParam.title = query
    options.value = await toolsStore.getTools(searchParam)
  }
  loading.value = false
}

const optionClick = (url: string) => {
  router.push(url)
}

onMounted(() => {
})
</script>

<template>
  <header class="h-24 w-full flex justify-between pt-2 pb-2 c-xs:h-16 c-xs:border-b-[1px] items-center">
    <div class="flex items-center w-full">
      <div class="hidden c-sm:block c-md:hidden c-xs:block">
        <svg @click="componentStore.setleftComDrawerStatus(!componentStore.leftComDrawer)" :class="['icon', { 'rotate': componentStore.leftComDrawer }]" t="1702978210636" viewBox="0 0 1024 1024" version="1.1" xmlns="http://www.w3.org/2000/svg" p-id="7618" width="30" height="30">
          <path fill="#444" fill-opacity=".9" d="M895.936 256l-768-0.896 0.128-64L896 192l-0.064 64zM179.2 689.152l202.688-152a32 32 0 0 0 0-51.2L179.2 333.952a32 32 0 0 0-51.2 25.6v304a32 32 0 0 0 51.2 25.6z m12.8-89.6v-176l117.312 88L192 599.552zM896 544H480v-64H896v64z m-0.064 288l-768-0.896 0.128-64L896 768l-0.064 64z" p-id="7619"></path>
        </svg>
      </div>
      
      <!-- c-md:block -->
      <div class="hidden c-md:block">
        <svg @click="componentStore.setLeftComStatus(!componentStore.leftCom)" :class="['icon', { 'rotate': componentStore.leftCom }]" t="1702978210636" viewBox="0 0 1024 1024" version="1.1" xmlns="http://www.w3.org/2000/svg" p-id="7618" width="30" height="30">
          <path fill="#444" fill-opacity=".9" d="M895.936 256l-768-0.896 0.128-64L896 192l-0.064 64zM179.2 689.152l202.688-152a32 32 0 0 0 0-51.2L179.2 333.952a32 32 0 0 0-51.2 25.6v304a32 32 0 0 0 51.2 25.6z m12.8-89.6v-176l117.312 88L192 599.552zM896 544H480v-64H896v64z m-0.064 288l-768-0.896 0.128-64L896 768l-0.064 64z" p-id="7619"></path>
        </svg>
      </div>
    

      <div class="ml-3 mr-1">
        <router-link to="/">
          <svg t="1715590310537" class="icon" viewBox="0 0 1053 1024" version="1.1" xmlns="http://www.w3.org/2000/svg" p-id="4287" width="25" height="25">
            <path d="M526.63454 58.067422a21.503527 21.503527 0 0 1-27.501109 0.175539l474.979265 381.50475a31.538506 31.538506 0 1 0 39.496274-49.150919L538.629705 9.004273a41.602742 41.602742 0 0 0-51.988799 0.234052L11.573871 398.671586a31.538506 31.538506 0 1 0 39.993635 48.79984L526.63454 58.067422z" fill="#2c2c2c" p-id="4288"></path><path d="M1013.60897 564.087832L538.629705 182.583083a41.602742 41.602742 0 0 0-51.988799 0.204795L11.573871 572.191883a31.538506 31.538506 0 1 0 39.993635 48.79984l66.763331-54.709653v361.61033A94.644775 94.644775 0 0 0 213.004869 1022.537175H441.732179v-247.275931a15.79851 15.79851 0 0 1 15.739997-15.79851h110.472541c8.68918 0 15.769253 7.080073 15.769253 15.79851v247.275931H812.441281a94.615518 94.615518 0 0 0 94.644775-94.615518V559.465305l66.997383 53.831959a31.538506 31.538506 0 1 0 39.525531-49.209432z m-169.629183 363.804568c0 17.436874-14.101633 31.538506-31.567763 31.538506h-165.591785v-184.198919a78.875522 78.875522 0 0 0-78.875522-78.904778h-110.472541a78.875522 78.875522 0 0 0-78.846265 78.904778v184.198919h-165.591786c-17.46613 0-31.597019-14.130889-31.597019-31.538506V514.527323L512.883986 242.851471l331.095801 265.941578v419.128608z" fill="#2c2c2c" p-id="4289" stroke="black" stroke-width="10"></path>
          </svg>
        </router-link>
      </div>
      
    
      <div class="c-xs:w-[85%] w-full mr-3">
        <!-- <el-input 
          v-model="searchParam.title" 
          placeholder="搜索工具" 
          class="h-10 ml-3" 
          @keyup.enter.native="search">
          <template #append>
            <el-button :icon="Search" @click="search"/>
          </template>
        </el-input> -->
        <el-select
          v-model="searchParam.title"
          filterable
          remote
          reserve-keyword
          remote-show-suffix
          :suffix-transition="false"
          :suffix-icon="Search"
          placeholder="输入关键词搜索，如文本、json、图片等"
          :remote-method="searchTools"
          :loading="loading"
          class="ml-3"
          size="large"
        >
          <el-option
            v-for="item in options"
            :key="item.id"
            :label="item.title + ' - ' + item.desc"
            :value="item.id"
            @click="optionClick(item.url)"
          >
          </el-option>
        </el-select>
      </div>
    </div>
  </header>
</template>

<style scoped>


/* 科技感搜索框 */
.el-select :deep(.el-select__wrapper){
  background: linear-gradient(135deg, #ffffff 0%, #f8f9ff 100%);
  border: 1px solid rgba(64, 158, 255, 0.2);
  border-radius: 8px;
  transition: all 0.3s ease;
  box-shadow: 0 2px 8px rgba(64, 158, 255, 0.1);
}

/* 搜索框容器 */
.el-select {
  transition: width 0.3s ease;
}

.el-select :deep(.el-select__wrapper):hover {
  border-color: #409EFF;
  box-shadow: 0 4px 12px rgba(64, 158, 255, 0.2);
}

.el-select :deep(.el-select__wrapper.is-focus) {
  border-color: #409EFF;
  box-shadow: 0 0 0 2px rgba(64, 158, 255, 0.2);
}

/* 科技感图标 */
.icon {
  transition: all 0.3s ease;
  transform-origin: center;
}

.icon:hover {
  transform: scale(1.1);
  filter: drop-shadow(0 0 8px rgba(64, 158, 255, 0.5));
}

/* 旋转动画 */
.icon.rotate {
  transform: rotate(180deg);
}

/* 简约Header */
header {
  background: transparent;
  position: relative;
}
</style>
