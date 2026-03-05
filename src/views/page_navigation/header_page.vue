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

const router = useRouter();

onMounted(() => {
  console.log("Mounted : headerPage")
})

onUnmounted(() => {
  console.log("UnMounted : headerPage")
})

defineOptions({
  name: 'header_page',
});

const form = ref();
const btnDetail = ref();
const closeBtn = ref();
const btn2 = ref();
const refresh = ref();
const clseDetailTab = ref();
const openBtnDetailTag = ref();
const viy2CodeInput_NWppR = ref();
const viy2InputBox_OibG5 = ref();

const formData = reactive({
  datafieldviy2CodeInput_NWppR: '',
  datafieldviy2InputBox_OibG5: ''
});

const btnDetailClick = () => {
  openDetailPage();
};
const closeBtnClick = () => {
  closeCurrentTag();
};
const btn2Click = () => {
  openNonActiveTag();
};
const refreshClick = () => {
  refreshCurrentTag();
};
const clseDetailTabClick = () => {
  closeDetailPage();
};
const openBtnDetailTagClick = () => {
  openDetailOnSameTag();
};

function openDetailPage() {
  router.push('detail')
}

//it is use for just not focuse the another non active tag
function openNonActiveTag() {
  useMultiTags().openTag({
    name: 'detail'
  })

  //  router.push('detail')

}

function closeCurrentTag() {

  //it will use to close the current page and navigate to another page
  useMultiTags().closeTag();
  router.push('/')
}

function refreshCurrentTag() {
  useMultiTags().refreshCurrent();
}

function openDetailOnSameTag() {
  useMultiTags().updateTag({
    name: 'detail'
  });

  router.push({
    name: 'detail'
  });

  useMultiTags().removeTagCache({
    name: 'header_page'
  });

}

// async function closeDetailPage(){
//   await  useMultiTags.closeTag({
//         name: 'detail'
//     });
// }
</script>

<template>
  <VueForm ref="form" :model="formData" v-loading="lockScreen">
    <VueButton icon-position="left" id="btnDetail" ref="btnDetail" @click="btnDetailClick">
      open Detail Page
    </VueButton>
    <VueButton icon-position="left" id="closeBtn" ref="closeBtn" @click="closeBtnClick">
      Close Current Tag
    </VueButton>
    <VueButton icon-position="left" id="btn2" ref="btn2" @click="btn2Click">
      open no active tag
    </VueButton>
    <VueButton icon-position="left" id="refresh" ref="refresh" @click="refreshClick">
      Refresh Me
    </VueButton>
    <VueButton icon-position="left" id="clseDetailTab" ref="clseDetailTab" @click="clseDetailTabClick">
      close the detail Tab
    </VueButton>
    <VueButton icon-position="left" id="openBtnDetailTag" ref="openBtnDetailTag" @click="openBtnDetailTagClick">
      open Detail Tag on Same Tag
    </VueButton>

    <VueFormItem label="Name" prop="datafieldviy2CodeInput_NWppR">
      <VueCodeInput id="viy2CodeInput_NWppR" ref="viy2CodeInput_NWppR" v-model="formData.datafieldviy2CodeInput_NWppR" />
    </VueFormItem>


    <VueFormItem label="Age" prop="datafieldviy2InputBox_OibG5">
      <VueInput data-type="string" id="viy2InputBox_OibG5" ref="viy2InputBox_OibG5" v-model="formData.datafieldviy2InputBox_OibG5">


      </VueInput>
    </VueFormItem>


  </VueForm>
</template>