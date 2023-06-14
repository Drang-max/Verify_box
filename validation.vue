<template>
  <div class="container">
    <valiInput :inputLen="inputLen" @getCode="getCode"></valiInput>
  </div>
</template>
<script setup lang="ts">
import valiInput from '@/components/valiInput.vue';

import { Ref, ref } from 'vue';

//定义输入框的长度
let inputLen: Ref<number> = ref(4);

let getCode = (code: any) => {
  console.log(code);
};
</script>

<style lang="scss">
.container {
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
