<template>
  <div class="numberBox" ref="numberBox">
    <span>案件累计</span>
    <div>
      <div class="scrollList">
        <div v-for="(num, index) in scrollNumList" :key="index">{{ num }}</div>
      </div>
    </div>
    <div>
      <div class="scrollList">
        <div v-for="(num, index) in scrollNumList" :key="index">{{ num }}</div>
      </div>
    </div>
    <span>,</span>
    <div>
      <div class="scrollList">
        <div v-for="(num, index) in scrollNumList" :key="index">{{ num }}</div>
      </div>
    </div>
    <div>
      <div class="scrollList">
        <div v-for="(num, index) in scrollNumList" :key="index">{{ num }}</div>
      </div>
    </div>
    <div>
      <div class="scrollList">
        <div v-for="(num, index) in scrollNumList" :key="index">{{ num }}</div>
      </div>
    </div>
    <span>,</span>
    <div>
      <div class="scrollList">
        <div v-for="(num, index) in scrollNumList" :key="index">{{ num }}</div>
      </div>
    </div>
    <div>
      <div class="scrollList">
        <div v-for="(num, index) in scrollNumList" :key="index">{{ num }}</div>
      </div>
    </div>
    <div>
      <div class="scrollList">
        <div v-for="(num, index) in scrollNumList" :key="index">{{ num }}</div>
      </div>
    </div>
    <span>宗</span>
  </div>
  {{ numberVal }}
</template>

<script setup>
import { onMounted, ref, watch } from "vue";

// 接收该自定义属性来获取父组件期望修改的值，该值切换则组件上数字就切换
const props = defineProps({
  numberVal: Number,
});

const numberBoxEle = ref(null);
const scrollNumList = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];// 用于渲染
// 获取每个scrollList的DOM元素
const scrollListEle = ref(null);
onMounted(() => {
  numberBoxEle.value = document.querySelector(".numberBox");
  scrollListEle.value = document.querySelectorAll(".scrollList");
  // 通过监听props.numberVal的改变来实现组件上数字的切换
  watch(
    () => props.numberVal,
    () => {
      checkNumChange();
    },
    { immediate: true }
  );
});


/**
 * 
 * @param {Number} index 屏幕上8位显示的索引
 * @param {Number} num 目标位置希望改动为多少的目标值
 */
const scrollNum = function (index, num) {
  let top = -num * 40;// 40是容纳div的高度
  scrollListEle.value[index].style.top = top + "px";
};

// 改变画面上的数字
const checkNumChange = function () {
  let numberStr = props.numberVal + "";
  let countDiff = 8 - numberStr.length;
  // 对接受的数字进行8位补齐
  for (let i = 0; i < countDiff; i++) {
    numberStr = 0 + numberStr;
  }
  // 调用scrollNum实现对应位置数字的改变
  for (let i = 0; i < 8; i++) {
    scrollNum(i, +numberStr[i]);
  }
};
</script>

<style scope>
.numberBox {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 50px;
  width: 500px;
  background-color: #020b44;
}
.numberBox > div {
  width: 30px;
  height: 40px;
  margin: 10px 5px;
  border: 2px solid #5d708f;
  border-radius: 5%;
  background-color: #0b2160;
  color: #e49449;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 25px;
  position: relative;
  overflow: hidden;
}

.scrollList {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  position: absolute;
  transition: 1.5s;
  top: -120px;
}

.scrollList > div {
  width: 30px;
  height: 40px;
  display: flex;
  justify-content: center;
  align-items: center;
}
span {
  color: #ffffff;
}
</style>
