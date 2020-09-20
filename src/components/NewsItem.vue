<template>
	<div class="news_list_item">
		<div class="news_card">
			<div class="news_card_image">
				<img :src="url + 'thumbnails/' + image" alt="">
			</div>
			<div class="news_card_title">
				<p>{{ title }}</p>
			</div>
			<div class="news_card_excerpt">
				<p>{{ excerpt }}</p>
			</div>
			<div class="news_card_date">
				<span>{{ date }}</span>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	props: ['image', 'title', 'excerpt', 'date'],
	computed: {
		url() {
			return (process.env.NODE_ENV == 'production') ? '/assets/images/' : ''
		}
	}
}
</script>

<style lang="less">
.news {
	&_list_item {
		max-width: calc(100% / 3);
		display: flex;
		flex-direction: column;
		align-items: stretch;
		flex-basis: calc(100% / 3);
		flex-grow: 0;
		flex-shrink: 0;
		padding-bottom: 81px;
		position: relative;

		@media screen and (max-width: 940px) {
			max-width: calc(100% / 2);
			flex-basis: calc(100% / 2);
		}
		@media screen and (max-width: 688px) {
			max-width: 100%;
			flex-basis: 100%;
			padding-bottom: 41px;
		}

		&:not(:nth-child(3n + 3)) {
			.news_card {
				padding-right: 20px;

				@media screen and (max-width: 940px) { padding-right: 0; }
				@media screen and (max-width: 688px) { padding-right: 0; }
			}
		}

		&:not(:nth-child(2n + 2)) {
			.news_card {
				@media screen and (max-width: 940px) { padding-right: 40px; }
				@media screen and (max-width: 688px) { padding-right: 0; }
			}
		}

		&:not(&--withoutBB):before {
			content: '';
			width: 100%;
			border-bottom: 1px dashed #333;
			position: absolute;
			bottom: 40px;
			left: 0;
			opacity: .4;

			@media screen and (max-width: 688px) { bottom: 20px; }
		}
	}

	&_card {
		flex-grow: 1;

		&_image {
			height: 220px;
			border-radius: 10px;
			margin-bottom: 15px;
			overflow: hidden;

			@media screen and (max-width: 1024px) { height: 210px; }
			@media screen and (max-width: 940px) { height: 220px; }
			@media screen and (max-width: 688px) { height: 195px; }

			img {
				width: 100%;
				height: 100%;
				object-fit: cover;
				object-position: center;
			}
		}

		&_title {
			margin-bottom: 15px;

			p {
				font-weight: 600;
				font-size: 24px;
				line-height: 30px;
				color: #333;

				@media screen and (max-width: 688px) { font-size: 20px; }
			}
		}

		&_excerpt {
			margin-bottom: 15px;

			p {
				font-weight: 300;
				font-size: 18px;
				line-height: 24px;
				letter-spacing: -0.02em;

				@media screen and (max-width: 688px) {
					font-size: 16px;
					line-height: 22px;
					letter-spacing: -0.01em;
				}
			}
		}

		&_date {
			span {
				font-weight: 300;
				font-size: 12px;
				line-height: 15px;
				letter-spacing: -0.01em;
				opacity: 0.5;
			}
		}
	}
}
</style>