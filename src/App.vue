<template>
  <main>
    <AddCategory v-if="shouldShowAddCategory" @addCategory="addCategory" />
    <div v-else>
      <NavBar />
      <div class="container flex">
        <div class="w-1/2">
          <BillsTable />
        </div>
        <div clasd="w-1/2">
          <Chart :bills="activeBills" />
        </div>
      </div>
    </div>
  </main>
</template>

<script>
//import Vue from 'vue';

import AddCategory from './components/AddCategory';
//import AddBill from './components/AddBill';
import NavBar from './components/NavBar';
import Chart from './components/Chart';
import BillsTable from './components/BillsTable';

export default {
  name: 'App',
  components: {
    AddCategory,
    //AddBill,
    NavBar,
    Chart,
    BillsTable
  },
  data() {
    return {
      bills: [],
      categories: [],
      shouldShowAddCategory: true
    };
  },
  methods: {
    addCategory(category) {
      this.categories.push(category);
      this.shouldShowAddCategory = false;
    }
  }
};
</script>
