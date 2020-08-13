<template>
  <div class="h-100 w-full flex items-center justify-center font-sans">
    <div class="bg-white rounded shadow p-6 m-4 w-full lg:w-3/4 lg:max-w-lg">
      <div class="mb-4">
        <h1 class="text-gray-700">Enter a category of bills</h1>
        <p class="text-gray-700">E.g. 'Electricity' or 'Gas' or 'Internet'</p>
        <div class="flex mt-4">
          <input
            class="shadow appearance-none border rounded w-full py-2 px-3 mr-4 text-gray-700"
            placeholder="Add category"
            v-model="category"
          />
          <button
            class="flex-no-shrink p-2 border-2 rounded bg-teal-700 text-white border-teal-700 hover:text-white hover:bg-teal-900 hover:border-teal-900"
            @click="handleClick"
          >
            Add
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'AddCategory',
  data() {
    return {
      category: ''
    };
  },
  methods: {
    handleClick() {
      if (!this.category) {
        alert('Enter a category');
        return;
      }

      this.$emit('addCategory', this.category);
    }
  }
}
</script>
