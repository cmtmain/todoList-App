<template>
	<div class="input-add">
		<input type="text" v-model="todo" @keypress.enter="handelAdd" />
		<button @click="handelAdd"></button>
	</div>
</template>

<script>
	export default {
		data() {
			return {
				todo: ''
			}
		},
		methods: {
			handelAdd() {
				if (this.todo === '') return;
				this.$emit('addTodo', {
					title: this.todo
				});
				this.todo = '';
			}
		}
	}
</script>

<style scoped>
	.input-add {
		position: relative;
		height: 50px;
		border-radius: 25px;
		overflow: hidden;
		box-shadow: #aaa 0 0 10px 0;
	}

	input {
		position: absolute;
		left: 50%;
		transform: translateX(-50%);
		padding-left: 15px;
		padding-right: 50px;
		font-size: 20px;
		width: 100%;
		min-height: 50px;
		line-height: 50px;
	}

	button {
		position: absolute;
		top: 50%;
		right: 2px;
		transform: translateY(-50%);
		width: 46px;
		height: 46px;
		border: none;
		border-radius: 50%;
		background: linear-gradient(to bottom, #e66465, #9198e5);
	}

	button::after,
	button::before {
		content: "";
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
		background-color: white;
	}

	button::before {
		width: 2px;
		height: 50%;
	}

	button::after {
		width: 50%;
		height: 2px;
	}
</style>
