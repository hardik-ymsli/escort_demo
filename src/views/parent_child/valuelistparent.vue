<script setup>
import {
  useLockScreen,
} from 'viy-ui';
import {
  useI18n
} from 'vue-i18n';

import categoryPopupComp from '/src/views/parent_child/valuelistchild.vue';

const {
  t
} = useI18n();
const lockScreenUtils = useLockScreen();
const lockScreen = lockScreenUtils.lockScreen;

defineOptions({
  name: 'valuelistparent',
});

const form = ref();
const category = ref();

const formData = reactive({
  category: ''
});
</script>

<template>
  <VueForm ref="form" :model="formData" v-loading="lockScreen">

    <VueFormItem label="Category" prop="category">
      <VueValueList popup-type="dialog" dialog-width="500px" :use-popup="true" id="category" ref="category" v-model="formData.category" :popup-component="categoryPopupComp">

      </VueValueList>
    </VueFormItem>


  </VueForm>
</template>