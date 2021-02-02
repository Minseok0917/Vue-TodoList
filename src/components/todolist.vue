<template>
    <div class="todolist">
        <h1>TodoList</h1>
        <input type="text" v-model="inputValue" @keydown="keydown">
        <div class="todoContent">
            <div v-for="(data,index) in state" :key="index" :data-idx="index">
                <span :class="{ active : data.isActive }" @click="ActiveClick" >{{data.value}}</span>
                <button @click="DeleteClick">X</button>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data:function(){
        return {
            state:[],
            inputValue:""
        };
    },
    methods:{
        keydown:function(event){
            const {target,keyCode} = event;
            const value = target.value;
            const success = [9,13].includes(keyCode);
            if( success ){
                event.preventDefault();
                if( value ){
                    this.state = [...this.state,{
                        value:value,
                        isActive:false
                    }];
                    this.inputValue = "";
                }
            }
        },
        ActiveClick:function(event){
            const parent = event.target.parentNode;
            const index = parent.getAttribute("data-idx");
            this.state[index].isActive = !this.state[index].isActive;
        },
        DeleteClick:function(event){
            const parent = event.target.parentNode;
            const index = parent.getAttribute("data-idx");
            this.state.splice(index,1);
        }
    }
}
</script>

<style>
    .todoContent>div>span.active{ text-decoration: line-through;}
</style>