<template>
    <section>
        <transition-group name="list" tag="ul">
            <li v-for="(todoItem, index) in propsdata" v-bind:key="todoItem" class="shadow">
                <i class="checkBtn fas fa-check" aria-hidden="true"></i>
                {{todoItem}}
                <span class="removeBtn" type="button" v-on:click="removeTodo(todoItem, index)">
                    <i class="far fa-trash-alt" alria-hidden="true"></i>
                </span>
             </li>
        </transition-group>
    </section>
</template>
    
<script>
export default {
    props:['propsdata'],
    methods: {
        removeTodo(todoItem, index){  //뷰의 특성상 데이터 속성이 변화면 화면에 즉시 반영하므로 자동 갱신함.
            //localStorage.removeItem(todoItem);
            //this.todoItems.splice(index,1); //splice() 자바스크립트 내장함수 배열 특정 인덱스 삭제 
           // console.log(todoItem, index); 
           this.$emit('removeTodo2',todoItem, index);
        }
    },
}
</script>

<style>
    ul{
        list-style-type: none; /* 목록아이템 스타일 지정 */
        padding-left: 0px;
        margin-top: 0;
        text-align: left;
    }
    li{
        display: flex; /* 비율 기준의 레이아웃 방식인 flex로 지정 */
        min-height: 50px;
        height: 50px;
        line-height: 50px;
        margin: 0.5rem 0;
        padding: 0 0.9rem;
        background: white;
        border-radius: 5px;
    }

    .checkBtn{
        line-height: 45px;
        color: #62acde;
        margin-left: 5px;
    }

    .removeBtn{
        margin-left: auto;
        color: #de4343;
    }

</style>

<style scoped>
    .list-enter-active, .list-leave-active{
        transition: all ls;
    }
    .list-enter, .list-leave-to{
        opacity: 0;
        transform: translateY(30px);
    }
</style>