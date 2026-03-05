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

defineOptions({
  name: 'table1',
});

const form = ref();
const demotable = ref();

const formData = reactive({});

const demotableEditConfig = reactive({
  trigger: 'click'

});

const demotableMouseConfig = reactive({

  extension: true

});

const demotableFirstNameEditRender = computed(() => {
  return {
    enabled: false,
  };
});
</script>

<template>
  <VueForm ref="form" :model="formData" v-loading="lockScreen">


    <VueTable id="demotable" ref="demotable" :edit-config="demotableEditConfig" :mouse-config="demotableMouseConfig">

      <VueIndexColumn align="center" width="50px" min-width="50px" header-align="center" title="S.No." />

      <VueInputColumn :edit-render="demotableFirstNameEditRender" field="firstName" :resizable="false" width="200px" title="First Name">


      </VueInputColumn>

    </VueTable>


  </VueForm>
</template>