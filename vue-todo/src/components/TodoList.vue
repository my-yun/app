<template>
	<div>
		<transition-group name="list" tag="ul">
			<li v-for="(todoItem, index) in propsdata" v-bind:key="todoItem.item" class="shadow">
				<i class="fa-regular fa-square-check checkBtn" v-bind:class="{checkBtnCompleted: todoItem.completed}" v-on:click="toggleComplete(todoItem, index)"></i>
				<span v-bind:class="{textCompleted: todoItem.completed}">{{ todoItem.item }}</span>
				<span class="removeBtn" v-on:click="removeTodo(todoItem, index)">
					<i class="fa-solid fa-trash"></i>
				</span>
			</li>
		</transition-group>
	</div>
</template>

<script>
export default {
	props:['propsdata'],
	methods: {
		removeTodo: function(todoItem, index){
			this.$emit('removeItem',todoItem, index);                                                                                                                                                                                        
		},
		toggleComplete: function(todoItem){
			
			todoItem.completed =!todoItem.completed;
			// 로컬 스토리지 데이터 갱신
			localStorage.removeItem(todoItem.item);
			localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
		}
	},
	
}
</script>

<style>
ul{
	list-style-type: none;
	padding-left: 0;
	margin-top: 0;
	text-align: left;
}
li{
	display: flex;
	min-height: 50px;
	height: 50px;
	line-height: 50px;
	margin:0.5rem 0;
	padding: 0 0.9rem;
	background:#fff;
	border-radius: 5px;
	align-items: center
}
.checkBtn {
	color:#696;
	margin-right: 5px;
}
.checkBtnCompleted{
	color:#999;
}
.textCompleted{
	text-decoration: line-through;
	color: #999;
}
.removeBtn {
	margin-left: auto;
	color:#333;	
}

.list-item {
	display: inline-block;
	margin-right: 10px;
}
.list-enter-active, .list-leave-active {
	transition: all 1s;
}
.list-enter-from, .list-leave-to /* .list-leave-active below version 2.1.8 */ {
	opacity: 0;
	transform: translateY(30px);
}
</style>