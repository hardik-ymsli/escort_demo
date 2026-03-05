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

//here we define the props or the properties in which we define the name of the props inside the square bracket
//which we getting the data from the parent and acess by this props name 
const props = defineProps(['lastName', 'parentValue'])

const emit = defineEmits(['onChildInput'])

defineOptions({
  name: 'child',
});

const form = ref();
const childInput = ref();
const getBtn = ref();
const setBtn = ref();

const formData = reactive({
  childInput: ''
});

const getBtnClick = () => {
  getValueFromParent();
};
const setBtnClick = () => {
  setValueFromChildToParent();
};

function getValueFromParent() {
  console.log(props)
  console.log(props.lastName)
  console.log(props.parentValue)
}

function setValueFromChildToParent() {
  emit('onChildInput', formData.childInput)
}
</script>

<template>
  <VueForm ref="form" :model="formData" v-loading="lockScreen">


    <VueFormItem label="Child Input" prop="childInput">
      <VueInput data-type="string" id="childInput" ref="childInput" v-model="formData.childInput">


      </VueInput>
    </VueFormItem>

    <VueButton icon-position="left" id="getBtn" ref="getBtn" @click="getBtnClick">
      get Value From Parent
    </VueButton>
    <VueButton icon-position="left" id="setBtn" ref="setBtn" @click="setBtnClick">
      from child to parent
    </VueButton>


  </VueForm>
</template>