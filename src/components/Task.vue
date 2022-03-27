<template>
    <li class="showarea" :id='task.id'  @mouseover="ifshow=true" @mouseout="ifshow=false" :style="{'display': showChange}">
        <div class='choose' @click='choose'>
            <img :src='task.reminder ? "/images/xuanzhong.png" : "/images/weixuanzhong.png"' alt='是否选中'>
        </div>
        <input v-model='singleTask.text' @blur="check" :class="task.reminder ? 'deletedata' : 'showdata'" readonly ondblclick='this.readOnly=false' onchange='this.readOnly=true'>   
        <div class='delete' @mouseover="ifcu=true" @mouseout="ifcu=false" @click='deletetask' :style="{'visibility': (ifshow ? 'visible' : 'hidden')}"> 
            <img :src="ifcu ? '/images/cushanchu.png' : '/images/xishanchu.png'" alt='删除键'>
        </div>
    </li>
</template>
<script>
export default {
    name:'Task',
    props:{
        task:Object,
        status:String,
    },
    data(){
        return{
            singleTask:this.task,
            ifshow:false,
            ifcu:false
        }
    },
    computed:{
        showChange(){
            let style;
            switch(this.status){
                case '1':
                    style='flex';
                    break;
                case '2':
                    if(this.task.reminder==false){
                        style='flex';
                    }else{
                        style='none';
                    }
                    break;
                case '3':
                    if(this.task.reminder==true){
                        style='flex';
                    }else{
                        style='none';
                    }
                    break;
                default:
                    break;
            }
            return style;
        }
    },
    methods:{
        choose(){
            this.$emit('choose',this.task.id);
        },
        deletetask(){
            this.$emit('deleteTask',this.task.id);
        },
        check(){
            if(this.task.text==''){
                    this.$emit('deleteTask',this.task.id)
            }
        }
    }
}
</script>
<style scoped>
.show{
    display: flex;
}
.hide{
    display: none;
}
li{
    margin:2px auto;
    background-color:white ;
    display: flex;
    width: 690px;
    height: 60px;
    box-shadow: 0 0px 0px rgba(0,0,0,0.10),0 5px 5px rgba(0,0,0,0.10),0 5px 5px rgba(0,0,0,0.10),0 5px 5px rgba(0,0,0,0.10);
}
.showdata {
    transition:all 0.5s;
    font-size: 20px;
    outline: none;
    width:600px;
    height:60px;
    border: 0px;
    text-decoration: none;
    color: black;
}
.deletedata {
    transition:all 0.5s;
    font-size: 20px;
    outline: none;
    width:600px;
    height:60px;
    border: 0px;
    text-decoration: line-through;
    color:#ead7d7;
}
.choose{
    display:flex;
    flex-direction: column;
    justify-content: center;
}
.choose img{
    max-width:30px;
    margin:auto 10px;
}
.delete{
    visibility: hidden;
    display:flex;
    flex-direction: column;
    justify-content: center;
}
.delete img{
    max-width:20px;
    margin:auto 10px;
}
</style>