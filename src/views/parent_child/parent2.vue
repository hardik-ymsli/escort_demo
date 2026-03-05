<script setup>
import {
  useLockScreen,
} from 'viy-ui';
import {
  useI18n
} from 'vue-i18n';

import childSubPagePage from '/src/views/parent_child/child2.vue';

const {
  t
} = useI18n();
const lockScreenUtils = useLockScreen();
const lockScreen = lockScreenUtils.lockScreen;

const selectedName = ref("defaultName");

defineOptions({
  name: 'parent2',
});

const form = ref();
const fullName = ref();
const selectedValue = ref();
const childSubPage = ref();

const formData = reactive({
  fullName: ''
});

function functiontoClearName() {

  formData.fullName = ' ';
}

function functiontoSelectFullName(event) {
  selectedName.value = event;

}
</script>

<template>
  <VueForm ref="form" :model="formData" v-loading="lockScreen">


    <VueFormItem label="Full Name" prop="fullName">
      <VueInput data-type="string" id="fullName" ref="fullName" v-model="formData.fullName">


      </VueInput>
    </VueFormItem>

    <VueText id="selectedValue" ref="selectedValue" :style="{ width : '100%', display : 'inline-block', }" v-html="selectedName">
    </VueText>
    <childSubPagePage :fullName="formData.fullName" @clearFullName="functiontoClearName" @selectFullName="functiontoSelectFullName" id="childSubPage" ref="childSubPage" />


  </VueForm>
</template>