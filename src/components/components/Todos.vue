<template>
    <div class="div">
        <ul>
            <li v-for="(todo, index) in todos" :key="index">{{ todo }}<span @click="del(index)" data-id="index"
                    class="delet" >x</span></li>

        </ul>

    </div>
    <div>
        <ul>
            <li v-for="(todo, index) in todos2" :key="index">{{ todo }}<span @click="del2(index)" data-id="index"
                    class="delet">x</span></li>

        </ul>
    </div>
</template>
<script>
export default {
    props: {
        todos: Array,
        todos2: Array
    },


    methods: {
        del(id) {
            console.log(id);
            {
                this.todos.splice(id, 1);
            }

        },
        del2(id) {
            console.log(id);
            {
                this.todos2.splice(id, 1);
            }
        },
        editli(todo, index) {

            input.value = todo;

            this.todos.splice(index, 1);

        }
    }
};
</script>
<style>
ul li {

    border: 1px solid #444;
    border-radius: 5px;
    /* width: 450px; */
    list-style-type: none;
    position: relative;
    /* right: 100px; */
    /* padding-left: 20px; */
    /* margin: 3px; */
    text-align: center;
    /* margin-left: 38%; */
    padding: 8px
}

li {
    background-color: white;
}

ul li:hover {
    background-color: rgb(238, 234, 234);
}

.close {
    color: rgb(223, 81, 81);
    float: right;
    padding-right: 5px;
    cursor: pointer;


}

.delet {
    color: red;
    float: right;
    cursor: pointer;

}
</style>
  