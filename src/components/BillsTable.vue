<template>
  <table class="table">
    <thead class="bg-blue-400 text-white">
      <tr>
        <th
          scope="col"
          class="py-1 px-3"
        >
          Date
        </th>
        <th
          scope="col"
          class="py-1 px-3"
        >
          Amount
        </th>
        <th
          scope="col"
          class="py-1 px-3"
        >
          Category
        </th>
        <th
          scope="col"
        ></th>
      </tr>
    </thead>
    <tbody>
      <tr class="p-4 bg-blue-100 text-center">
        <td colspan="4">
          <button
            class="py-1 px-3 underline text-gray-700"
            @click="triggerShowAddBill"
          >
            Add new
          </button>
        </td>
      </tr>
      <tr
        v-for="(bill, index) in bills"
        :key="index"
        class="p-4"
      >
        <td class="py-1 px-3 text-gray-700">{{ bill.date | moment('MMM D, YYYY') }}</td>
        <td class="py-1 px-3 text-gray-700">${{ bill.amount }}</td>
        <td class="py-1 px-3 text-gray-700">{{ bill.category }}</td>
        <td class="py-1 px-3">
          <button
            class="py-1 px-3 text-gray-700"
            @click="removeBill(index)"
          >
            &times;
          </button>
        </td>
      </tr>
    </tbody>
  </table>
</template>

<script>
  export default {
    name: 'BillsTable',
    props: ['bills'],
    methods: {
      triggerShowAddBill() {
        this.$emit('triggerShowAddBill');
      },
      removeBill(index) {
        this.$emit('removeBill', index);
      }
    }
  };
</script>
