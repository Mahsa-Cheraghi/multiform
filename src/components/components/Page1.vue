<template>
    <div v-show="this.state == 1">

        <div class="container">

            <div class="package1">
                <div class="row">
                    <h class="h">اطلاعات عمومی طرح</h>
                    <hr>
                </div>
                <div class="row">
                    <div class="col-lg-4">
                        <lable>عنوان طرح</lable>
                        <input type="text" class="form-control" v-model="name" onkeypress="return event.keyCode != 13;" />
                        <span class="span" :class="{ span2: flag }">{{ formdata.error }}</span>
                    </div>

                    <div class="col-lg-4">
                        <lable>نام اختصاری:</lable>
                        <input type="text" class="form-control" v-model="formdata.name" />
                    </div>
                </div>
                <div class="row">
                    <div class="col-lg-4">
                        <lable>نوع طرح:</lable>
                        <select class="form-control" v-model="formdata.type">
                            <option v-for="(type, index) in formdata.types" :key="index">
                                {{ type }}
                            </option>
                        </select>
                    </div>
                    <div class="col-lg-4">
                        <lable>طراحی مطالعه:</lable>
                        <br>
                        <select class="form-control select" v-model="formdata.design">
                            <option class="select" v-for="(design, index) in formdata.designing" :key="index">
                                {{ design }}
                            </option>
                        </select>
                    </div>
                </div>
                <br>
                <div class="row">
                    <div class="col-lg-4">
                        <lable>تاریخ شروع کارآزمایی:</lable>

                        <date-picker v-model="formdata.datestart" />
                    </div>
                    <div class="col-lg-4">
                        <label>تاریخ پایان کارآزمایی:</label>
                        <date-picker v-model="formdata.dateend" />
                    </div>
                </div>
                <div class="row">
                    <div class="col-lg-7">
                        <div class="choose">
                            <label class=" btn btn-success search-file-btn">
                                <input class="form-control" name="file2" type="file" style="display:None;"> <span
                                    class="file">choosefile
                                </span>
                            </label>
                            <input type="text" class=" text file2">

                        </div>
                    </div>
                </div>
                <div class="row">
                    <div class="col-lg-5">
                        <button @click.prevent="change" class="but">بعدی</button>
                    </div>
                </div>
            </div>

        </div>
        <button @click.prevent="page3" class="but-page3">3</button>
        <button @click.prevent="page2" class="but-page2">2</button>
        <button class="but-page1">1</button>


    </div>
</template>
<script>
import DatePicker from 'vue3-persian-datetime-picker'
import useValidate from '@vuelidate/core'
import { required } from '@vuelidate/validators'
import Swal from 'sweetalert2'
export default {
    components: { DatePicker },
    props: {
        formdata: Object,
        state: Number
    },
    data() {
        return {
            v$: useValidate(),
            flag: false,
            name: this.formdata.title
        }
    },

    methods: {
        change() {
            this.v$.$validate()
            if (!this.v$.$error) {
                Swal.fire({
                    title: 'thanks!',
                    text: 'successfully',
                    icon: 'success',
                    confirmButtonText: 'Ok'
                })
                this.$emit("stateUpdate", 2);
                this.flag = false;
                console.log(this.name)
            } else {
                this.flag = true;
                // console.log(this.flag)

            }
        },
        page2() {
            this.v$.$validate()
            if (!this.v$.$error) {
                alert('Form successfully submitted.')
                this.$emit("stateUpdate", 2);
                this.flag = false;
                // console.log(this.flag)
            } else {
                this.flag = true;
                // console.log(this.flag)

            }
        },
        page3() {
            this.v$.$validate()
            if (!this.v$.$error) {
                alert('Form successfully submitted.')


                this.$emit("stateUpdate2", 2);
                this.flag = false;
                console.log(this.flag)
            } else {
                this.flag = true;
                console.log(this.flag)

            }
        }

    },
    validations() {
        return {
            name: { required },

        }

    }
}

</script>
<style scope>
@import url("../../../css/all.css");

body {
    background-color: rgb(250, 253, 250) !important;
    direction: rtl;
}

.data {

    font-size: 30px;
    border: none;
}



.package1 {

    direction: rtl;
    width: 80%;
}

.h {
    padding: 4%;
    font-size: 2rem;

}

#file {
    position: relative;
    overflow: hidden;
    background-color: rgb(22, 129, 22);

}


.text {
    height: 50px;
    margin-top: 10%;
    width: 50%;
    border-radius: 15px;
}

.but {
    margin-top: 10px;
    background-color: rgb(22, 129, 22);
    padding: 5px 22px;
    border-radius: 8px;
    color: white;
}

.span {
    opacity: 0;
}

.span2 {
    opacity: 1;
    color: red;
    border: 1px solid red;
    font-size: 11px;
    padding: 2px;
}

input:hover {
    /* border: none; */
    outline: none;
    border: 1px solid rgb(29, 126, 29);
    ;
    background-color: rgb(250, 252, 250);

}

input:focus {
    border: 1.5px solid rgb(29, 126, 29) !important;
}

.but-page1,
.but-page2,
.but-page3 {
    border-radius: 50%;
    padding: 5px 10px;
    background-color: rgb(19, 180, 19);
    color: white;
}

.but-page2,
.but-page3 {
    background-color: rgb(161, 235, 161);
}
</style>