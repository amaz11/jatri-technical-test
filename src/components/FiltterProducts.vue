<template>
  <label for="Price">{{ name }}:</label>
  <select class="inputBox" :value="value" @input="handelInput">
    <option value="ascending">Ascending</option>
    <option value="descending">Descending</option>
  </select>
</template>

<script setup>
defineProps(["name", "value"]);

const emit = defineEmits(["update:value"]);
const handelInput = (e)=>{
    emit('update:value', e.target.value)
}
</script>

<style scoped>
.inputBox{
    padding: 5px 20px;
    border: .5px solid rgb(187, 187, 187) ;
    border-radius: 5px; 
}
.inputBox:focus{
    outline: 0;
}
</style>
