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

const nameList = ref([])
const emit = defineEmits(['onClearFullName', 'onSelectFullName'])

defineOptions({
  name: 'chi',
});

const form = ref();
const fullNames = ref();
const addBtn = ref();

const formData = reactive({
  fullName: ''
});

const fullNamesProps = computed(() => {
  return {
    label: 'fullName',
    value: 'fullName',

  }
});

const fullNamesChange = (val, option, oldVal, oldOption) => {
  emit('onSelectFullName', val)
};

const addBtnClick = () => {
  addValueToList();
}

;

function addValueToList() {
  nameList.value.push({
    fullName: props.fullName
  })

  emit('onClearFullName')
}
</script>

<template>
  <VueForm ref="form" :model="formData" v-loading="lockScreen">

    <VueFormItem label="FullNames" prop="fullName">
      <VueSelect id="fullNames" ref="fullNames" v-model="formData.fullName" @change="fullNamesChange" :options="nameList" :props="fullNamesProps">


      </VueSelect>
    </VueFormItem>

    <VueButton icon-position="left" id="addBtn" ref="addBtn" @click="addBtnClick">
      Add
    </VueButton>


  </VueForm>
</template>