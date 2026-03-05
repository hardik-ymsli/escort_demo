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

defineOptions({
  name: 'valuelistchild',
});

const form = ref();
const fullNameTable = ref();
const setBtn = ref();

const formData = reactive({});

const fullNameTableEditConfig = reactive({
  trigger: 'click'

});

const fullNameTableMouseConfig = reactive({

  extension: true

});

const fullNameDataSetApi = useApi({
  method: 'post',
  localData: [{
      firstName: "Hardik",
      lastName: "Gupta"
    },

    {
      firstName: "Hardik",
      lastName: "Rathore"
    },

    {
      firstName: "Hardik",
      lastName: "Mittal"
    },

  ],

});
const fullNameDataSet = fullNameDataSetApi.data;

const fullNameTableFirstNameEditRender = computed(() => {
  return {
    enabled: false,
  };
});

const fullNameTableLastNameEditRender = computed(() => {
  return {
    enabled: false,
  };
});

const setBtnClick = () => {
  setData();
};

function setData() {
  alert("set selected data")
}
</script>

<template>
  <VueForm ref="form" :model="formData" v-loading="lockScreen">


    <VueTable id="fullNameTable" ref="fullNameTable" :data="fullNameDataSet" :edit-config="fullNameTableEditConfig" :mouse-config="fullNameTableMouseConfig">
      <VueInputColumn :edit-render="fullNameTableFirstNameEditRender" field="firstName" width="200px" title="First Name">


      </VueInputColumn>
      <VueInputColumn :edit-render="fullNameTableLastNameEditRender" field="lastName" width="200px" title="Last Name">


      </VueInputColumn>

    </VueTable>

    <VueButton icon-position="left" id="setBtn" ref="setBtn" @click="setBtnClick">
      Set
    </VueButton>


  </VueForm>
</template>