<template>
  <input
    type="tel"
    :maxlength="6"
    ref="code"
    id="code"
    :autofocus="true"
    autocomplete="off"
    v-model="codeValue"
    @blur="inputFocus = false"
    @focus="inputFocus = true"
    @input="submit"
  />
  <label
    for="code"
    class="label-center"
    v-for="(item, index) in inputLen"
    :key="index"
    :class="{
      active: index == codeValue.length && inputFocus,
      activeBorder: index == codeValue.length && inputFocus,
    }"
  >
    {{ codeValue[index] }}
  </label>
</template>

<script setup lang="ts">
import { ref, defineProps, toRefs, Ref, defineEmits } from 'vue';

let props = defineProps({
  inputLen: {
    type: Number,
    required: true,
  },
});
let { inputLen } = toRefs(props);

//声明输入框的值
let codeValue: Ref<string> = ref('');
//定义输入框是否聚焦
let inputFocus: Ref<boolean> = ref(false);
//定义一个事件把输入框的值传给父组件
let emit = defineEmits(['getCode']);

let submit = function () {
  if (codeValue.value.length == inputLen.value) {
    emit('getCode', codeValue.value);
  }
};
</script>

<style>
input {
  width: 40px;
  opacity: 0;
}
.label-center {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 40px;
  height: 60px;
  border: 1px solid #d8d8d8;
  background-color: #fff;
  border-radius: 10px;
  cursor: pointer;
  margin: 0 10px;
}
.active::after {
  content: '';
  display: inline-block;
  height: 60%;
  width: 2px;
  background: #313131;
  animation: 0.8s animate infinite;
}

.activeBorder {
  border: 1px solid black;
}

@keyframes animate {
  100% {
    opacity: 0;
  }
}
</style>
