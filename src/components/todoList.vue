<template>
	<div class="todo-list">
		<div class="todo-item" v-for="item in todos" :key="item.id" v-show="flag(item.target)">
			<label @contextmenu.prevent="handleDown(item.id)">
				<input type="checkbox" @change="handleChange(item.id)" :checked="item.target">
				<span class="check-button"></span>
				<span>{{item.title}}</span>
			</label>
		</div>
	</div>
</template>

<script>
	export default {
		props: ['todos', 'selected'],
		methods: {
			handleChange(id) {
				this.$emit('changeTarget', id);
			},
			flag(a) {
				if (this.selected == 0) return true;
				else if (this.selected == 1) return a;
				else return !a;
			},
			handleDown(id){
				this.$emit('removeTodo',id);
			}
		}
	}
</script>

<style scoped>
	.todo-list {
		height: 310px;
		overflow-y: scroll;
	}

	.todo-list::-webkit-scrollbar {
		width: 5px;
	}

	.todo-list::-webkit-scrollbar-thumb {
		border-radius: 10px;
		background: rgba(0, 0, 0, 0.1);
	}

	.todo-item {
		width: 100%;
		margin-bottom: 10px;
		border-radius: 10px;
		background-color: white;
	}

	.check-button {
		margin-right: 5px;
		width: 20px;
		height: 20px;
		top: 50%;
		border: #CC99CC solid 1.5px;
		border-radius: 50%;
		box-shadow: inset white 0 0 0 3px;
	}

	label {
		display: flex;
		align-items: center;
		justify-content: flex-start;
		padding: 0 2.5%;
		width: 100%;
		margin: 0 auto;
		height: 45px;
		line-height: 45px;
	}

	input {
		display: none;
	}

	input:checked~.check-button {
		background-color: #CC99CC;
	}

	input:checked~span {
		text-decoration: line-through;
	}
</style>
