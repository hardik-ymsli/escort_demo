<script setup>
import {
  useLockScreen,
  IconAddLocation,
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
  name: 'form_1',
});

const form = ref();
const text = ref();
const fname = ref();
const lName = ref();
const age = ref();
const dob = ref();
const hobbies = ref();
const yoe = ref();
const yoeDropDown = ref();
const ta = ref();
const btnset = ref();
const printBtn = ref();

const formData = reactive({
  firstName: '',
  lastName: '',
  age: undefined,
  dob: '',
  hobbies: [],
  yoe: '',
  textarea: ''
});

const rules = reactive({
  fnameRules: [{
      required: true

        ,
      message: computed(() => {
          return t('error.required');
        })

        ,
      trigger: "blur"

    }

  ]

});

const yoeProps = computed(() => {
  return {
    label: 'name',
    value: 'value',

  }
});

const hobbiesDataSetApi = useApi({
  method: 'get',
  localData: [{
      name: 'hockey',
      value: '1'
    },
    {
      name: 'badminton',
      value: '2'
    }

  ],

});
const hobbiesDataSet = hobbiesDataSetApi.data;
const yoeDropDownDataSetApi = useApi({
  method: 'post',
  localData: [{
      text: ' 1'
    },
    {
      text: ' 2'
    },
    {
      text: ' 3'
    },

  ],

});
const yoeDropDownDataSet = yoeDropDownDataSetApi.data;
const yoeDataSetApi = useApi({
  method: 'get',
  localData: [{
      name: '<= 1 year',
      value: '1'
    },

    {
      name: '> 1 year',
      value: '2'
    },
  ],

});
const yoeDataSet = yoeDataSetApi.data;
const genderDataSetApi = useApi({
  method: 'get',
  localData: [{
      storedValue: 'M',
      displayValue: 'Male'
    },
    {
      storedValue: 'F',
      displayValue: 'Female'
    },

  ],

});
const genderDataSet = genderDataSetApi.data;

const fnameOnSuffixIconClick = (event) => {
  console.log('sufix icon clicked..');
};
const fnameEnterKey = (event) => {
  console.log('enterkey event');
}

;
const fnameChange = (value) => {
  console.log("change event")
  console.log(value);
};
const fnameClear =
  //clear: Triggered when the input is cleared by clicking the clear button
  () => {
    console.log("kills")
  };

const taBlur = (event) => {
  console.log('blurred me');

};
const taFocus = (event) => {
  console.log('you just focused')
};
const taInput = (value) => {
  console.log(value);
};
const taChange = (value) => {
  console.log('input Event');
};
const btnsetClick = () => {
  formData.firstName = 'gupta'
  formData.lastName = 'Hardik'
};
const printBtnClick = () => {
  doSome();
};

function doSome() {
  console.log(formData.firstName)
  console.log(formData.lastName)
  console.log(formData.dob)
  console.log(formData.gender)
  console.log(formData.hobbies)
  console.log(formData.yoe)
  console.log(formData.age)
  console.log(formData.textarea)
}
</script>

<template>
  <VueForm ref="form" :model="formData" v-loading="lockScreen">
    <VueText type="danger" size="large" id="text" ref="text" :style="{ width : '100%', display : 'inline-block', fontSize : '25px', fontWeight : 'bolder', fontStyle : 'italic', color : '#D9EA19', backgroundColor : '#DD7F21', textAlign : 'center', lineHeight : '40px', }"> Hell Everyone
    </VueText>


    <VueFormItem :label="t('label.firstName')" prop="firstName" :rules="rules.fnameRules">
      <VueInput data-type="string" type="text" :clearable="true" id="fname" ref="fname" v-model="formData.firstName" :on-suffix-icon-click="fnameOnSuffixIconClick" @change="fnameChange" @clear="fnameClear" :suffix-icon="IconAddLocation" @keydown.enter="fnameEnterKey">


      </VueInput>
    </VueFormItem>


    <VueFormItem :label="t('label.lastName')" prop="lastName">
      <VueInput data-type="string" id="lName" ref="lName" v-model="formData.lastName">


      </VueInput>
    </VueFormItem>


    <VueFormItem label="label.age" prop="age">
      <VueInputNumber :min="0" :max="200" :step="2" :use-separator="true" :controls="true" placeholder="Enter Age.." text-align="right" id="age" ref="age" v-model="formData.age">
        <template #prefix>
          $
        </template>

      </VueInputNumber>


    </VueFormItem>


    <VueFormItem :label="t('label.dob')" prop="dob">
      <VueDatePicker type="date" id="dob" ref="dob" v-model="formData.dob" :format="CONST_SYSTEM_DATE_FORMAT.ddmmyyyy" :value-format="CONST_SYSTEM_DATE_VALUE_FORMAT.yyyymmdd" />
    </VueFormItem>


    <VueFormItem :label="t('label.hobbies')" prop="hobbies">

      <VueCheckboxGroup id="hobbies" ref="hobbies" v-model="formData.hobbies" split-size="default">
        <VueCheckbox v-for="option in hobbiesDataSet" :key="option.value" :label="option.value" :name="option.name" :disabled="option.disabled">
          {{option.name}}
        </VueCheckbox>
      </VueCheckboxGroup>
    </VueFormItem>


    <VueFormItem :label="t('label.yoe')" prop="yoe">
      <VueSelect id="yoe" ref="yoe" v-model="formData.yoe" :options="yoeDataSet" :props="yoeProps">


      </VueSelect>
    </VueFormItem>

    <VueDropdown :split-button="true" id="yoeDropDown" ref="yoeDropDown">
      <VueIcon class="vue-icon--left">
      </VueIcon>
      yoeDropDown
      <template #dropdown>
        <VueDropdownMenu>
          <VueDropdownItem v-for="item in yoeDropDownDataSet" :command="item.command" :disabled="item.disabled" :divided="item.divided" :icon="item.icon">
            {{item.text}}
          </VueDropdownItem>
        </VueDropdownMenu>
      </template>
    </VueDropdown>

    <VueFormItem :label="t('label.description')" prop="textarea">
      <VueInput type="textarea" :uppercase="true" resize="both" placeholder="Enter the Text Here..." :rows="5" :maxlength="50" :show-word-limit="true" id="ta" ref="ta" v-model="formData.textarea" @blur="taBlur" @focus="taFocus" @input="taInput" @change="taChange" />
    </VueFormItem>

    <VueButton icon-position="left" id="btnset" ref="btnset" @click="btnsetClick">
      {{t('button.setButton')}}

    </VueButton>
    <VueButton icon-position="left" id="printBtn" ref="printBtn" @click="printBtnClick">
      {{t('Button.printButton')}}

    </VueButton>


  </VueForm>
</template>