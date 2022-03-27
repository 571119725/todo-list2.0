<template>
    <form target="#" >
        <div id='chooseAll' @click='chooseAll' :style="{'visibility': (tasks.length>0? 'visible' : 'hidden')}">
            <img :src="showChooseAll ?'/images/cu.png' : '/images/xi.png'" alt="下拉">
        </div>
        <label>
            <input v-model='text' @keydown="addTask(e)" autocomplete="off" type="text" placeholder="What need to be done?" name="todo">
        </label>
    </form>
</template>
<script>
export default{
    name:'InputBox',
    props:{
        tasks:Array,
    },
    data(){
        return{
            id:'',
            text:'',
            reminder:false
        }
    },
    methods:{
        chooseAll(){
            if(this.choose==false){
                this.choose=!this.choose;
                this.$emit('chooseAll','1');
            }else{
                this.choose=!this.choose;
                this.$emit('chooseAll','2');
            }
        },
        addTask(e){
            if (!e)
                e = window.event;//火狐中是 window.event
            if ((e.keyCode || e.which) == 13) {
                e.preventDefault();
                if(this.text.trim()!=''){
                    const newTask={
                        id: Math.floor(Math.random()*100000),
                        text: this.text.trim(),
                        reminder:false
                    };
                    this.text='';
                    this.$emit('add-task',newTask);
                }
            }
        },
    },
    computed:{
        showChooseAll(){
            let state=1;
            this.tasks.forEach(element => {
                if(element.reminder==false){
                    state=0;
                }
            });
            if(state==1){
                return true;
            }else{
                return false;
            }
        }
    }
}
</script>
<style scoped>
form{
    background-color:white ;
    display: flex;
    width: 690px;
    height: 60px;
    box-shadow: 0 0px 0px rgba(0,0,0,0.10),0 5px 5px rgba(0,0,0,0.10),0 5px 5px rgba(0,0,0,0.10),0 5px 5px rgba(0,0,0,0.10);
}
div{
    visibility: hidden;
    display:flex;
    flex-direction: column;
    justify-content: center;
}
img{
    max-width:30px;
    margin:auto 10px;
}
input{
    font-size: 20px;
    outline: none;
    width:640px;
    height:60px;
    border: 0px;
}
input::-webkit-input-placeholder {
    color:#ead7d7;
    font-style: italic;
    font-size: 20px;
}
</style>