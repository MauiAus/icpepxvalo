<template>
    <div id="schedBody">
        <div id="schedBox" v-for="list in schedList" :key="list.index">
            <div v-if="list.id > 0">
                <div id="topBox" v-if="dateCheck(list.date)">
                    <p id="day">{{list.day}} - </p>
                    <p id="date">{{list.date}}</p>
                </div>
                <div id="botBox">
                    <h1 id="time">{{list.time}}</h1>
                    <p id="teama">{{list.teama}}</p>
                    <p id="score">{{list.ascore}}-{{list.bscore}}</p>
                    <p id="teamb">{{list.teamb}}</p>
                    <p id="type">{{list.type}}</p>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name:"Schedule",
    data(){
        return{
            schedList:[],
            dateTemp:"",
            emptyCheck:"",
        }
    },
    methods:{
        loadData(){
            this.$http.get('https://icpepvaloact2.firebaseio.com/Mastersheet.json').then(function(data){
                return data.json();
            }).then(function(data){
                var tempArr= [];
                for(let key in data){
                    tempArr.push(data[key]);
                }
                console.log(tempArr.length)
                for(let i = 1; i < tempArr.length; i++){
                    this.schedList.push({id:tempArr[i].Id,day:tempArr[i].Day,date:tempArr[i].Date,time:tempArr[i].Time,teama:tempArr[i].Teama,ascore:tempArr[i].Ascore,bscore:tempArr[i].Bscore,teamb:tempArr[i].Teamb,type:tempArr[i].Type});
                }
                console.log(this.schedList)
            })
        },
        dateCheck(date){
            if(this.dateTemp == ""){
                this.dateTemp = date;
            }
            else{
                if(this.dateTemp == date){
                    return false;
                }
                else{
                    this.dateTemp = date;
                    return true;
                }
            }
        },
        indexCheck(i){
            if(i > 0){
                return true;
            }
            else{
                return false;
            }
        }
    },
    created(){
        this.loadData();
    },
}
</script>

<style lang="scss" scoped>
#schedBox{
    float:left;
    width:100%;
    display:grid;
    #topBox{
        display:flex;
        background-color:burlywood;
        padding-left: 5%;
        padding-right:5%;
        #day{
            font-weight: bold;
        }
    }
    #botBox{
        padding-left: 5%;
        padding-right:5%;
        background-color: cadetblue;
        display:flex;
        min-height: 10vh;
        max-height: 20vh;
        p{
            text-align: center;
        }
        #time{
            width:20%;
            margin:auto;
        }
        #teama{
            width:20%;
            margin:auto;
        }
        #score{
            width:20%;
            margin:auto;
        }
        #teamb{
            width:20%;
            margin:auto;
        }
        #type{
            width:20%;
            margin:auto;
            text-align: right;
        }
    }
}
</style>


<!--
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
                    tempData.push({id:row.id,day:row.day,date:row.date,time:row.time,teama:row.teama,ascore:row.ascore,bscore:row.bscore,teamb:row.teamb,type:row.type});
                })


            }
            accessSpreadsheet();
            this.schedList = tempData;

-->

