<template>
  <div class="container">

    <form class="form"  v-on:submit="hand(event)">
      <Page1 :formdata="this.formdata" @stateUpdate="updateState" @stateUpdate2="updateState2" :state="this.State">
      </Page1>
      <br />
      <!-- {{ this.state }} -->
      <Page2 :formdata2="this.formdata2" @stateUpdate="updateState" @statePrev="prevstate" :state="this.State" />
      <br>
      <Page3 :formdata3="this.formdata3" @statePrev="prevstate" @statePrev2="prevstate2" :state="this.State" />
    </form>
  </div>
</template>
<script>
import Page1 from './Page1.vue';
import Page2 from './Page2.vue';
import Page3 from './Page3.vue';
import useValidate from '@vuelidate/core'
import { required } from '@vuelidate/validators'
export default {
  components: { Page1, Page2, Page3 },

  data() {
    return {

      State: 1,
      formdata: {
        state: 1,
        title: '',
        name: '',
        types: ['پرسشگری', 'نظرسنجی'],
        designing: ['موازی', 'متقاطع', 'فاکتوریل', 'واحد'],
        datestart: '',
        dataend: '',
        error: '*پرکردن این فیلد اجباری است'
      },
      formdata2: {
        title: '',
        target: ['علوم پایه', 'تشخیصی', 'تحقیقات', 'پیشگیری'],
        phase: ['0', 1, 1 - 2, 2],
        Randomization: ['تصادفی به گروه های مداخله', 'اختصاص غیر تصادفی', 'مصداق ندارد'],
        blinding: ['کور نشده است', 'افراد شرکت کننده در مطالعه', 'ارزیابی کننده', 'تحلیلگردرمطالعه'],
        texterror: 'پرکردن این فیلد اجباریست*'

      },
      formdata3: {
                error:'',
        in: '',
        out: '',
        datestart: '',
        dateend: '',
        gender: ['مرد', 'زن', 'هردو'],
      },



    }
  },

  methods: {
    //   submitform(){
    //     console.log(this.v$)
    //     this.v$.$validate()
    //     if(!this.v.$error){
    //       alert('oook');
    //     }else{
    //       alert('no');
    //     }

    // },
    updateState(n) {
      console.log(n)
      this.State += 1;
      console.log(this.State)
    },
    updateState2() {
      this.State += 2;
    },
    prevstate(n) {
      this.State -= 1;
      console.log(this.State)
    },
    prevstate2() {
      this.State -= 2;
    }
  },
  watch: {
    State(newState, old) {
      console.log(newState, old)
    }
  },


};

</script>
<style>
body {

  text-decoration: rtl;
}
</style>