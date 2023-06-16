<template>
<tr class="productRow" >
        <td>{{ product.id }}</td>
        <td>{{ product.title }}</td>
        <td>{{ product.rating }}</td>
        <td>{{ product.price }}</td>

        <td>
          <button @click="toggleDetails(product.id)" class="btn" :class="{'btnShow':!showtoggle, 'btnHidde':showtoggle}">
          <span v-if="showtoggle"> Hide Details</span>
              <span v-else> Show Details</span>
            </button></td>
   </tr>

   <tr >
    <td colspan="5"  :class="{'open-details': showtoggle, 'close-details': !showtoggle}"  v-if="showtoggle">
       <Details :id="singleProductId" />
    </td>
    </tr>
</template>

<script setup>
import Details from './Details.vue';
import { ref } from 'vue';

    const props = defineProps(["product"])
    const showtoggle = ref(false)
    const singleProductId = ref(null)
    const toggleDetails = (id)=> {
        if(props.product?.id === id){
            showtoggle.value = !showtoggle.value
        }
       singleProductId.value = id
        }
</script>

<style  scoped>
.productRow td{
  font-size: 12.5px;
  padding: 8px;
  font-weight: 500;
  text-align: center;

}

tr:nth-child(even){background-color: #f2f2f2;}

tr:hover {background-color: #faeeeec7;}
tr:first-child {
  border-bottom-left-radius: 8px;
  
}
tr:last-child {
  border-bottom-right-radius: 8px;
}
 
.btn {
  padding: 8px;
  border: 0;
  border-radius: 5px;
  color: #fff;
  font-size: 12px;
  font-weight: 600;
  cursor: pointer;
}

.btnShow{
  background-color: #00A372;
}

.btnHidde{
  background-color: #CA241D;
}
 td[colspan="5"] {
    text-align: none;
      padding: 16px;
      background-color: #eeeeee6a;
      color: black;
      border-bottom: none;
      height: 0;
      opacity: 0;
      overflow: hidden;
      transition: height 0.3s ease-in-out, opacity 0.3s ease-in-out;
      margin: 0 auto;
      overflow: hidden;
      transform-origin: top center; 
      font-size: 14px;
      line-height: 1.5;
    }

    .open-details {
      animation-name: openDetails;
      animation-duration: 0.2s;
      animation-timing-function: cubic-bezier(0.6, -0.28, 0.735, 0.045);
      animation-fill-mode: forwards;
    }

    @keyframes openDetails {
      0% {
        height: 0;
        opacity: 0;
        transform: scaleY(0);
      }

      100% {
        height: auto;
        opacity: 1;
        transform: scaleY(1);
      }
    }

    .close-details {
      animation-name: closeDetails;
      animation-duration: 0.5s;
      animation-timing-function: cubic-bezier(0.6, -0.28, 0.735, 0.045);
      animation-fill-mode: forwards;
    }

    @keyframes closeDetails {
      0% {
        height: auto;
        opacity: 1;
        transform: scaleY(1);
      }

      100% {
        height: 0;
        opacity: 0;
        transform: scaleY(0);
      }
    }

</style>