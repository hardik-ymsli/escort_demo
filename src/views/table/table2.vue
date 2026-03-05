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

import {
  CONST_SYSTEM_DATE_FORMAT
} from "@/constants";
import {
  CONST_SYSTEM_DATE_VALUE_FORMAT
} from "@/constants";

const {
  t
} = useI18n();
const lockScreenUtils = useLockScreen();
const lockScreen = lockScreenUtils.lockScreen;

defineOptions({
  name: 'table2',
});

const form = ref();
const btn = ref();
const table = ref();
const deleteBtn = ref();
const saveBtn = ref();
const addBtn = ref();

const formData = reactive({});

const tableEditConfig = reactive({
  trigger: 'click'

});

const tableMouseConfig = reactive({

  extension: true

});

const tableRowConfig = reactive({
  isCurrent: true,
});

const employeeDataSetApi = useApi({
  method: 'post',
  localData: [{
      "employeeId": "EMP001",
      "firstName": "Hardik",
      "lastName": "Gupta",
      "gender": "Male",
      "dob": "1999-04-12",
      "age": 26
    },
    {
      "employeeId": "EMP002",
      "firstName": "Rahul",
      "lastName": "Sharma",
      "gender": "Male",
      "dob": "1997-08-21",
      "age": 28
    },
    {
      "employeeId": "EMP003",
      "firstName": "Priya",
      "lastName": "Verma",
      "gender": "Female",
      "dob": "2000-01-15",
      "age": 25
    },
    {
      "employeeId": "EMP004",
      "firstName": "Aman",
      "lastName": "Singh",
      "gender": "Male",
      "dob": "1998-11-05",
      "age": 27
    },
    {
      "employeeId": "EMP005",
      "firstName": "Neha",
      "lastName": "Kumar",
      "gender": "Female",
      "dob": "2001-06-30",
      "age": 24
    }
  ],

}, {
  manual: true,
});
const employeeDataSet = employeeDataSetApi.data;

const btnClick = () => {
  retriveData();
};

const tableEmployeeIdEditRender = computed(() => {
  return {
    enabled: true,
    defaultValue: 'Ymsli358',
  };
});

const tableFirstNameEditRender = computed(() => {
  return {
    enabled: true,
    attrs: {

      maxlength: 50,
      uppercase: true,

    },
  };
});

const tableLastNameEditRender = computed(() => {
  return {
    enabled: true,
    attrs: {

      maxlength: 50,
      uppercase: true,

    },
  };
});

const tableGenderEditRender = computed(() => {
  return {
    enabled: true,
    defaultValue: 'M',
    attrs: {

      activeText: 'Female',
      inactiveText: 'Male',
      activeValue: 'F',
      inactiveValue: 'M',

    },
  };
});

const tableDobEditRender = computed(() => {
  return {
    enabled: true,
    attrs: {

      valueFormat: CONST_SYSTEM_DATE_VALUE_FORMAT.yyyymmdd,
      format: CONST_SYSTEM_DATE_FORMAT.ddmmyyyy,

    },
  };
});

const tableAgeEditRender = computed(() => {
  return {
    enabled: true,
    attrs: {

      min: 0,
      max: 200,
      step: 1,
      stepStrictly: true,
      controls: true,

    },
  };
});

const deleteBtnClick = () => {
  onDeleteRow();

};
const saveBtnClick = () => {
  onSaveRow();
};
const addBtnClick = () => {
  onAddRow();
};

function retriveData() {
  employeeDataSetApi.runAsync();
}

function onAddRow() {

  //table id
  let newRow = {
    "dob": "1999-04-12",
    "age": 0
  }
  table.value.insertAt(newRow, -1);
}

function onDeleteRow() {

  //first get current row which you are selected 
  let selectedRow = table.value.getCurrentRecord();
  table.value.remove(selectedRow);

}

function onSaveRow() {
  console.log(table.value.getTableData().visibleData);
}
</script>

<template>
  <VueForm ref="form" :model="formData" v-loading="lockScreen">
    <VueButton icon-position="left" id="btn" ref="btn" @click="btnClick">
      retrive
    </VueButton>


    <VueTable :show-header="true" id="table" ref="table" :data="employeeDataSet" :edit-config="tableEditConfig" :mouse-config="tableMouseConfig" :row-config="tableRowConfig">

      <VueIndexColumn align="center" width="50px" min-width="50px" header-align="center" />

      <VueInputColumn :edit-render="tableEmployeeIdEditRender" field="employeeId" width="200px" title="EmployeeId">


      </VueInputColumn>
      <VueInputColumn :edit-render="tableFirstNameEditRender" field="firstName" width="200px" :title="t('label.firstName')" header-align="center">


      </VueInputColumn>
      <VueInputColumn :edit-render="tableLastNameEditRender" field="lastName" width="200px" :title="t('label.lastName')" header-align="center">


      </VueInputColumn>

      <VueSwitchColumn :edit-render="tableGenderEditRender" field="gender" width="200px" :title="t('label.gender')">
      </VueSwitchColumn>
      <VueDateTimeColumn :edit-render="tableDobEditRender" field="dob" width="200px" :title="t('label.dob')">
      </VueDateTimeColumn>
      <VueNumberColumn :edit-render="tableAgeEditRender" field="age" :min="0" :max="200" :step="1" :step-strictly="true" :title="t('label.age')" width="100px" header-align="center">
      </VueNumberColumn>

    </VueTable>

    <VueButton icon-position="left" id="deleteBtn" ref="deleteBtn" @click="deleteBtnClick">
      delete
    </VueButton>
    <VueButton icon-position="left" id="saveBtn" ref="saveBtn" @click="saveBtnClick">
      Save
    </VueButton>
    <VueButton icon-position="left" id="addBtn" ref="addBtn" @click="addBtnClick">
      Add
    </VueButton>


  </VueForm>
</template>