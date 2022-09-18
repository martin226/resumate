<template>
  <div class="space-y-8 text-center m-auto">
    <h2 class="text-4xl">First, select a template.</h2>
    <div class="flex flex-row gap-8">
      <img
        src="@/assets/resume1.png"
        class="w-48 h-64 border-2 border-blue-500 cursor-pointer"
        ref="template-0"
        @click="selectTemplate(0)"
      />
      <img
        src="@/assets/resume2.png"
        class="w-48 h-64 border-2 border-black cursor-pointer"
        ref="template-1"
        @click="selectTemplate(1)"
      />
      <img
        src="@/assets/resume3.png"
        class="w-48 h-64 border-2 border-black cursor-pointer"
        ref="template-2"
        @click="selectTemplate(2)"
      />
      <img
        src="@/assets/resume4.png"
        class="w-48 h-64 border-2 border-black cursor-pointer"
        ref="template-3"
        @click="selectTemplate(3)"
      />
    </div>
    <button
      class="bg-blue-500 px-8 py-4 text-xl font-semibold text-white"
      @click="$emit('next')"
    >
      Next
    </button>
  </div>
</template>

<script>
export default {
  name: 'BuilderTemplate',
  data() {
    return {
      selectedTemplate: 0,
    }
  },
  methods: {
    selectTemplate(index) {
      this.selectedTemplate = index
      this.$refs[`template-${index}`].classList.add('border-blue-500')
      this.$refs[`template-${index}`].classList.remove('border-black')
      for (let i = 0; i < 4; i++) {
        if (i !== index) {
          this.$refs[`template-${i}`].classList.add('border-black')
          this.$refs[`template-${i}`].classList.remove('border-blue-500')
        }
      }
      this.$emit('template', index)
    },
  },
}
</script>
