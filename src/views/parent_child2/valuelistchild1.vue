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

const emit = defineEmits(['select']);

defineOptions({
  name: 'valuelistchild1',
});

const form = ref();
const fullNameTable = ref();
const btn = ref();

const formData = reactive({});

const fullNameTableEditConfig = reactive({
  trigger: 'click'

});

const fullNameTableMouseConfig = reactive({

  extension: true

});

const fullNameTableRowConfig = reactive({
  isCurrent: true,
});

const fullNamesDataSetApi = useApi({
  method: 'post',
  localData: [{
      firstName: 'Hardik',
      lastName: 'Gupta'
    },
    {
      firstName: 'Rahul',
      lastName: 'Sharma'
    }
  ],

});
const fullNamesDataSet = fullNamesDataSetApi.data;

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

const btnClick = () => {
  setSelectedData();
};

function setSelectedData() {

  let selectRecord = fullNameTable.value.getCurrentRecord();

  // alert(selectRecord.firstName + " " + selectRecord.lastName);

  emit('select', selectRecord)
}
</script>

<template>
  <VueForm ref="form" :model="formData" v-loading="lockScreen">


    <VueTable :stripe="true" :border="true" :show-header="true" :show-footer="true" id="fullNameTable" ref="fullNameTable" :data="fullNamesDataSet" :edit-config="fullNameTableEditConfig" :mouse-config="fullNameTableMouseConfig" :row-config="fullNameTableRowConfig">
      <VueInputColumn :edit-render="fullNameTableFirstNameEditRender" field="firstName" width="200px" title="First Name">


      </VueInputColumn>
      <VueInputColumn :edit-render="fullNameTableLastNameEditRender" field="lastName" width="200px" title="Last Name">


      </VueInputColumn>

    </VueTable>

    <VueButton icon-position="left" id="btn" ref="btn" @click="btnClick">
      set
    </VueButton>


  </VueForm>
</template>