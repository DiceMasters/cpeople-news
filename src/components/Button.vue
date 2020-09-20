<template>
	<button
		class="button"
		@click="clickHandler"
	>
		<slot></slot>
	</button>
</template>

<script>
export default {
	methods: {
		clickHandler() {
			this.$emit('click')
		}
	}
}
</script>

<style lang="less">
.button {
	min-height: 50px;
	display: flex;
	align-items: center;
	justify-content: center;
	background-color: gray;
	font-weight: bold;
	font-size: 18px;
	line-height: 25px;
	color: white;
	padding: 12px 52px;
	border: none;
	border-radius: 100px;
	transition: opacity .3s;
	cursor: pointer;

	&:hover { opacity: .75; }
	&:focus { outline: none; }

	&_pink { background-color: #FF6C6C; }
}
</style>