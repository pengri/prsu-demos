<template>
  <div class="common-layout">
    <el-container style="height: 100%">
      <el-aside width="200px">
        <div class="common-menu">
          <el-row justify="space-between" align="middle">
            <h2 class="common-menu-title">北医AI</h2>
            <el-avatar class="common-menu-avatar" :size="26" :src="circleUrl" />
          </el-row>
          <el-menu
            background-color="#ECECEE"
            class="el-menu-vertical-demo"
            :default-active="activeId"
            text-color="#000"
            active-text-color="#000"
          >
            <template v-for="menu in menus" :key="menu.id">
              <el-menu-item
                v-if="!menu.children"
                :index="menu.id"
                :key="menu.id"
                @click="handleClick(menu)"
              >
                <el-icon class="menu-icon"
                  ><component v-if="menu.icon" :is="menu.icon"></component
                ></el-icon>
                <span>{{ menu.name }}</span>
              </el-menu-item>
              <el-sub-menu v-else :index="menu.id" :key="menu.id">
                <template #title>
                  <el-icon class="menu-icon"
                    ><component v-if="menu.icon" :is="menu.icon"></component
                  ></el-icon>
                  <span>{{ menu.name }}</span>
                </template>
                <template v-for="child in menu.children" :key="child.id">
                  <el-menu-item :index="child.id" @click="handleClick(menu)">{{
                    child.name
                  }}</el-menu-item>
                </template>
              </el-sub-menu>
            </template>
          </el-menu>
        </div>
      </el-aside>
      <el-main>
        <RouterView></RouterView>
      </el-main>
    </el-container>
  </div>
</template>
<script lang="ts">
import { ref } from 'vue'

import IconTeacherAssist from '@/components/icons/IconTeacherAssit.vue'
import IconKnList from '@/components/icons/IconKnList.vue'
import IconMakeTest from '@/components/icons/IconMakeTest.vue'
import IconQA from '@/components/icons/IconQA.vue'
import IconReadWrite from '@/components/icons/IconReadWrite.vue'
import IconTeacherAssit from '@/components/icons/IconTeacherAssit.vue'
</script>
<script setup lang="ts">
import { RouterView, useRouter } from 'vue-router'
const circleUrl = 'https://cube.elemecdn.com/3/7c/3ea6beec64369c2642b92c6726f1epng.png'
const menus = [
  {
    name: '自由问答',
    id: 'm1',
    path: '',
    icon: IconQA
  },
  {
    name: '课程助教',
    id: 'm2',
    path: 'assistant',
    icon: IconTeacherAssist
  },
  {
    name: '知识大纲',
    id: 'm3',
    icon: IconKnList
  },
  {
    name: '智能读写',
    id: 'm4',
    icon: IconReadWrite
  },
  {
    name: '智能出题',
    id: 'm5',
    icon: IconMakeTest,
    children: [
      {
        name: '单选',
        id: 'm5-1'
      },
      {
        name: '多选',
        id: 'm5-2'
      },
      {
        name: '问答',
        id: 'm5-3'
      },
      {
        name: '填空',
        id: 'm5-4'
      },
      {
        name: '判断',
        id: 'm5-5'
      }
    ]
  }
]

const router = useRouter()
const activeId = ref('m1')
const handleClick = (menu: any) => {
  activeId.value = menu.id
  router.push(`/chat/${menu.path}`)
}
</script>

<style scoped lang="scss">
.common-menu-title {
  padding: 20px 0 20px 45px;
  font-weight: 600;
}
.common-menu-avatar {
  margin: 20px;
  cursor: pointer;
}
.common-layout {
  width: 100%;
  height: 100%;
}
.common-menu {
  background-color: #ececee;
  height: 100%;
  overflow-y: hidden;
}
.el-menu-vertical-demo {
  background-color: #ececee;
  :deep(.el-sub-menu__title) {
    padding: 0;
    border-radius: 30px;
    margin: 0 20px;
    span {
      font-weight: 600;
    }
  }
  :deep(.el-menu-item) {
    span {
      font-weight: 600;
    }
    padding: 0;
    border-radius: 30px;
    margin: 5px 20px;
    &:hover {
      background-color: white;
    }
    &.is-active {
      background-color: white;
      .menu-icon {
        filter: grayscale(0);
      }
    }
  }
  :deep(.el-sub-menu) {
    .el-menu-item {
      margin-left: 40px;
      font-weight: 400;
    }
  }
}
.menu-icon {
  filter: grayscale(100%);
}
:v-deep() {
  .el-menu {
    height: 100%;
    --el-menu-item-height: 50px;
    overflow-y: auto;
  }
}
</style>
