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

defineOptions({
  name: 'first_page',
});

const form = ref();
const Demo = ref();

const formData = reactive({
  Demo: ''
});
</script>

<template>
  <VueForm ref="form" :model="formData" v-loading="lockScreen">


    <VueFormItem label="Demo" prop="Demo">
      <VueInput data-type="string" id="Demo" ref="Demo" v-model="formData.Demo">


      </VueInput>
    </VueFormItem>


  </VueForm>
</template>