<template>
    <form v-on:submit.prevent="submitForm" method='post'>
        <label>Customer</label>
            <input type="text" v-model="form.customer">
        <label>Part No</label>
            <input type="text" v-model="form.part_no">
        <label>Part Name</label>
            <input type="text" v-model="form.part_name">
        <label>Mould Size</label>
            <input type="text" v-model="form.mould_size">
        <label>Cavity</label>
            <input type="text" v-model="form.cavity">
        <label>Ton Sale</label>
            <input type="text" v-model="form.ton_sale">
        <label>Ton PD</label>
            <input type="text" v-model="form.ton_pd">
        <label>C/T Sale</label>
            <input type="text" v-model="form.ct_sale">
        <label>C/T PD</label>
            <input type="text" v-model="form.ct_pd">
        <label>Customer-Part No-Part Name</label>
            <input type="text" v-model="form.customer_part_no_part_name">
        <label>C/T</label>
            <input type="text" v-model="form.ct">
        <label>PCS/HR</label>
            <input type="text" v-model="form.pcs_hr">
        <button type="button" class="btn btn-primary" @click="submitForm">Submit</button>
    </form>
</template>

<script>
import { ref } from 'vue'
import axios from 'axios'

export default ({
    setup() {
        const form = ref({
            customer: null,
            part_no: null,
            part_name: null,
            mould_size: null,
            cavity: null,
            ton_sale: null,
            ton_pd: null,
            ct_sale: null,
            ct_pd: null,
            customer_part_no_part_name: null,
            ct: null,
            pcs_hr: null,
        })

        const submitForm = async () => {
            return await axios({
                method: 'POST',
                url: "http://127.0.0.1:8081/insertModule",
                data: form,
            }).then(res => {
                return res.data
            }).catch(e => {
                return e
            })
        }

        return {
            form,
            submitForm,
        }
    },
})
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