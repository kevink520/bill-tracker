<template>
  <ul class="list-reset inline flex justify-center border-b-4 mb-0">
    <li
      class="top-menu-item" 
      v-for="category in categories"
      :key="category"
    >
      {{category}}
    </li>
    <li
      class="top-menu-item"
      @click="triggerAddShowCategory"
    >
      +
    </li>
  </ul>
</template>

<script>
export default {
  props: ['categories'],
  methods: {
    triggerShowAddCategory() {
      this.$emit('triggerShowAddCategory');
    }
  }
}
</script>

<style>
.top-menu-item {
  @apply .p-4 .inline .bg-gray-200 .uppercase .font-black .cursor-pointer;
}
.top-menu-item:hover {
  @apply .bg-gray-400;
}
</style>
