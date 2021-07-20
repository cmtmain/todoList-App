<template>
	<div class="container">
		<h1>欢迎使用LYT待办事项</h1>
		<todo-add @addTodo="addTodo" />
		<todo-filter :selected="filter" @changeFilter="id=>filter=id" />
		<todo-list :todos="filteredTodos" :selected="filter" @changeTarget="changeFilterTodos"
			@removeTodo="removeFilterItem"></todo-list>
	</div>
</template>

<script>
	import todoAdd from './components/todoAdd.vue'
	import todoFilter from './components/todoFilter.vue'
	import todoList from './components/todoList.vue'

	export default {
		name: 'App',
		data() {
			return {
				filter: 0,
				filteredTodos: [{
					id: 0,
					title: 'ToDo 1',
					target: false
				}, {
					id: 1,
					title: 'ToDo 2',
					target: false
				}, {
					id: 2,
					title: 'ToDo 3',
					target: false
				}]
			}
		},
		methods: {
			addTodo(item) {
				for (let i = 0; i < this.filteredTodos.length; i++) {
					if (!this.filteredTodos.some(item => item.id == i)) {
						item.id = i;
						break;
					}
				}
				item.id = item.id !== undefined ? item.id : this.filteredTodos.length;
				item.target = false;
				this.filteredTodos.push(item);
				localStorage.setItem('todolist', JSON.stringify(this.filteredTodos));
			},
			changeFilterTodos(id) {
				this.filteredTodos = this.filteredTodos.map(item => {
					if (item.id == id) item.target = !item.target;
					return item
				});
			},
			removeFilterItem(id) {
				this.filteredTodos = this.filteredTodos.filter(item => item.id != id);
			}
		},
		components: {
			todoAdd,
			todoFilter,
			todoList
		},
		mounted() {
			let data = JSON.parse(localStorage.getItem('todolist'));
			this.filteredTodos = data ? data : [];
		},
		beforeUpdate() {
			localStorage.setItem('todolist', JSON.stringify(this.filteredTodos));
		}
	}
</script>

<style lang="css">
	* {
		margin: 0;
		padding: 0;
		box-sizing: border-box;
	}

	body {
		height: 100vh;
		background-color: #CCCCFF;
	}

	input {
		border: none;
		outline: none;
	}

	#app {
		display: flex;
		align-items: center;
		justify-content: center;
		height: 100%;
		width: 100%;
	}

	.container {
		padding: 30px;
		display: flex;
		align-items: center;
		justify-content: space-evenly;
		flex-direction: column;
		min-width: 400px;
		width: 60%;
		max-width: 500px;
		height: 60vh;
		border-radius: 15px;
		box-shadow: #666666 0px 0px 10px 0px;
		background-color: rgb(250, 250, 250);
		;
	}

	.container>* {
		margin: 10px;
	}

	.container div {
		width: 100%;
	}
</style>
