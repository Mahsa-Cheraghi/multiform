<template>
    <div v-show="this.state == 3">
        <div class="container">
            <div class="packade3">
                <div class="row">
                    <h>اطلاعات شرکت کنندکان</h>
                    <hr>
                </div>
                <div class="row">
                    <div class="col-lg-2"></div>
                    <div class="col-lg-4">
                        <div class="one-box">
                            <label>شرایط ورود به مطالعه:</label>
                            <div>
                                <input class="form-control" v-model="val" ref="title" type="text"
                                    onkeypress="return event.keyCode != 13;" />
                                <span @click="sendvalue" id="submit">+</span>
                            </div>
                            <Todos :todos="this.todos" />

                        </div>
                    </div>
                    <div class="col-lg-4">
                        <div class="one-box">
                            <label>شرایط عدم ورود به مطالعه:</label>
                            <div>
                                <input class="form-control" v-model="vall" ref="title" type="text" id="input"
                                    onkeypress="return event.keyCode != 13;" />
                                <span @click="sendvalue2" id="submit">+</span>
                            </div>
                            <Todos :todos2="this.todos2" />
                            <div class="col-lg-2"></div>
                        </div>
                    </div>
                </div>
                <div class="row">
                    <div class="col-lg-10">
                        <label>بیمارگیری خاتمه پیدا کرده است</label>
                        <input type="checkbox" class="form-check-input">
                    </div>
                    <div class="col-lg-2"></div>
                </div>
                <br>
                <div class="row">
                    <div class="col-lg-2"></div>
                    <div class="col-lg-4">
                        <lable>تاریخ شروع کارآزمایی:</lable>
                        <date-picker v-model="formdata3.datestart" />
                        <!-- <VueDatePicker class="date" v-model="formdata3.datestart"></VueDatePicker> -->
                    </div>
                    <div class="col-lg-4">
                        <label>تاریخ پایان کارآزمایی:</label>
                        <date-picker v-model="formdata3.dateend" />
                    </div>
                    <div class="col-lg-2"></div>
                </div>
                <div class="row">
                    <!-- <div class="col-lg-2"></div> -->
                    <div>

                        <div class="col-lg-3">
                            <div class="age min">

                                <label>حداقل سن</label>
                                <input type="checkbox" class="form-check-input" v-model="agreement" name="agreement"
                                    @click="dis">

                                <div class="chekbox" :class={dis:agreement}>

                                    <div>
                                        <div> روز:<input type="number" v-model="day" class="form-control" /></div>
                                        <div>ماه:<input type="number" v-model="month" class="form-control" /></div>
                                        <div>سال:<input type="number" v-model="year" class="form-control" /></div>
                                    </div>



                                </div>

                            </div>
                            <span class="span" :class="{ spanerror: flag }">{{ Error }}</span>
                            <br>
                            <span class="span" :class="{ spanerror: flag2 }">{{ Error2 }}</span>
                        </div>

                        <div class="col-lg-3">

                            <div class="age">
                                <label>حداکثر سن</label>
                                <input type="checkbox" class="form-check-input" v-model="agreement2" name="agreement2"
                                    @click="dis2">
                                <div class="chekbox" :class={dis2:agreement2}>

                                    <div>
                                        <div> روز:<input type="number" v-model="day2" class="form-control" /></div>
                                        <div>ماه:<input type="number" v-model="month2" class="form-control" /></div>
                                        <div>سال:<input type="number" v-model="year2" class="form-control" /></div>
                                    </div>



                                </div>
                            </div>
                        </div>
                    </div>

                    <div class="col-lg-4">
                        <label>جنسیت:</label>
                        <select class="form-control">
                            <option v-for="(gend, index) in formdata3.gender" :key="index">
                                {{ gend }}
                            </option>
                        </select>
                    </div>
                    <!-- <div class="col-lg-2"></div> -->
                </div>
                <div class="div">
                    <button class="butprev" @click.prevent="prevpage()">قبلی</button>
                </div>

                <div class="div">
                    <button @click.prevent="valid" class="sabt">ثبت طرح</button>
                </div>
            </div>
        </div>
        <button class="but-page-3">3</button>

        <button @click.prevent="gotopage2" class="but-page-2">2</button>
        <button @click.prevent="gotopage1" class="but-page-1">1</button>
    </div>
