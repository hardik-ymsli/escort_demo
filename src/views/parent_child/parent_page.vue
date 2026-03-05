<script setup>
import {
  useLockScreen,
} from 'viy-ui';
import {
  useI18n
} from 'vue-i18n';

import childSubPagePage from '/src/views/parent_child/child_page.vue';

const {
  t
} = useI18n();
const lockScreenUtils = useLockScreen();
const lockScreen = lockScreenUtils.lockScreen;

defineOptions({
  name: 'parent_page',
});

const form = ref();
const ParentInput = ref();
const childSubPage = ref();

const formData = reactive({
  ParentInput: ''
});

function onChildDataCapture(event) {
  console.log(event);
}
</script>

<template>
  <VueForm ref="form" :model="formData" v-loading="lockScreen">


    <VueFormItem label="Parent Input" prop="ParentInput">
      <VueInput data-type="string" id="ParentInput" ref="ParentInput" v-model="formData.ParentInput">


      </VueInput>
    </VueFormItem>

    <childSubPagePage lastName="Hardik" :parentInput="formData.ParentInput" @onChildInput="onChildDataCapture" id="childSubPage" ref="childSubPage" />


  </VueForm>
</template>