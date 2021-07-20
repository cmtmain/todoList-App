<template>
	<div class="filters">
		<span :class="selected==0?'active':''" @click="handleClick(0)">全部</span>
		<span :class="selected==1?'active':''" @click="handleClick(1)">已完成</span>
		<span :class="selected==2?'active':''" @click="handleClick(2)">未完成</span>
	</div>
</template>

<script>
	export default {
		props: ['selected'],
		methods:{
			handleClick(id){
				this.$emit('changeFilter',id);
			}
		}
	}
</script>

<style lang="css" scoped>
	.filters {
		display: flex;
		align-items: center;
		justify-content: space-evenly;
	}

	span {
		flex: 1;
		color: #aaa;
		text-align: center;
	}

	.active {
		color: black;
		font-size: 19px;
	}
</style>
