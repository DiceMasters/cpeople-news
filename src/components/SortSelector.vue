<template>
	<div class="sort_selector">
		<div class="sort_selector_current" @click="toggleList">{{ getCurrentSelector }}</div>
		<div class="sort_selector_list" :class="{ active: isListOpened }">
			<div
				class="sort_selector_list_item"
				v-for="(item, index) in selectors"
				:key="index"
				@click="changeCurrent(index)"
			>
				{{ item.title }}
			</div>
		</div>
	</div>
</template>

<script>
export default {
	props: {
		selectors: {
			type: Array,
			default() {
				return []
			}
		},
		start: {
			type: Number,
			default: 0
		}
	},
	data() {
		return {
			current: 0,
			isListOpened: false,
		}
	},
	mounted() {
		this.current = this.start
		this.$emit('input', this.selectors.find( (val, i) => i === this.current))

		document.addEventListener('click', e => {
			if (!e.target.closest('.sort_selector')) {
				this.closeList()
			}
		})
	},
	methods: {
		changeCurrent(index) {
			let current = this.selectors.find( (val, i) => i === index)

			this.current = index
			this.closeList()

			this.$emit('input', current)
			this.$emit('reset')
		},
		toggleList() {
			this.isListOpened = !this.isListOpened
		},
		closeList() {
			this.isListOpened = false
		}
	},
	computed: {
		getCurrentSelector() {
			return this.selectors[this.current].title
		}
	}
}
</script>

<style lang="less">
.sort {
	&_selector {
		position: relative;

		&_current {
			font-weight: 600;
			font-size: 18px;
			line-height: 25px;
			letter-spacing: -0.02em;
			padding-right: 20px;
			position: relative;
			cursor: pointer;

			&:after {
				content: '';
				width: 12px;
				height: 7px;
				background-image: url("data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTIiIGhlaWdodD0iOCIgdmlld0JveD0iMCAwIDEyIDgiIGZpbGw9Im5vbmUiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyI+CjxwYXRoIGQ9Ik0xIDFMNiA2TDExIDEiIHN0cm9rZT0iIzE2MTUxNSIgc3Ryb2tlLXdpZHRoPSIyIi8+Cjwvc3ZnPgo=");
				background-size: contain;
				background-repeat: no-repeat;
				background-position: center;
				position: absolute;
				top: 10px;
				right: 0;
				transform-origin: center;
				transition: transform .3s;
			}

			&:hover {
				color: #FF6C6C;

				&:after { background-image: url("data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTIiIGhlaWdodD0iOCIgdmlld0JveD0iMCAwIDEyIDgiIGZpbGw9Im5vbmUiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyI+CjxwYXRoIGQ9Ik0xIDFMNiA2TDExIDEiIHN0cm9rZT0iI0ZGNkM2QyIgc3Ryb2tlLXdpZHRoPSIyIi8+Cjwvc3ZnPgo="); }
			}

			&.active:after { transform: rotate(180deg); }
		}

		&_list {
			width: 100%;
			display: none;
			flex-direction: column;
			align-items: stretch;
			background-color: white;
			position: absolute;
			top: calc(100% + 3px);
			left: 0;
			z-index: 1;

			&.active { display: flex; }

			&_item {
				font-weight: normal;
				background-color: #fff;
				padding: 5px 7px;
				cursor: pointer;

				&:hover { background-color: rgba(0, 0, 0, .1); }
			}
		}
	}
}
</style>