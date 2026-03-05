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

const props = defineProps(['fullName']);
const nameList = ref([]); //empty array to just fetching the data to show on the select field

//define the event emittor
//emit name should be same as the filed in it

const emit = defineEmits(['clearFullName', 'selectFullName'])

defineOptions({
  name: 'child2',
});

const form = ref();
const nameDropDown = ref();
const addBtn = ref();

const formData = reactive({
  nameDropDown: ''
});

const nameDropDownProps = computed(() => {
  return {
    label: 'fullName',
    value: 'fullName',

  }
});

const nameDropDownChange = (val, option, oldVal, oldOption) => {
  emit('selectFullName', val)
};

const addBtnClick = () => {
  addValuetoList();
};

function addValuetoList() {
  nameList.value.push({
    fullName: props.fullName
  });
  //then i have to pass the event to just clear the data from the fullName filed
  emit('clearFullName')
}
</script>

<template>
  <VueForm ref="form" :model="formData" v-loading="lockScreen">

    <VueFormItem label="FullNames" prop="nameDropDown">
      <VueSelect id="nameDropDown" ref="nameDropDown" v-model="formData.nameDropDown" @change="nameDropDownChange" :options="nameList" :props="nameDropDownProps">


      </VueSelect>
    </VueFormItem>

    <VueButton icon-position="left" id="addBtn" ref="addBtn" @click="addBtnClick">
      AddValuetoList
    </VueButton>


  </VueForm>
</template>