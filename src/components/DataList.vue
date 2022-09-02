<template>
   <table class="DataShowned" v-if="status.ready">
       <!-- 利用setup()裡的status查看資料準備好了沒 -->
       <thead>
           <tr class="title">
               <th>MC-TON</th>
               <th v-for="i in 24" :key=i>{{ i-1 }}-{{ i }}</th>
           </tr>
       </thead>
       <tbody v-for="i in 15" :key=i>
            <tr v-if="i%2==1">
                <th class="colored" rowspan="2" v-if="datas[i-1].MC_TON != null">{{ datas[i-1].MC_TON }}</th>
                <th class="colored" rowspan="2" v-else>MC_TON</th>
                <td class="colored" scope="row" v-for="j in 24" :key="j">{{ datas[i-1].List[j-1].product }}</td>
            </tr>
            <tr v-else>
                <th rowspan="2" v-if="datas[i-1].MC_TON != null">{{ datas[i-1].MC_TON }}</th>
                <th rowspan="2" v-else>MC-TON</th>
                <td scope="row" v-for="j in 24" :key="j">{{ datas[i-1].List[j-1].product }}</td>
            </tr>
            <tr v-if="i%2==1">
                <td class="colored" scope="row" v-for="j in 24" :key="j">{{ datas[i-1].List[j-1].product_2 }}</td>
            </tr>
            <tr v-else>
                <td scope="row" v-for="j in 24" :key="j">{{ datas[i-1].List[j-1].product_2 }}</td>
            </tr>
       </tbody>
   </table>
</template>
<script>

import { onBeforeMount, ref } from 'vue'
import axios from 'axios';

/*
            <tr v-for="(data, i) in datas" :key=i>
                <td scope="row" v-for="(info, j) in data" :key=j>{{ info }}</td>
            </tr>
*/

export default {
    setup () {
        const datas = ref([]);
        const status = ref({
            ready: false,
        });
        const machineOptions = ref([]);

        // async 是這樣寫
        const getMachineInfo = async () => {
            return await axios({
                method: 'POST',
                url: "http://127.0.0.1:8081/loadMachineInfo",
            }).then(res => {
                return res.data.machine
            }).catch(e => {
                console.log(e.message)
                return [];
            });
        };

        const getElement = async (index) => {
            return await axios({
                method: 'POST',
                url: "http://127.0.0.1:8081/loadDataList",
                data: { MC_TON: machineOptions.value[index] }
            }).then(res => {
                return res.data.List
            }).catch(e => {
                console.log(e)
            })
        }

        onBeforeMount(async () => {
            // 看起來你的機器列表固定就是 15 個，我就不特別寫例外處理
            machineOptions.value = await getMachineInfo();

            // 注意：並不建議在 v-for 中執行 async function，因為無法 await 確認執行順序。
            // 因此直接暴力解，在這裡先把 15 個機器的資料準備好
            for (let i = 0; i < 15; i++) {
                let element = await getElement(i)
                datas.value.push(element) // 將每個機器的資料彙整
            }
            status.value.ready = true
            console.log(datas)
        })
        return {
            status,
            datas,
        }
    },
    /* 資料從後端來，需要傳到datas，重翰學長提醒要在setup裡面實作 */
}
</script>

<style scoped>
    table, th, td {
        border: 1px solid;
        text-align: center;
    }
    .DataShowned {
        width: 100%;
    }
    .colored {
        background-color: #D2E9FF;
    }
    .title {
        font-size: 25px;
    }
</style>