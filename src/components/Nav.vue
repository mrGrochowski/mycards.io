<template>
  <nav id="bottom-navigation" class="block fixed inset-x-0 bottom-0 z-10 bg-transparent">
    <div id="tabs" class="flex justify-between">
      <a
        href="#"
        class="
          w-full
          focus:text-teal-500
          hover:text-teal-500
          justify-center
          inline-block
          text-center
          pt-2
          pb-1
        "
      >
        <Home class="inline-block mb-1" />
        <span class="tab tab-home block text-xs">Home</span>
      </a>
      <a
        href="#"
        class="
          w-full
          focus:text-teal-500
          hover:text-teal-500
          justify-center
          inline-block
          text-center
          pt-2
          pb-1
        "
      >
        <Category class="inline-block mb-1" />
        <span class="tab tab-kategori block text-xs">Category</span>
      </a>
      <a
        href="#"
        class="
          w-full
          focus:text-teal-500
          hover:text-teal-500
          justify-center
          inline-block
          text-center
          pt-2
          pb-1
        "
      >
        <Compass class="inline-block mb-1" />
        <span class="tab tab-explore block text-xs">Explore</span>
      </a>
    </div>
  </nav>
</template>

<script>
import Home from '../assets/home.svg'
import Category from '../assets/category.svg'
import Compass from '../assets/compass.svg'
export default {
  components: {
    Home,
    Category,
    Compass,
  },
}
</script>
