<template>
	<div>
		<ul>
			<li v-for="todoItem in todoItems" v-bind:key="todoItem" class="shadow">
				{{ todoItem }}
				<span class="removeBtn">
					<i class="fa-solid fa-trash"></i>
				</span>
			</li>
		</ul>
	</div>
</template>

<script>
export default {
	data: function() {
		return {
			todoItems: []
		}
	}, 
	created: function(){
		if(localStorage.length>0){
			for(var i = 0; i < localStorage.length; i++){
				if(localStorage.key(i) !== 'loglevel:webpack-dev-version'){
					this.todoItems.push(localStorage.key(i));
				}
			}
		}
	}
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
}
.checkBtn {
	line-height: 45px;
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
.removeBtn i{
	line-height: 50px;
}
</style>