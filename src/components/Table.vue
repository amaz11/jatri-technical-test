<template>
  <div v-if="products.length">
    <div class="flitter">
      <FiltterProducts
      name="Price"
      :value="priceFilter"
      v-on:update:value="priceFilter = $event"
    />
    <FiltterProducts
      name="Rating"
      :value="ratingFilter"
      v-on:update:value="ratingFilter = $event"
    />
    </div>

    <table>
      <thead>
        <th>SI</th>
        <th>Name</th>
        <th>Rating</th>
        <th>Price</th>
        <th>Action</th>
      </thead>
      <tbody v-for="product in filteredProducts" :key="product.id">
        <TableRow :product="product" />
      </tbody>
   
    </table>
    <Pagination
        :currentPage="currentPage"
        :totalPages="totalPages"
        @previous="previousPage"
        @next="nextPage"
        @goToP="goToPage"
      />
  </div>

  <div class="loaderTable" v-else>
    <Loader/>
  </div>
</template>

<script setup>
import { computed, onMounted, ref } from "vue";
import TableRow from "./TableRow.vue";
import Pagination from "./Pagination.vue";
import FiltterProducts from "./FiltterProducts.vue";
import Loader from "./Loader.vue";

const products = ref([]);
const currentPage = ref(1);
const perPage = ref(5);
const totalItems = ref(0);
const ratingFilter = ref("");
const priceFilter = ref("");

// Data Fetching
onMounted(async () => {
  try {
    const res = await fetch("https://dummyjson.com/products");
    const data = await res.json();
    products.value = data?.products;
    totalItems.value = data?.products.length;
  } catch (error) {
    console.log(error);
  }
});

// Pagination Data
const paginatedData = () => {
  const startIndex = (currentPage.value - 1) * perPage.value;
  const endIndex = startIndex + perPage.value;
  return products.value.slice(startIndex, endIndex);
};

// Total Page
const totalPages = computed(() => {
  return Math.ceil(totalItems.value / perPage.value);
});

// Previous page btn
const previousPage = () => {
  if (currentPage.value > 1) {
    currentPage.value--;
  }
};

// Next page btn
const nextPage = () => {
  if (currentPage.value < totalPages.value) {
    currentPage.value++;
  }
};

// Single page Click
const goToPage = (page) => {
  currentPage.value = page;
};

// Product Filter 
const filteredProducts = computed(() => {
  let filtered = paginatedData();

  if (priceFilter.value === "ascending") {
    filtered = filtered.sort((a, b) => a.price - b.price);
  } else if (priceFilter.value === "descending") {
    filtered = filtered.sort((a, b) => b.price - a.price);
  }

  if (ratingFilter.value === "ascending") {
    filtered = filtered.sort((a, b) => a.rating - b.rating);
  } else if (ratingFilter.value === "descending") {
    filtered = filtered.sort((a, b) => b.rating - a.rating);
  }
  return filtered;
});

</script>

<style scoped>
table {
  border-collapse: collapse;
  width: 100%;
  margin-bottom: 16px;
  margin-top: 15px;
}

th {
  padding-top: 12px;
  padding-bottom: 12px;
  background-color: #ed4836;
  color: white;
  margin: auto;
  text-align: center;
  font-weight: 700;
  font-size: 16px;
}

th:first-child {
  border-top-left-radius: 8px;
}

th:last-child {
  border-top-right-radius: 8px;
}

.flitter{
  display: flex;
  justify-content: flex-end;
  margin-right: 8px;
  gap: 5px;
}

.loaderTable{
  display: flex;
  justify-content: center;
  align-items: center;
  height: 50vh;
}
</style>
