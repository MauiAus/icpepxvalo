<template>
    <div id="standBox">
        <div id="navBox">
            <p v-on:click="toggleA()">Group A</p>
            <p v-on:click="toggleB()">Group B</p>
            <p v-on:click="toggleF()">Finals</p>
        </div>
        <div id="bracketA">
            <div id="quarter">
                <p>Knockout</p>
                <div id="backBorder">
                    <div id="border1">
                    </div>
                    <div id="border2">
                    </div>
                    <div id = "teamBox">
                        <p>{{listData[0].teamName}}</p>
                    </div>
                    <div id = "teamBox1">
                        <p>{{listData[1].teamName}}</p>
                    </div>
                    <div id = "teamBox2">
                        <p>{{listData[2].teamName}}</p>
                    </div>
                    <div id = "teamBox3">
                        <p>{{listData[3].teamName}}</p>
                    </div>
                    <div id = "teamBox4">
                        <p>{{listData[4].teamName}}</p>
                    </div>
                    <div id = "teamBox5">
                        <p>{{listData[5].teamName}}</p>
                    </div>
                    <div id = "teamBox6">
                        <p>{{listData[6].teamName}}</p>
                    </div>
                    <div id = "teamBox7">
                        <p>{{listData[7].teamName}}</p>
                    </div>
                </div>
            </div>
            <div id="semi">
                <p>Quarterfinals</p>
                <div id="border">
                </div>
            </div>
            <div id="finals">
                <p>Semifinals</p>
                <div id="border">
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name:"Standings",
    data(){
        return{
            listData:[{teamName:"",quarterPos:"",quarterScore:"",semiPos:"",semiScore:"",finalPos:"",finalScore:""}],
            qStyle:["5vh","0vh","5vh","0vh","5vh","0vh","5vh","0vh"],
            showA:true,
            showB:false,
            finals:false,
            ctr:0,
        }
    },
    methods:{
        loadData(){
            const GoogleSpreadsheet = require('google-spreadsheet');
            const { promisify } = require('util');

            const creds = require('./client_secret.json');

            var tempData=[];

            async function accessSpreadsheet(tempData){
                const doc = new GoogleSpreadsheet('1DghFM-X5N4cbvHXYiN5bLc5gYLOo2-V7QqyZfelq2vw');
                await promisify(doc.useServiceAccountAuth)(creds);
                const info = await promisify(doc.getInfo)();
                const sheet = info.worksheets[0];
                
                const rows = await promisify(sheet.getRows)({
                    offset: 1
                });

                rows.forEach( row => {
                    tempData.push({teamName:row.teamname,quarterPos:row.quarterpos,quarterScore:row.quarterscore,semiPos:row.semipos,semiScore:row.semiscore,finalPos:row.finalpos,finalScore:row.finalscore});
                })
            }

            accessSpreadsheet(tempData);

            this.listData = tempData;
        },
        toggleA(){
            this.showA = true;
            this.showB = false;
            this.finals = false;
            console.log(this.listData)
            console.log(this.testList)
        },
        toggleB(){
            this.showA = false;
            this.showB = true;
            this.finals = false;
        },
        toggleF(){
            this.showA = false;
            this.showB = false;
            this.finals = true;
        },
        test(){
            if(this.ctr < 8)
            {
                console.log(this.qStyle)
                this.ctr+=1;
                console.log(this.ctr)
            }
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
    #bracketA{
        display: flex;
        min-height: 90vh;
        p{
            padding:2%;
        }
        #quarter{
            background-color: red;
            width:33.33%;
            #border1{
                position: absolute;
                margin-top: 10vh;
                border-bottom: 2px solid #fff;
                border-top: 2px solid #ffffff;
                border-right: 2px solid #ffffff;
                border-radius: 0;
                margin-left: 2vw;
                height:20vh;
                width:31.33%
            }
            #border2{
                position: absolute;
                margin-top: 45vh;
                border-bottom: 2px solid #fff;
                border-top: 2px solid #ffffff;
                border-right: 2px solid #ffffff;
                height:20vh;
                width:31.33%;
                margin-left:2vw;
            }
            #teamBox{
                position:absolute;
                background-color: blue;
                height:5vh;
                margin-top: 5vh;
                width: 25%;
                margin-left:2vw;
            }
            #teamBox1{
                position:absolute;
                background-color: blue;
                height:5vh;
                margin-top: 10vh;
                width: 25%;
                margin-left:2vw;
            }
            #teamBox2{
                position:absolute;
                background-color: blue;
                height:5vh;
                margin-top: 25.5vh;
                width: 25%;
                margin-left:2vw;
            }
            #teamBox3{
                position:absolute;
                background-color: blue;
                height:5vh;
                margin-top: 30.5vh;
                width: 25%;
                margin-left:2vw;
            }
            #teamBox4{
                position:absolute;
                background-color: blue;
                height:5vh;
                margin-top: 40vh;
                width: 25%;
                margin-left:2vw;
            }
            #teamBox5{
                position:absolute;
                background-color: blue;
                height:5vh;
                margin-top: 45vh;
                width: 25%;
                margin-left:2vw;
            }
            #teamBox6{
                position:absolute;
                background-color: blue;
                height:5vh;
                margin-top: 60.5vh;
                width: 25%;
                margin-left:2vw;
            }
            #teamBox7{
                position:absolute;
                background-color: blue;
                height:5vh;
                margin-top: 65vh;
                width: 25%;
                margin-left:2vw;
            }
        }
        #semi{
            background-color: green;
            width:33.33%;
            #border{
                position: absolute;
                margin-top: 20vh;
                border-bottom: 2px solid #fff;
                border-top: 2px solid #ffffff;
                border-right: 2px solid #ffffff;
                height:35vh;
                width:33.33%
            }
        }
        #finals{
            background-color: greenyellow;
            width:33.33%;
            #border{
                position: absolute;
                margin-top: 36vh;
                border-top: 2px solid #ffffff;
                border-right: 2px solid #ffffff;
                height:0vh;
                width:33.33%
            }
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

