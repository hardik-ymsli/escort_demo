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

const props = defineProps(['lastName', 'parentInput'])
const emit = defineEmits(['onChildInput'])

defineOptions({
  name: 'child_page',
});

const form = ref();
const ChildInput = ref();
const Btn = ref();
const setBtn = ref();

const formData = reactive({
  ChildInput: ''
});

const BtnClick = () => {
  doSome();
};
const setBtnClick = () => {
  emitValueToParent();
};

function doSome() {

  // console.log(lastName)
  console.log(props)
  console.log(props.lastName)
  console.log(props.parentInput)

}

function emitValueToParent() {
  emit('onChildInput', formData.ChildInput)
}
</script>

<template>
  <VueForm ref="form" :model="formData" v-loading="lockScreen">


    <VueFormItem label="Child Input" prop="ChildInput">
      <VueInput data-type="string" id="ChildInput" ref="ChildInput" v-model="formData.ChildInput">


      </VueInput>
    </VueFormItem>

    <VueButton icon-position="left" id="Btn" ref="Btn" @click="BtnClick">
      gettingValueFromParent
    </VueButton>
    <VueButton icon-position="left" id="setBtn" ref="setBtn" @click="setBtnClick">
      emitValueToParent
    </VueButton>


  </VueForm>
</template>