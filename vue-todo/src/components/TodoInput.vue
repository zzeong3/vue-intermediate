<template>
    <div class="inputBox shadow">
        <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo">
        <span class="addContainer" v-on:click="addTodo">
            <i class="fas fa-plus addBtn"></i>
        </span>

        <AlertModal v-if="showModal" @close="showModal = false">
            <h3 slot="header">경고
                <i class="fas fa-times closeModalBtn" @click="showModal = false"></i>
            </h3>
            <div slot="body">무엇가를 입력하세요</div>
            <div slot="footer">copy right</div>
        </AlertModal>
    </div>
</template>

<script>
import AlertModal from './common/AlertModal.vue'

export default {
    data() {
        return {
            newTodoItem: "",
            showModal: false,
        }
    },
    methods: {
        addTodo() {
            if (this.newTodoItem !== '') {
                this.$store.commit('addOneItem' , this.newTodoItem);
                this.clearInput();
            }  else {
                this.showModal = !this.showModal;
            }
        },
        clearInput() {
            this.newTodoItem= '';
        }
    },
    components: {
       AlertModal
    }
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
    width:auto;
}

.addContainer {
    float: right;
    background: linear-gradient(to right, #6478FB, #8763FB);
    display: block;
    width: 3rem;
    border-radius: 0 5px 5px 0;
}

.addBtn {
    color: white;
    vertical-align: middle;
}

.closeModalBtn {
    color: #42b983;
}
</style>