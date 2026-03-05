<script setup>
import {
  useLockScreen,
} from 'viy-ui';
import {
  useI18n
} from 'vue-i18n';
import {
  useApi
} from '@/composables/useApi';

const {
  t
} = useI18n();
const lockScreenUtils = useLockScreen();
const lockScreen = lockScreenUtils.lockScreen;

function doSome() {
  sampleDataSetApi.runAsync();

}

defineOptions({
  name: 'apicall1',
});

const form = ref();
const sel = ref();
const btn = ref();

const formData = reactive({
  sel: ''
});

const selProps = computed(() => {
  return {
    label: 'id',
    value: 'title',

  }
});

const sampleDataSetApi = useApi({
  url: '/posts',
  method: 'get',

}, {
  onSuccess: (data, params) => {
    VueMessage({
      message: 'congrats to load all the data',
      type: 'success'
    })
    console.log(data);
  },
  manual: true,
});
const sampleDataSet = sampleDataSetApi.data;

const selChange = () => {
  console.log(formData.sel)
};

const btnClick = () => {

  doSome();

};
</script>

<template>
  <VueForm ref="form" :model="formData" v-loading="lockScreen">

    <VueFormItem label="MatchMode" prop="sel">
      <VueSelect id="sel" ref="sel" v-model="formData.sel" @change="selChange" :options="sampleDataSet" :props="selProps">


      </VueSelect>
    </VueFormItem>

    <VueButton icon-position="left" id="btn" ref="btn" @click="btnClick">
      done
    </VueButton>


  </VueForm>
</template>