<template>
    <div id="schedBox">
        <div id="navBox">
            <p>Group A</p>
            <p>Group B</p>
            <p v-on:click="loadData()">Finals</p>
        </div>
    </div>
</template>

<script>
export default {
    name:"Schedule",
    methods:{
        loadData(){
            const GoogleSpreadsheet = require('google-spreadsheet');
            const { promisify } = require('util');

            const creds = require('./client_secret.json');

            async function accessSpreadsheet(){
                const doc = new GoogleSpreadsheet('1qypN_UXvLiJYZifBjBl7zx1_TUw9XoEXr1J4ejVqBeE');
                await promisify(doc.useServiceAccountAuth)(creds);
                const info = await promisify(doc.getInfo)();
                const sheet = info.worksheets[0];
                console.log(sheet.title); 
            }

            accessSpreadsheet();
        }
    }
}
</script>

<style lang="scss" scoped>
#schedBox{
    #navBox{
        display:flex;
        background-color: chartreuse;
        p{
            padding:0% 2%;
        }
    }
}
</style>


