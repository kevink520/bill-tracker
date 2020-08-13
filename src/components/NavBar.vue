<template>
  <ul class="list-reset flex flex-wrap justify-center mb-0 bg-gray-100">
    <li
      class="top-menu-item text-gray-700"
      :class="activeCategory === '' ? 'bg-gray-400' : 'bg-gray-100'"
      @click="clearActiveCategory"
    >
      All
    </li>
    <li
      class="top-menu-item text-gray-700"
      :class="activeCategory === category ? 'bg-gray-400' : 'bg-gray-100'"
      v-for="category in categories"
      :key="category"
      @click="setActiveCategory(category)"
    >
      {{category}}
    </li>
    <li
      class="top-menu-item text-gray-700"
      @click="triggerShowAddCategory"
    >
      +
    </li>
  </ul>
</template>

<script>
export default {
  props: ['categories', 'activeCategory'],
  methods: {
    triggerShowAddCategory() {
      this.$emit('triggerShowAddCategory');
    },
    clearActiveCategory() {
      this.$emit('clearActiveCategory');
    },
    setActiveCategory(category) {
      this.$emit('setActiveCategory', category);
    },
  },
};
</script>

<style>
.top-menu-item {
  @apply .p-4 .inline .uppercase .tracking-wider .cursor-pointer;
}
.top-menu-item:hover {
  @apply .bg-gray-400;
}
</style>
