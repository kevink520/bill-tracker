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
          :activeCategory="activeCategory"
          @triggerShowAddCategory="triggerShowAddCategory"
          @clearActiveCategory="clearActiveCategory"
          @setActiveCategory="setActiveCategory"
        />
        <div class="container flex p-6">
          <div class="w-1/2">
            <BillsTable
              :bills="activeBills"
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
      shouldShowAddBill: false,
      activeCategory: '',
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
    },
    clearActiveCategory() {
      this.activeCategory = '';
    },
    setActiveCategory(category) {
      this.activeCategory = category;
    },
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

    this.shouldShowAddCategory = this.bills.length === 0 && this.categories.length === 0;
  },
  computed: {
    activeBills() {
      return this.bills.filter(bill => this.activeCategory ? bill.category === this.activeCategory : true)
        .sort((a, b) => new Date(a.date) < new Date(b.date) ? 1 : -1);
    },
  },
};
</script>
