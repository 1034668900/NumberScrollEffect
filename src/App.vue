<script setup>
import { ref } from 'vue';
import DigitalScroll from './components/DigitalScroll.vue';

const inputVal = ref(10)
// 通过改变inputVal即可改变DigitalScroll组件的数字
window.changeNum = function(num){
    inputVal.value = num
}

</script>

<template>
 <div class="digital">
  <DigitalScroll  :numberVal="inputVal"></DigitalScroll>
 </div>
</template>
<style>
*{
    margin: 0;
    padding: 0;
}

</style>
