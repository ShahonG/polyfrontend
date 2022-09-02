<template>
    <h1 class="MC"> {{ MachineName }}</h1>
    <table class="DataShowned">
       <thead>
           <tr class="tag">
                <th>date</th>
                <td v-for="i in 24" :key=i>{{ i-1 }}-{{ i }}</td>
           </tr>
       </thead>
       <tbody v-for="(data, i) in datas" :key=i>
           <tr>
                <th rowspan="2">{{ data.Date }}</th>
                <td v-for="(data, j) in datas" :key=j>{{ data.One }}</td>
           </tr>
           <tr>
                <td v-for="(data, j) in datas" :key=j>{{ data.two }}</td>
           </tr>
       </tbody>
   </table>
</template>

<script>

export default {
    data () {
        return {
            MachineName: "1",
            datas: [
                {
                    Date: "2022.7.1" , 
                    One: "1, 1",
                    two: "2, 2"
                },
                {
                    Date: "2022.7.2" ,
                    One: "3, 3",
                    two: "4, 4",
                },
                {
                    Date: "2022.7.3",
                    One: "5, 5",
                    two: "6, 6"
                },
                {
                    Date: "2022.7.4",
                    One: "7, 7",
                    two: "8, 8",
                },
                {
                    Date: "2022.7.5",
                    One: "9, 9",
                    two: "10, 10",
                },
            ],
        }
    }
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
</style>