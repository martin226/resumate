<template>
  <div>
  <div class="grid grid-cols-6 w-full px-12 mt-16">
    <div class="col-span-2 flex flex-col">
      <h3 class="text-2xl">Tell us about yourself</h3>
      <div class="space-y-4 mt-4">
        <label class="block">
          <span class="text-gray-700">Full name</span>
          <input type="text" class="mt-1 block w-full" placeholder="John Doe" />
        </label>
        <label class="block">
          <span class="text-gray-700">Email</span>
          <input
            type="text"
            class="mt-1 block w-full"
            placeholder="john.doe@email.com"
          />
        </label>
        <label class="block">
          <span class="text-gray-700">Phone number</span>
          <input
            type="text"
            class="mt-1 block w-full"
            placeholder="(123) 456-7890"
          />
        </label>
        <label class="block">
          <span class="text-gray-700">Location</span>
          <input
            type="text"
            class="mt-1 block w-full"
            placeholder="Waterloo, ON"
          />
        </label>
        <label class="block">
          <span class="text-gray-700">Link</span>
          <input
            type="text"
            class="mt-1 block w-full"
            placeholder="mywebsite.com"
          />
        </label>
      </div>
    </div>
    <div class="col-span-4"></div>
  </div>
  <div class="rounded border-black border-2 float-right position-absolute">
     <vue-html2pdf
        :show-layout="false"
        :float-layout="false"
        :enable-download="true"
        :preview-modal="true"
        :paginate-elements-by-height="1400"
        filename="hee hee"
        :pdf-quality="2"
        :manual-pagination="false"
        pdf-format="a4"
        pdf-orientation="landscape"
        pdf-content-width="800px"
 
        @progress="onProgress($event)"
        @hasStartedGeneration="hasStartedGeneration()"
        @hasGenerated="hasGenerated($event)"
        ref="html2Pdf"
    >
        <section slot="pdf-content">
            <p>Hi</p>
        </section>
    </vue-html2pdf>
    </div>
   </div>
</template>

<script>
export default {
  name: ' BuilderCreate',
  data() {
    return {}
  },
  methods: {},
}
</script>
