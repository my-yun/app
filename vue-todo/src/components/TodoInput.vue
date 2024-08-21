<template>
	<div class="inputBox shadow">
		<input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo">
		<!-- <button v-on:click="addTodo">add</button> -->

		<span class="addContainer" v-on:click="addTodo">
			<i class="fa-solid fa-plus addBtn"></i>
		</span>

		<!-- <button id="show-modal" @click="showModal = true">Show Modal</button> -->
		<!-- use the modal component, pass in the prop -->
		<Modal v-if="showModal" @close="showModal = false">
			<template v-slot:header>
				<h3>경고!</h3>
				<i class="closeModalBtn fa-solid fa-xmark" v-on:click="showModal=false"></i>
			</template>
			<template v-slot:body>
				<p>할 일을 입력하세요.</p>
			</template>
		</Modal>
	</div>
</template>

<script> 
import Modal from './common/TodoModal.vue';
export default {
	data:function(){
		return{
			newTodoItem: "",
			showModal: false
		}
	},
	methods: {
		addTodo:function(){
			console.log(this.newTodoItem);

			if(this.newTodoItem !== ''){
				this.$emit('addTodoItem', this.newTodoItem);
				this.clearInput();
			}else{
				this.showModal = !this.showModal;
				// alert('내용을 입력해 주세요.');
			}
			
		},
		clearInput: function(){
			this.newTodoItem = "";
		}
	},
	components: {
		Modal:Modal
	}
}
</script>

<style scoped>
input:focuse{
	outline:none;
}
.inputBox {
	background:#fff;
	height: 50px;
	line-height: 50px;
	border-radius: 5px;
}
.inputBox input {
	border-style: none;
	font-size: 0.9rem;
	height: 100%;
	width: 75%;
	padding:0 10px;
	box-sizing: border-box;
}
.inputBox input:focus{
	outline: none;
}
.addContainer {
	float: right;
	background:linear-gradient(to right, #e2e4ea, #9c9da3);
	display: block;
	width: 3rem;
	height: 50px;
	border-radius: 0 5px 5px 0;;
}
.addBtn{
	color:#fff;
	vertical-align: middle;
	line-height: 50px;
}

.modal-enter {
  opacity: 0;
}

.modal-leave-active {
  opacity: 0;
}

.modal-enter .modal-container,
.modal-leave-active .modal-container {
  -webkit-transform: scale(1.1);
  transform: scale(1.1);
}
.closeModalBtn{
	position: absolute;
    top: 10px;
    right: 10px;
    font-size: 1.5rem;
    color: #000;
    cursor: pointer;
}
</style>