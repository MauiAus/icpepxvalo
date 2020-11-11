<template>
    <div id="standBox">
        <div id="navBox">
            <p>Group A</p>
            <p>Group B</p>
            <p v-on:click="loadData()">Finals</p>
        </div>
    </div>
</template>

<script>
export default {
    name:"Standings",
    data(){
        return{
            listData:[],
        }
    },
    methods:{
        loadData(){
            const GoogleSpreadsheet = require('google-spreadsheet');
            const { promisify } = require('util');

            const creds = require('./client_secret.json');

            async function accessSpreadsheet(){
                const doc = new GoogleSpreadsheet('1DghFM-X5N4cbvHXYiN5bLc5gYLOo2-V7QqyZfelq2vw');
                await promisify(doc.useServiceAccountAuth)(creds);
                const info = await promisify(doc.getInfo)();
                const sheet = info.worksheets[0];
                
                const rows = await promisify(sheet.getRows)({
                    offset: 1
                });

                var tempData = [];

                rows.forEach( row => {
                    tempData.push({teamName:row.teamname,quarterPos:row.quarterpos,quarterScore:row.quarterscore,semiPos:row.semipos,semiScore:row.semiscore,finalPos:row.finalpos,finalScore:row.finalscore});
                })
                return tempData;
            }

            this.listData = accessSpreadsheet();
            console.log(this.listData)
        }
    },
    beforeMount(){
        this.loadData();
    }
}
</script>

<style lang="scss" scoped>
#standBox{
    float:left;
    background-color: chocolate;
    width:100%;
    #navBox{
        background-color: chartreuse;
        display: flex;
        p{
            padding:0% 2%;
        }
    }
}
</style>

<!--
        loadData(){
            const GoogleSpreadsheet = require('google-spreadsheet');
            const { promisify } = require('util');

            const creds = require('./client_secret.json');

            async function accessSpreadsheet(){
                const doc = new GoogleSpreadsheet('1DghFM-X5N4cbvHXYiN5bLc5gYLOo2-V7QqyZfelq2vw');
                await promisify(doc.useServiceAccountAuth)(creds);
                const info = await promisify(doc.getInfo)();
                const sheet = info.worksheets[0];
                
                const rows = await promisify(sheet.getRows)({
                    offset: 1
                });

                var tempData = [];

                rows.forEach( row => {
                    console.log(row.teamName)
                    tempData.push[{teamName:row.teamName,quarterPos:row.quarterPos,quarterScore:row.quarterScore,semiPos:row.semiPos,semiScore:row.semiScore,finalPos:row.finalPos,finalScore:row.finalScore}]
                })

                console.log(tempData)
            }

            accessSpreadsheet();
            tempData.push[{teamName:row.teamname,quarterPos:row.quarterpos,quarterScore:row.quarterscore,semiPos:row.semipos,semiScore:row.semiscore,finalPos:row.finalpos,finalScore:row.finalscore}]
-->

