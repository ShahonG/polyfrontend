<template>
    <form v-on:submit.prevent="submitForm" method='post'>
        <label>MC-TON</label>
        <select required v-model="form.MC_TON">
            <option v-for="(option, i) in machineOptions" :key=i>{{ option }}</option>
        </select><br>
        <label>CUSTOMER-PART NO-PART NAME</label>
        <select required v-model="form.module">
            <option v-for="(option, i) in moduleOptions" :key=i>{{ option }}</option>
        </select><br>
        <table>
            <th>
            <label>OK Product</label>
                <input type="text" required v-model="form.product">
            </th>
            <th>
            <label>NG Product</label>
                <input type="text" required v-model="form.productNG">
            </th>
        </table>
        <table>
            <th>
            <label>OK Product <br>(not necessary)</label>
                <input type="text" v-model="form.product_2">
            </th>
            <th>
            <label>NG Product <br>(not necessary)</label>
                <input type="text" v-model="form.productNG_2">
            </th>
        </table>
        <label>time</label>
        
        <select required v-model="form.time">
            <option v-for="(time, i) in 24" :key=i>{{ i }} - {{ i+1 }}</option>
        </select><br><br>
        <button type="button" class="btn btn-primary" @click="submitForm">Submit</button>
    </form>
</template>

<script>
import { onMounted, ref } from 'vue'
import axios from 'axios'

export default {
    setup() {
        const machineOptions = ref([])
        const moduleOptions = ref([])

        onMounted(() => {
            axios({
                method: 'POST',
                url: "http://127.0.0.1:8081/loadMachineInfo",
            }).then(res => {
                // console.log(res)
                machineOptions.value = res.data.machine
                moduleOptions.value = res.data.module
                // pass some status to App.vue means insertion happen
            }).catch(e => {
                console.log(e)
            })
        })

        return {
            machineOptions,
            moduleOptions
        }
    },
    data () {
        return {
            form: {
                MC_TON: null,
                module: null,
                product: 0,
                productNG: 0,
                product_2: null,
                productNG_2: null,
                time: null,
            },
        }
    },
    methods: {
        submitForm () {
            console.log(this.form)
            axios({
                method: 'POST',
                url: "http://127.0.0.1:8081/insert",
                data: this.form,
            }).then(res => {
                console.log(res)
                location.reload()
            }).catch(e => {
                console.log(e)
            })
        }
    }
}
</script>


<style>
    form {
        max-width: 420px;
        margin: 30px auto;
        background: #aaa;
        text-align: left;
        padding: 40px;
        border-radius: 10px;
    }
    label {
        color: #000;
        display: inline-block;
        margin: 25px 0 15px;
        font-size: 0.6em;
        text-transform: uppercase;
        letter-spacing: 1px;
        font-weight: bold;
    }
    input {
        display: block;
        padding: 10px 6px;
        width: 100%;
        box-sizing: border-box;
        border: none;
        border-bottom: 1px solid #ddd;
        text-align: center;
        color: #000;
    }
    select {
        width: 100%;
        height: 30px;
    }
</style>