<script setup>
import {
  useLockScreen,
} from 'viy-ui';
import {
  useI18n
} from 'vue-i18n';

import childSubPagePage from '/src/views/parent_child2/chi.vue';

const {
  t
} = useI18n();
const lockScreenUtils = useLockScreen();
const lockScreen = lockScreenUtils.lockScreen;

//if we are using primitive data type then we have to use ref other wise for derived datatype we have ti use reactive 
const selectedName = ref("this is the name")

defineOptions({
  name: 'pat',
});

const form = ref();
const fullName = ref();
const text = ref();
const childSubPage = ref();

const formData = reactive({
  fullName: ''
});

function clearFullName() {
  formData.fullName = ''
}

function captureFullName(event) {
  selectedName.value = event

}
</script>

<template>
  <VueForm ref="form" :model="formData" v-loading="lockScreen">


    <VueFormItem label="full Name" prop="fullName">
      <VueInput data-type="string" id="fullName" ref="fullName" v-model="formData.fullName">


      </VueInput>
    </VueFormItem>

    <VueText id="text" ref="text" :style="{ width : '100%', display : 'inline-block', }" v-html="selectedName">
    </VueText>
    <childSubPagePage :fullName="formData.fullName" @onClearFullName="clearFullName" @onSelectFullName="captureFullName" id="childSubPage" ref="childSubPage" />


  </VueForm>
</template>