</template>
<script>
import DatePicker from 'vue3-persian-datetime-picker'
// import VuePersianDatetimePicker from 'vue-persian-datetime-picker';
import Todos from './Todos.vue'
import Swal from 'sweetalert2'
export default {
    components: { Todos, DatePicker },
    props: {
        formdata3: Object,
        state: Number
    },
    data() {
        return {
            agreement: false,
            agreement2: false,
            day: 0,
            month: 0,
            year: 0,
            day2: 0,
            month2: 0,
            year2: 0,
            id: 0,
            todos: [],
            todos2: [],
            val: this.formdata3.in,
            vall: this.formdata3.out,
            checkedNames: '',
            error: this.formdata3.error,
            Error: '',
            Error2: '',
            flag1: false, flag2: false,
            date: '',
            // flaginput:false
        }
    },
    methods: {
        prevpage() {
            this.$emit("statePrev", 3)
        },
        sendvalue(ev) {
            // $('#inputBox').tagator({
            //     prefix: 'tagator_',           // CSS class prefix
            //     height: 'auto',               // auto or element
            //     useDimmer: false,             // dims the screen when result list is visible
            //     showAllOptionsOnFocus: false, // shows all options even if input box is empty
            //     allowAutocompleteOnly: false, // only allow the autocomplete options
            //     autocomplete: []
            // })
            if (input.value.trim() != "") {
                this.todos.push(this.val);

            }
            input.value = "";
            console.log(this.todos);
        },
        sendvalue2(ev) {
            if (input.value.trim() != "") {
                this.todos2.push(this.vall);

            }

            // input2.value = "";
            console.log(this.todos2);
        },
        dis() {
            this.agreement = true;
            // console.log(this.agreement)
        },
        dis2() {
            this.agreement2 = true;
            // console.log(this.agreement2)
        },
        gotopage2() {
            this.$emit("statePrev", 3)
        },
        gotopage1() {
            this.$emit("statePrev2", 3)
        },
        valid() {
            if (this.day == 0 || this.day <= 0 || this.day >= 32) {
                this.Error = "روز نباید کمتراز یک و بیشتراز 31باشد"
                this.flag = true
            }
            else {
                this.Error = ''
                this.flag = false
            }
            if (this.month == 0 || this.month <= 0 || this.month >= 32) {
                this.Error2 = "ماه نباید کمتراز یک وبیشتراز12باشد"
                this.flag2 = true
            }
            else {


                this.Error2 = ""
                this.flag2 = false
            }
            if (this.flag == false & this.flag2 == false) {
                Swal.fire({
                    title: 'thanks!',
                    text: 'successfully',
                    icon: 'success',
                    confirmButtonText: 'Ok'
                })
            }

        }
    },


}

</script>
<style scoped>
.packade3 {
    direction: rtl;
}

.one-box {
    border: 1px solid #d1cbcb;
    padding: 10px;
    border-radius: 5px;

}

.age {
    /* text-align: center;
    justify-content: center;
    align-items: center; */
    margin-top: 35px;
}

.sabt {

    background-color: rgb(54, 189, 54);
    padding: 10px 25px;
    color: white;
    border-radius: 5px;
}

.div {
    text-align: center;
    margin-top: 2rem;

}

.butprev {

    padding: 5px 10px;
    background-color: white;
    border: 1px solid rgb(54, 189, 54);
    color: rgb(54, 189, 54);

    border-radius: 5px;
}

#submit {
    color: rgb(54, 189, 54);
    font-size: 1.8rem;
    top: -30px;
    right: -5px;
    float: left;
    cursor: pointer;
}

.ch {
    color: red;
}

.chekbox {
    display: none;
}

.dis {
    display: block;
}

.dis2 {
    display: block;
}

.but-page-1,
.but-page-2,
.but-page-3 {
    border-radius: 50%;
    background-color: rgb(161, 235, 161);
    padding: 5px 10px;
    margin: 2px;
}

.but-page-3 {
    background-color: rgb(19, 180, 19);
}

.spanerror,
.spanerror2 {
    opacity: 1;
    color: red;
    /* border: 1px solid red; */
    font-size: 11px;
    padding: 2px;
}
</style>