<template>
	<div class="news">
		<div class="news_list">
			<slot name="list"></slot>
		</div>
		<div class="news_controlls">
			<slot name="controlls"></slot>
		</div>
	</div>
</template>

<style lang="less">
.news {
	display: flex;
	flex-direction: column;
	align-items: stretch;

	&_list {
		display: flex;
		flex-wrap: wrap;
		align-items: stretch;
		margin-bottom: -21px;
		position: relative;

		@media screen and (max-width: 688px) { margin-bottom: -1px; }

		&:after {
			content: '';
			width: 100%;
			height: 3px;
			background-color: white;
			position: absolute;
			bottom: 39px;
			left: 0;

			@media screen and (max-width: 688px) { bottom: 18px; }
		}
	}

	&_controlls {
		display: flex;
		justify-content: center;

		@media screen and (max-width: 688px) {
			flex-direction: column;
			align-items: stretch;
		}
	}
}
</style>