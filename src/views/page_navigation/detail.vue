<script setup>
import {
  useLockScreen,
} from 'viy-ui';
import {
  useI18n
} from 'vue-i18n';

const {
  t
} = useI18n();
const lockScreenUtils = useLockScreen();
const lockScreen = lockScreenUtils.lockScreen;

onMounted(() => {
  console.log("Mounted : DetailPage")
})

onUnmounted(() => {
  console.log("UnMounted : DetailPage")
})

defineOptions({
  name: 'detail',
});

const form = ref();

const formData = reactive({});
</script>

<template>
  <VueForm ref="form" :model="formData" v-loading="lockScreen">


  </VueForm>
</template>