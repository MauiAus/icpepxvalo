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
                        <p id="name">{{listData[0].teamName}}</p>
                        <p id="score">{{listData[0].quarterScore}}</p>
                    </div>
                    <div id = "teamBox1">
                        <p id="name">{{listData[1].teamName}}</p>
                        <p id="score">{{listData[1].quarterScore}}</p>
                    </div>
                    <div id = "teamBox2">
                        <p id="name">{{listData[2].teamName}}</p>
                        <p id="score">{{listData[2].quarterScore}}</p>
                    </div>
                    <div id = "teamBox3">
                        <p id="name">{{listData[3].teamName}}</p>
                        <p id="score">{{listData[3].quarterScore}}</p>
                    </div>
                    <div id = "teamBox4">
                        <p id="name">{{listData[4].teamName}}</p>
                        <p id="score">{{listData[4].quarterScore}}</p>
                    </div>
                    <div id = "teamBox5">
                        <p id="name">{{listData[5].teamName}}</p>
                        <p id="score">{{listData[5].quarterScore}}</p>
                    </div>
                    <div id = "teamBox6">
                        <p id="name">{{listData[6].teamName}}</p>
                        <p id="score">{{listData[6].quarterScore}}</p>
                    </div>
                    <div id = "teamBox7">
                        <p id="name">{{listData[7].teamName}}</p>
                        <p id="score">{{listData[7].quarterScore}}</p>
                    </div>
                </div>
            </div>
            <div id="semi">
                <p>Quarterfinals</p>
                <div id="border">
                </div>
                <div id = "teamBox">
                    <p id="name">{{aqList[0].teamName}}</p>
                    <p id="score">{{aqList[0].semiScore}}</p>
                </div>
                <div id = "teamBox1">
                    <p id="name">{{aqList[1].teamName}}</p>
                    <p id="score">{{aqList[1].semiScore}}</p>
                </div>
                <div id = "teamBox2">
                    <p id="name">{{aqList[2].teamName}}</p>
                    <p id="score">{{aqList[2].semiScore}}</p>
                </div>
                <div id = "teamBox3">
                    <p id="name">{{aqList[3].teamName}}</p>
                    <p id="score">{{aqList[3].semiScore}}</p>
                </div>
            </div>
            <div id="finals">
                <p>Semifinals</p>
                <div id="border">
                </div>
                <div id = "teamBox">
                    <p id="name">{{asList[0].teamName}}</p>
                    <p id="score">{{asList[0].finalScore}}</p>
                </div>
                <div id = "teamBox1">
                    <p id="name">{{asList[1].teamName}}</p>
                    <p id="score">{{asList[1].finalScore}}</p>
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
            aqList:[{teamName:"",quarterPos:"",quarterScore:"",semiPos:"",semiScore:"",finalPos:"",finalScore:""}],
            asList:[{teamName:"",quarterPos:"",quarterScore:"",semiPos:"",semiScore:"",finalPos:"",finalScore:""}],
            showA:true,
            showB:false,
            finals:false,
            ctr:0,
        }
    },
    methods:{
        loadDataA(){
            const GoogleSpreadsheet = require('google-spreadsheet');
            const { promisify } = require('util');

            const creds = require('./client_secret.json');

            var tempData=[];
            var aqData=[];
            var asData=[];

            async function accessSpreadsheet(){
                const doc = new GoogleSpreadsheet('1DghFM-X5N4cbvHXYiN5bLc5gYLOo2-V7QqyZfelq2vw');
                await promisify(doc.useServiceAccountAuth)(creds);
                const info = await promisify(doc.getInfo)();
                const sheet = info.worksheets[0];
                
                const rows = await promisify(sheet.getRows)({
                    offset: 1
                });

                rows.forEach( row => {
                    if(row.semipos > 0){
                        aqData.push({teamName:row.teamname,quarterPos:row.quarterpos,quarterScore:row.quarterscore,semiPos:row.semipos,semiScore:row.semiscore,finalPos:row.finalpos,finalScore:row.finalscore});
                    }
                    if(row.finalpos > 0){
                        asData.push({teamName:row.teamname,quarterPos:row.quarterpos,quarterScore:row.quarterscore,semiPos:row.semipos,semiScore:row.semiscore,finalPos:row.finalpos,finalScore:row.finalscore});
                    }
                    tempData.push({teamName:row.teamname,quarterPos:row.quarterpos,quarterScore:row.quarterscore,semiPos:row.semipos,semiScore:row.semiscore,finalPos:row.finalpos,finalScore:row.finalscore});
                })
            }

            accessSpreadsheet();

            this.listData = tempData;
            this.aqList = aqData;
            this.asList = asData;
        },
        loadDataB(){
            const GoogleSpreadsheet = require('google-spreadsheet');
            const { promisify } = require('util');

            const creds = require('./client_secret.json');

            var tempData=[];
            var aqData=[];
            var asData=[];

            async function accessSpreadsheet(){
                const doc = new GoogleSpreadsheet('1vCL8wCDDVVDHa34uvJX0Uc7eKI49OWQtdioEaUuUcII');
                await promisify(doc.useServiceAccountAuth)(creds);
                const info = await promisify(doc.getInfo)();
                const sheet = info.worksheets[0];
                
                const rows = await promisify(sheet.getRows)({
                    offset: 1
                });

                rows.forEach( row => {
                    if(row.semipos > 0){
                        aqData.push({teamName:row.teamname,quarterPos:row.quarterpos,quarterScore:row.quarterscore,semiPos:row.semipos,semiScore:row.semiscore,finalPos:row.finalpos,finalScore:row.finalscore});
                    }
                    if(row.finalpos > 0){
                        asData.push({teamName:row.teamname,quarterPos:row.quarterpos,quarterScore:row.quarterscore,semiPos:row.semipos,semiScore:row.semiscore,finalPos:row.finalpos,finalScore:row.finalscore});
                    }
                    tempData.push({teamName:row.teamname,quarterPos:row.quarterpos,quarterScore:row.quarterscore,semiPos:row.semipos,semiScore:row.semiscore,finalPos:row.finalpos,finalScore:row.finalscore});
                })
            }

            accessSpreadsheet();

            this.listData = tempData;
            this.aqList = aqData;
            this.asList = asData;
        },
        toggleA(){
            this.showA = true;
            this.showB = false;
            this.finals = false;
            this.loadDataA();
        },
        toggleB(){
            this.showA = false;
            this.showB = true;
            this.finals = false;
            this.loadDataB();
        },
        toggleF(){
            this.showA = false;
            this.showB = false;
            this.finals = true;
        },
    },
    beforeMount(){
        this.loadDataA();
    },
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
            #name{
                margin-top: 6px;
                margin-left: 4px;
                width:85%;
            }
            #score{
                margin-top: 6px;
                margin-right:4px;
            }
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
                display: flex;
            }
            #teamBox{
                display:flex;
                position:absolute;
                background-color: blue;
                height:5vh;
                margin-top: 5vh;
                width: 25%;
                margin-left:2vw;
                border-left: 5px solid #111;
                border-radius: 2px;
            }
            #teamBox1{
                display:flex;
                position:absolute;
                background-color: blue;
                height:5vh;
                margin-top: 10vh;
                width: 25%;
                margin-left:2vw;
                border-left: 5px solid #111;
            }
            #teamBox2{
                display:flex;
                position:absolute;
                background-color: blue;
                height:5vh;
                margin-top: 25.5vh;
                width: 25%;
                margin-left:2vw;
                border-left: 5px solid #111;
            }
            #teamBox3{
                display:flex;
                position:absolute;
                background-color: blue;
                height:5vh;
                margin-top: 30.5vh;
                width: 25%;
                margin-left:2vw;
                border-left: 5px solid #111;
            }
            #teamBox4{
                display:flex;
                position:absolute;
                background-color: blue;
                height:5vh;
                margin-top: 40vh;
                width: 25%;
                margin-left:2vw;
                border-left: 5px solid #111;
            }
            #teamBox5{
                display:flex;
                position:absolute;
                background-color: blue;
                height:5vh;
                margin-top: 45vh;
                width: 25%;
                margin-left:2vw;
                border-left: 5px solid #111;
            }
            #teamBox6{
                display:flex;
                position:absolute;
                background-color: blue;
                height:5vh;
                margin-top: 60.5vh;
                width: 25%;
                margin-left:2vw;
                border-left: 5px solid #111;
            }
            #teamBox7{
                display:flex;
                position:absolute;
                background-color: blue;
                height:5vh;
                margin-top: 65vh;
                width: 25%;
                margin-left:2vw;
                border-left: 5px solid #111;
            }
        }
        #semi{
            background-color: green;
            width:33.33%;
            #name{
                margin-top: 6px;
                margin-left: 4px;
                width:85%;
            }
            #score{
                margin-top: 6px;
                margin-right:4px;
            }
            #border{
                position: absolute;
                margin-top: 20vh;
                border-bottom: 2px solid #fff;
                border-top: 2px solid #ffffff;
                border-right: 2px solid #ffffff;
                height:35vh;
                width:33.33%
            }
            #teamBox{
                display:flex;
                position:absolute;
                background-color: blue;
                height:5vh;
                margin-top: 15vh;
                width: 25%;
                margin-left:4vw;
                border-left: 5px solid #111;
            }
            #teamBox1{
                display:flex;
                position:absolute;
                background-color: blue;
                height:5vh;
                margin-top: 20vh;
                width: 25%;
                margin-left:4vw;
                border-left: 5px solid #111;
            }
            #teamBox2{
                display:flex;
                position:absolute;
                background-color: blue;
                height:5vh;
                margin-top: 50vh;
                width: 25%;
                margin-left:4vw;
                border-left: 5px solid #111;
            }
            #teamBox3{
                display:flex;
                position:absolute;
                background-color: blue;
                height:5vh;
                margin-top: 55vh;
                width: 25%;
                margin-left:4vw;
                border-left: 5px solid #111;
            }
        }
        #finals{
            background-color: greenyellow;
            width:33.33%;
            #name{
                margin-top: 6px;
                margin-left: 4px;
                width:85%;
            }
            #score{
                margin-top: 6px;
                margin-right:4px;
            }
            #border{
                position: absolute;
                margin-top: 36vh;
                border-top: 2px solid #ffffff;
                border-right: 2px solid #ffffff;
                height:0vh;
                width:33.33%
            }
            #teamBox{
                display:flex;
                position:absolute;
                background-color: blue;
                height:5vh;
                margin-top: 31.5vh;
                width: 25%;
                margin-left:4vw;
                border-left: 5px solid #111;
            }
            #teamBox1{
                display:flex;
                position:absolute;
                background-color: blue;
                height:5vh;
                margin-top: 36.5vh;
                width: 25%;
                margin-left:4vw;
                border-left: 5px solid #111;
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

            tempList.push({teamName:this.listData[i].teamname,quarterPos:this.listData[i].quarterpos,quarterScore:this.listData[i].quarterscore,semiPos:this.listData[i].semipos,semiScore:this.listData[i].semiscore,finalPos:this.listData[i].finalpos,finalScore:this.listData[i].finalscore})
-->

