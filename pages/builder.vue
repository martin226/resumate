<template>
  <div class="flex flex-col">
    <div class="flex min-h-screen flex-col">
      <nav class="rounded border-gray-200 bg-white px-8 py-2.5">
        <div
          class="container mx-auto flex flex-wrap items-center justify-between"
        >
          <NuxtLink to="/" class="flex items-center">
            <span class="self-center whitespace-nowrap text-xl font-semibold"
              >Resumate</span
            >
          </NuxtLink>
        </div>
      </nav>
      <div class="flex flex-1">
        <BuilderTemplate
          @template="(i) => (template = i)"
          @next="stage++"
          v-if="stage == 0"
        />
        <BuilderCreate @next="stage++" v-if="stage == 1" :template="template" />
      </div>
    </div>
  </div>
</template>

<script>
import Pages from './index.vue'
export default {
  name: 'BuilderPage',
  components: { Pages },
  data() {
    return {
      stage: 0,
      template: 0,
    }
  },
}
</script>
