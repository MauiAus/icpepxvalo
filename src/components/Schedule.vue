<template>
    <div id="schedBox">
    </div>
</template>

<script>
export default {
    name:"Schedule",
    data(){
        return{
            schedList:[],
        }
    },
    methods:{
        loadData(){
            const GoogleSpreadsheet = require('google-spreadsheet');
            const { promisify } = require('util');

            const creds = require('./client_secret.json');

            var tempData=[];

            async function accessSpreadsheet(){
                const doc = new GoogleSpreadsheet('1c1HXy7YA9ycbMr4N5z-rqlp_ZAwWARYWL0ckKp1LyTw');
                await promisify(doc.useServiceAccountAuth)(creds);
                const info = await promisify(doc.getInfo)();
                const sheet = info.worksheets[0];
                
                const rows = await promisify(sheet.getRows)({
                    offset: 1
                });

                rows.forEach( row => {
                    tempData.push({day:row.day,date:row.date,time:row.time,teama:row.teama,ascore:row.ascore,bscore:row.bscore,teamb:row.teamb,type:row.type});
                })
            }
            accessSpreadsheet();
            this.schedList = tempData;
            console.log(this.schedList)
        },
    },
    beforeMount(){
        this.loadData();
    }
}
</script>

<style lang="scss" scoped>
#schedBox{
    float:left;
    width:100%;
}
</style>


