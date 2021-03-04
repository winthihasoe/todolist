<template>
    <div class="to-do" :class="{done:toDoList.done}">
        <div class="flexing">
            <div>
                <h5 @click="showDetail=!showDetail">{{toDoList.title}}</h5>
                <h6 v-if="showDetail">{{toDoList.title}}</h6>
            </div>
            <div>
                <span class="material-icons" @click="remove">
                delete_outline
                </span>
                <span class="material-icons">
                edit
                </span>
                <span class="material-icons" @click="done">
                done_outline
                </span>
        </div>
        </div>
        

    </div>
</template>

<script>
export default {
    props:["toDoList"],
    data(){
        return {
            showDetail:false,
            path:"http://localhost:3000/toDoLists/"
        }
    },
    methods:{
        remove(){
            let removePath=this.path+this.toDoList.id;
            fetch(removePath,{method:"DELETE"})
            .then(()=>{
                this.$emit("remove",this.toDoList.id);
            })
            .catch((err)=>{
                console.log(err);
            })
        },
        done(){
            let donePath=this.path+this.toDoList.id;
            fetch(donePath,{
                 method:"PATCH",
                headers:{
                    "Content-Type":"application/json"
                },
                body:JSON.stringify(
                    {
                        done:!this.toDoList.done
                    }
                )
            })
            .then(()=>{
                this.$emit("done",this.toDoList.id)
            })
            .catch((err)=>{
                console.log(err)
            })
        }
    }
}
</script>

<style>
    .to-do{
        background-color: rgb(219, 215, 215);
        padding: 20px;
        margin: 20px auto;
        border: none;
        border-left: crimson 4px solid;
        border-radius: 10px;
        color: grey;
        box-shadow: 3px 3px #c4c0c0;
        
    }
    h5{
        cursor: pointer;
    }
    .flexing{
        display: flex;
        align-items: center;
        justify-content: space-between;
    }
    span{
        cursor: pointer;
    }
    .done{
        border-color: gold;
    }
</style>