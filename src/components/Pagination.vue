<template>
  <div class="pagination">
      <button class="previousNextBtn" @click="handlePrevious" :disabled="currentPage === 1">Previous</button>
      <button class="btnPerPage" v-for="page in totalPages" :key="page" @click="handleGoToPage(page)" :class="{ active: currentPage === page }">{{ page }}</button>
      <button class="previousNextBtn" @click="handleNext" :disabled="currentPage === totalPages">Next</button>
    </div>
</template>

<script setup>
defineProps(['currentPage','totalPages'])
const emit = defineEmits(["previous", "next", "goToP"]);
const handlePrevious = () => {
  emit("previous");
};
const handleNext = () => {
  emit("next");
};
const handleGoToPage = (page) => {
  emit("goToP", page);
};
</script>

<style scoped>
.pagination{
  margin-top: 10px;
  padding: 8px;
  display: flex;
  justify-content: center;
  gap: 5px;
}
.previousNextBtn{
  background-color: #00A372;
  padding: 8px;
  border: 0;
  border-radius: 5px;
  color: #fff;
  font-size: 12px;
  font-weight: 600;
  cursor: pointer;
}
.btnPerPage{
  background-color: #37a484;
  padding: 8px;
  width: 35px;
  height: 35px;
  border: 0;
  border-radius: 50%;
  color: #fff;
  font-size: 12px;
  font-weight: 600;
  cursor: pointer;
}
</style>
