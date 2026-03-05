<script setup>
import {
  useLockScreen,
} from 'viy-ui';
import {
  useI18n
} from 'vue-i18n';

import childSubPagePage from '/src/views/parent_child2/child.vue';

const {
  t
} = useI18n();
const lockScreenUtils = useLockScreen();
const lockScreen = lockScreenUtils.lockScreen;

defineOptions({
  name: 'parent',
});

const form = ref();
const parentInput = ref();
const childSubPage = ref();

const formData = reactive({
  parentInput: ''
});

function childValueCaptured(event) {
  console.log(event)
}
</script>

<template>
  <VueForm ref="form" :model="formData" v-loading="lockScreen">


    <VueFormItem label="Parent Input" prop="parentInput">
      <VueInput data-type="string" id="parentInput" ref="parentInput" v-model="formData.parentInput">


      </VueInput>
    </VueFormItem>

    <childSubPagePage lastName="Hardik" :parentValue="formData.parentInput" @onChildInput="childValueCaptured" id="childSubPage" ref="childSubPage" />


  </VueForm>
</template>