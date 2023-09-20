<template>
    <div v-show="this.state == 2">
        <div class="container">
            <div class="package2">
                <h class="h">اطلاعات تخصصی طرح</h>
                <hr>
                <div class="row">
                    <din class="col-lg-2"></din>
                    <div class="col-lg-4">
                        <label>هدف مطالعه</label>
                        <select class="form-control">
                            <option v-for="(targ, index) in formdata2.target" :key="index">
                                {{ targ }}
                            </option>
                        </select>
                    </div>
                    <div class="col-lg-4">
                        <label>فازمطالعه</label>
                        <select class="form-control">
                            <option v-for="(phas, index) in formdata2.phase" :key="index">
                                {{ phas }}

                            </option>
                        </select>
                    </div>
                    <div class="col-lg-2"></div>
                </div>
                <div class="row">
                    <div class="col-lg-2"></div>
                    <div class="col-lg-4">
                        <label>تصادفی سازی</label>
                        <select class="form-control">
                            <option v-for="(Random, index) in formdata2.Randomization" :key="index">
                                {{ Random }}
                            </option>
                        </select>
                    </div>
                    <div class="col-lg-4">
                        <label>کور سازی</label>
                        <select class="form-control">
                            <option v-for="(blin, index) in formdata2.blinding" :key="index">
                                {{ blin }}

                            </option>
                        </select>
                    </div>
                    <div class="col-lg-2"></div>
                </div>
                <div class="row">

                    <div class="col-lg-4"></div>
                    <div class="col-lg-4">
                        <input type="text" class="form-control" v-model="inputtext" onkeypress="return event.keyCode != 13;" />
                        <span class="red" :class="{ span2: flag }">{{ formdata2.texterror }}</span>
                    </div>
                    <div class="col-lg-4"></div>
                </div>
                <div class="row">
                    <div class="buttons">
                        <button @click.prevent="changepage" class="next">بعدی</button>
                        <button @click.prevent="prevpage()" class="prev">قبلی</button>
                    </div>
                </div>
            </div>
        </div>
        <button @click.prevent="changepage()" class="but-page-3">3</button>
        <button class="but-page-2">2</button>
        <button @click.prevent="prevpage()" class="but-page-1">1</button>


    </div>
</template>

<script>

import useValidate from '@vuelidate/core'
import { required } from '@vuelidate/validators'
export default {
    props: {
        formdata2: Object,
        state: Number,
    },
    data() {
        return {
            v$: useValidate(),
            flag: false,
            inputtext: this.formdata2.title,
            // texterror: ''
        }
    },
    methods: {
        changepage() {
          if(this.inputtext==="")
        // this.v$.$validate()
        //     if (!this.v$.$error)
        {
                // this.$emit("stateUpdate", 2);
                this.flag = true;
                console.log(this.inputtext)
            } else {
                this.flag = false;
                this.$emit("stateUpdate", 2);

                console.log(this.inputtext)

            }

        },
        prevpage() {
            this.$emit("statePrev", 2)
        },
        validations() {
            return {
                inputtext: { required },

            }

        }

    },
}
</script>
<style scoped>
body {
    direction: rtl !important;
}

.package2 {
    direction: rtl !important;
}

.head {
    margin-top: 2rem;
    width: 100%;
    background-color: rgb(54, 189, 54);

    border: 1px solid #444;
    text-align: center;
    padding: 5px;
    /* color: rgb(54, 189, 54); */
    margin-bottom: 0.5rem;
}


.action {
    background-color: rgb(242, 248, 242);
    border: 2px solid rgb(187, 178, 178) !important;
    color: rgb(56, 54, 54);
    padding: 5px;
    margin: 10px;
}

.but1 {
    float: right;

    padding: 5px 15px;
    margin: 5rem 2rem;
    background-color: rgb(22, 129, 22);
    color: white;
}

.group {
    margin-top: 4rem;
    border: 1px solid #ccc5c5;
    border-radius: 8px;
}

.buttons {
    text-align: center;
    margin-top: 1rem;
}

.next,
.prev {
    padding: 4px 14px;
    margin: 5px;
    color: #444;
    background-color: rgb(54, 189, 54);
}

.prev {
    background-color: white;
    border: 1px solid rgb(54, 189, 54);
    color: rgb(54, 189, 54);
    ;
}

.but-page-1,
.but-page-3 {
    border-radius: 50%;
    background-color: rgb(161, 235, 161);
    padding: 5px 10px;
    margin: 2px;
}

.but-page-2 {
    border-radius: 50%;
    background-color: rgb(19, 180, 19);
    padding: 5px 10px;
}

.input {
    margin-top: 2rem;
}

.red {
    opacity: 0;
}

.span2 {
    opacity: 1;
    color: red;
    border: 1px solid red;
    font-size: 11px;
    padding: 2px;
}
</style>
