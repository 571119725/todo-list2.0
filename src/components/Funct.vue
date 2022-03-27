<template>
    <ul id='functlist' :style="{'visibility': (tasks.length>0? 'visible' : 'hidden')}">
        <li>
            <div class="function">
                <div><span :textContent='updateContent'></span><span> item left</span></div>
                <div>
                    <button id="button1" :class="clickfir ? 'showborder' : 'transparent'" @click='showAll'>All</button>
                    <button id="button2" :class="clicksec ? 'showborder' : 'transparent'" @click='showActive'>Active</button>
                    <button id="button3" :class="clickthr ? 'showborder' : 'transparent'" @click='showCompleted'>Completed</button>
                </div>
                <div><button id="clear" @click="$emit('clearTasks')" :style="{'visibility' : showClear}">Clear completed</button></div>
            </div>
        </li>
        <li class="shallow1" id="shallow1"></li>
        <li class="shallow2" id="shallow2"></li>
    </ul>
</template>
<script>
export default {
    name:'Funct',
    props:{
        tasks:Array,
        status:String
    },
    data(){
        return{
            clickfir:Boolean,
            clicksec:Boolean,
            clickthr:Boolean,
        }
    },
    computed:{
        updateContent:function(){
            let count=0
            this.tasks.forEach(element => {
                if(element.reminder==false){
                    count++;
                }
            });
            return count
        },
        showClear:function(){
            let state=0;
            this.tasks.forEach((element)=>{
                if(element.reminder==true){
                    state=1;
                }
            });
            if(state==1){
                return 'visible'
            }else{
                return 'hidden';
            }
        },
    },
    methods:{
        showAll(){
            this.clickfir=true;
            this.clicksec=false;
            this.clickthr=false;
            this.$emit('showChange','1');
        },
        showActive(){
            this.clickfir=false;
            this.clicksec=true;
            this.clickthr=false;
            this.$emit('showChange','2');
        },
        showCompleted(){
            this.clickfir=false;
            this.clicksec=false;
            this.clickthr=true;
            this.$emit('showChange','3');
        },
        
    },
    created(){
        switch(this.status){
            case '1':
                this.clickfir=true;
                this.clicksec=false;
                this.clickthr=false;
                break;
            case '2':
                this.clickfir=false;
                this.clicksec=true;
                this.clickthr=false;
                break;
            case '3':
                this.clickfir=false;
                this.clicksec=false;
                this.clickthr=true;
                break;
        }
    },
    emits:['clearTasks','showChange']
}
</script>
<style scoped>
ul{
    visibility: hidden;
    display: flex;
    flex-direction: column;
    align-items: center;
}
li{
    list-style-type: none;
}
.function{
    background-color: white;
    width: 690px;
    height: 40px;
    display:flex;
    justify-content: space-between;
    align-items: center;
    box-shadow: 0 5px 5px rgba(0,0,0,0.10),0 0px 0px rgba(0,0,0,0.10),0 5px 5px rgba(0,0,0,0.10),0 5px 5px rgba(0,0,0,0.10);
}
.function span{
    font-size:15px;
    color:#777777;
}
.function span:nth-child(1){
    margin-left: 20px;
}
button{
    text-align: center;
    background-color: white;
    color: #777777;
    margin: auto 10px;
    height:25px;
    line-height: 25px;
    padding:0px 10px;
    border:0.5px solid transparent;
}
.transparent{
    border:0.5px solid transparent;
}
.showborder{
    border: 0.5px solid #ead7d7;
}
.function button:hover{
    border: 0.5px solid #ead7d7;
}
.function div:nth-child(3){
    visibility: hidden;
}
/* .function div:nth-child(2) button:nth-child(1){
    border: 0.5px solid #ead7d7;
} */
.shallow1{
    margin-top: 1px;
    width:670px;
    height:6px;
    background-color: white;
    box-shadow: 0 5px 5px rgba(0,0,0,0.10),0 5px 5px rgba(0,0,0,0.10),0 5px 5px rgba(0,0,0,0.10),0 5px 5px rgba(0,0,0,0.10);
}
.shallow2{
    margin-top: 1px;
    width:650px;
    height:6px;
    background-color: white;
    box-shadow: 0 5px 5px rgba(0,0,0,0.10),0 5px 5px rgba(0,0,0,0.10),0 5px 5px rgba(0,0,0,0.10),0 5px 5px rgba(0,0,0,0.10);
}
</style>