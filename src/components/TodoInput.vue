<template>
    <div class="inputBox shadow">
        <input type ="text" v-model="newTodoItem" placeholder="Type what you have to do" v-on:keyup.enter="addTodo">
        <span class="addContainer" v-on:click="addTodo">
            <i class="addBtn fa fa-plus" aria-hidden="true"></i>
        </span>
        <modal :show="showModal" @close="close">
            <h3 slot="header">경고</h3>
            <span slot="body">
                할일을 입력하세요
            </span>
            <i slot="footer" class="closeModalBtn fa fa-times" aria-hidden="true" @click = "showModal = false"></i>
        </modal>
    </div>
</template>

<script>
import Modal from './common/Modal.vue'

export default {
    data(){
        return{
            newTodoItem: '',
            showModal: false
        }
    },
    methods: {
        addTodo() {
            if(this.newTodoItem !== ""){
                var value = this.newTodoItem && this.newTodoItem.trim();
                this.$emit('addTodo', value);
                this.clearInput();
            } else {
                console.log('에러모달');
                this.showModal = !this.showModal;
                console.log('this.showModal' , this.showModal);
            }
        },
        clearInput() {
            this.newTodoItem = '';
        },
        close(){
            console.log('close');
            this.showModal = false;
        }
    },
    components: {
        Modal: Modal,
    },
}
</script>

<style scoped>
    input:focus {
        outline: none;
    }
    .inputBox {
        background: white;
        height: 50px;
        line-height: 50px;
        border-radius: 5px;
    }
    .inputBox input {
        border-style: none;
        font-size: 0.9rem;
    }
    .addContainer {
        float: right;
        background: linear-gradient(to right, #6478FB , #8763FB);
        display: inline-block;
        width: 3rem;
        border-radius: 0 5px 5px 0;
    }
    .addBtn {
        color : white;
        vertical-align: middle;
    }
</style>
