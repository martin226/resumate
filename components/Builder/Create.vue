<template>
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
