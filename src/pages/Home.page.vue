<script setup lang="ts">
import { Heart } from '@vicons/tabler';
import { useHead } from '@vueuse/head';
import ColoredCard from '../components/ColoredCard.vue';
import ToolCard from '../components/ToolCard.vue';
import { useToolStore } from '@/tools/tools.store';
import { config } from '@/config';

const toolStore = useToolStore();

useHead({ title: 'Tooly - Handy dev tools' });
</script>

<template>
  <div class="home-page">
    <div class="grid-wrapper">
      <n-grid v-if="config.showBanner" x-gap="12" y-gap="12" cols="1 400:2 800:3 1200:4 2000:8">
        <n-gi>
          <ColoredCard title="Like Tooly?" :icon="Heart">
            Give us a star on
            <a
              href="https://github.com/Gyarbij/tooly"
              rel="noopener"
              target="_blank"
              aria-label="Tooly' GitHub repository"
            >GitHub</a>
            or follow us on
            <a
              href="https://twitter.com/gyarbij"
              rel="noopener"
              target="_blank"
              aria-label="Gyarbij Twitter"
            >Twitter</a>! Thank you
            <n-icon :component="Heart" />
          </ColoredCard>
        </n-gi>
      </n-grid>

      <transition name="height">
        <div v-if="toolStore.favoriteTools.length > 0">
          <n-h3>Your favorite tools</n-h3>
          <n-grid x-gap="12" y-gap="12" cols="1 400:2 800:3 1200:4 2000:8">
            <n-gi v-for="tool in toolStore.favoriteTools" :key="tool.name">
              <ToolCard :tool="tool" />
            </n-gi>
          </n-grid>
        </div>
      </transition>

      <div v-if="toolStore.newTools.length > 0">
        <n-h3>Newest tools</n-h3>
        <n-grid x-gap="12" y-gap="12" cols="1 400:2 800:3 1200:4 2000:8">
          <n-gi v-for="tool in toolStore.newTools" :key="tool.name">
            <ToolCard :tool="tool" />
          </n-gi>
        </n-grid>
      </div>

      <n-h3>All the tools</n-h3>
      <n-grid x-gap="12" y-gap="12" cols="1 400:2 800:3 1200:4 2000:8">
        <n-gi v-for="tool in toolStore.tools" :key="tool.name">
          <transition>
            <ToolCard :tool="tool" />
          </transition>
        </n-gi>
      </n-grid>
    </div>
  </div>
</template>

<style scoped lang="less">
.home-page {
  padding-top: 50px;
}

.n-h3 {
  margin-bottom: 10px;
}

::v-deep(.n-grid) {
  margin-bottom: 30px;
}

.height-enter-active,
.height-leave-active {
  transition: all 0.5s ease-in-out;
  overflow: hidden;
  max-height: 500px;
}

.height-enter-from,
.height-leave-to {
  max-height: 42px;
  overflow: hidden;
  opacity: 0;
  margin-bottom: 0;
}
</style>