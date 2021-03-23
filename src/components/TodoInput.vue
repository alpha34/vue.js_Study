<template>
    <div class="inputBox shadow">
     <!-- v-model : 폼에서 주로 사용되는 속성, 폼에 입력한 값을 뷰 인스턴스의 데이터와 즉시 동기화 -->
    <input type="text" v-model="newTodoItem" placeholder="Type what you have to do" v-on:keyup.enter="addTodo">
    <span class="addContainer" v-on:click="addTodo">
        <i class="addBtn fas fa-plus" aria-hidden="true"></i>
    </span> 
    <!-- <button v-on:click="addTodo">추가</button> -->    

    <!-- 모달 추가 -->
    <modal v-if="showModal" @close="showModal = false">
      <h3 slot="header">경고</h3>
      <span slot="footer" @click="showModal = false">할 일을 입력하세요.
        <i class="closeModalBtn fas fa-times" aria-hidden="true"></i>
      </span>
    </modal>

    </div>
</template>

<script>
import Modal from './common/Modal.vue'


export default {
    data(){
        return{
            newTodoItem:'',
            showModal:false
        }
    },
    methods: {
        addTodo(){
            //예외처리코드 추가
            if(this.newTodoItem !== ""){
                var value = this.newTodoItem && this.newTodoItem.trim();  //앞뒤 공백 문자 제거
                this.$emit('addTodo', value);  //
                //console.log(this.newTodoItem);
                //localStorage.setItem(value,value);
                this.clearInput();  //인풋 박스 입력값 초기화
            }else{
                this.showModal = !this.showModal; //텍스트 미입력시 모달 동작
            }
        },
        clearInput(){
            this.newTodoItem ='';
        }
    },
    components:{ //모달 컴포넌트 등록
        Modal : Modal 
    }    
}
</script>

<style>
    input:focus{
        outline:none;
    }
    .inputBox{
        background:white;
        height: 50px;
        line-height: 50px;
        border-radius: 5px;
    }
    .inputBox input{
        border-style: none;
        font-size: 0.9rem;
    }
    .addContainer{
        float: right;
        background: linear-gradient(to right, #6478FB, #8763FB);
        display: block;
        width: 3rem;
        border-radius: 0 5px 5px 0;
    }
    .addBtn{
        color: white;
        vertical-align: middle;
    }
</style>