<template>
	<div class="sort_group">
		<slot></slot>
	</div>
</template>

<style lang="less">
.sort {
	&_group {
		display: flex;
		flex-wrap: wrap;
		padding-bottom: 60px;

		@media screen and (max-width: 688px) { padding-bottom: 40px; }

		.sort_selector:not(:last-child) {
			margin-right: 75px;

			@media screen and (max-width: 1024px) { margin-right: 67px; }
			@media screen and (max-width: 940px) { margin-right: 69px; }
			@media screen and (max-width: 688px) { margin-right: 63px; }
		}
	}
}
</style>