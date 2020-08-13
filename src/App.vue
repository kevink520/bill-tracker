<template>
  <main>
    <AddCategory
      v-if="shouldShowAddCategory"
      @addCategory="addCategory"
    />
    <div v-else>
      <AddBill
        v-if="shouldShowAddBill"
	:categories="categories"
        @addBill="addBill"
      />
      <div v-else>
        <NavBar
          :categories="categories"
          @triggerShowAddCategory="triggerShowAddCategory"
        />
        <div class="container flex">
          <div class="w-1/2">
            <BillsTable
              :bills="bills"
              @triggerShowAddBill="triggerShowAddBill"
              @removeBill="removeBill"
            />
          </div>
          <div clasd="w-1/2">
            <Chart :bills="activeBills" />
          </div>
	</div>
      </div>
    </div>
  </main>
</template>

<script>
import Vue from 'vue';
import AddCategory from './components/AddCategory';
import AddBill from './components/AddBill';
import NavBar from './components/NavBar';
import Chart from './components/Chart';
import BillsTable from './components/BillsTable';
Vue.use(require('vue-moment'));

export default {
  name: 'App',
  components: {
    AddCategory,
    AddBill,
    NavBar,
    Chart,
    BillsTable
  },
  data() {
    return {
      bills: [],
      categories: [],
      shouldShowAddCategory: true,
      shouldShowAddBill: false
    };
  },
  methods: {
    addCategory(category) {
      this.categories.push(category);
      this.shouldShowAddCategory = false;
    },
    triggerShowAddCategory() {
      this.shouldShowAddCategory = true;
    },
    addBill(bill) {
      this.bills.push(bill);
      this.shouldShowAddBill = false;
    },
    triggerShowAddBill() {
      this.shouldShowAddBill = true;
    },
    removeBill(index) {
      this.bills = this.bills.slice(0, index).concat(this.bills.slice(index + 1));
    }
  },
  watch: {
    bills() {
      localStorage.setItem('bills', JSON.stringify(this.bills));
    },
    categories() {
      localStorage.setItem('categories', JSON.stringify(this.categories));
    }
  },
  mounted() {
    if (localStorage.getItem('bills')) {
      this.bills = JSON.parse(localStorage.getItem('bills'));
    }

    if (localStorage.getItem('categories')) {
      this.categories = JSON.parse(localStorage.getItem('categories'));
    }

    if (this.bills.length === 0 && this.categories.length === 0) {
      this.shouldShowAddCategory = true;
    }
  }
};
</script>
