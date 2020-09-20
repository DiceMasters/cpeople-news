<template>
	<div id="app">
		<SortGroup>
			<SortSelector :selectors="years" v-model="selectorYear" @reset="resetMoreNews" />
			<SortSelector :selectors="months" v-model="selectorMonths" :start="12" @reset="resetMoreNews" />
		</SortGroup>
		<NewsList>
			<template v-slot:list>
				<NewsItem
					v-for="(item, index) in getCountedNews"
					:key="index"
					:image="item.image"
					:title="item.title"
					:excerpt="item.text"
					:date="item.date"
				/>
			</template>
			<template v-slot:controlls>
				<Button class="button_pink" v-if="!isAllNewsViewed" @click="loadMoreNews">загрузить еще</Button>
			</template>
		</NewsList>
	</div>
</template>

<script>
import SortGroup from './components/SortGroup'
import SortSelector from './components/SortSelector'
import Button from './components/Button'
import NewsList from './components/NewsList'
import NewsItem from './components/NewsItem'

export default {
	name: 'App',
	components: { SortGroup, SortSelector, Button, NewsList, NewsItem },
	data() {
		return {
			years: [
				{ title: '2019 год', val: 2019 },
				{ title: '2018 год', val: 2018 },
				{ title: '2017 год', val: 2017 },
				{ title: '2016 год', val: 2016 }
			],
			months: [
				{ title: 'Январь', val: 'jan' },
				{ title: 'Февраль', val: 'feb' },
				{ title: 'Март', val: 'mar' },
				{ title: 'Апрель', val: 'apr' },
				{ title: 'Май', val: 'may' },
				{ title: 'Июнь', val: 'jun' },
				{ title: 'Июль', val: 'jul' },
				{ title: 'Август', val: 'aug' },
				{ title: 'Сентябрь', val: 'sep' },
				{ title: 'Октябрь', val: 'okt' },
				{ title: 'Ноябрь', val: 'nov' },
				{ title: 'Декабрь', val: 'dec' },
				{ title: 'Все месяцы', val: 'all' }
			],
			selectorYear: null,
			selectorMonths: null,
			newsData: [],
			viewedNewsCount: 9
		}
	},
	mounted() {
		this.axios.get('https://raw.githubusercontent.com/DiceMasters/JSON-storage/master/cp-json.json')
			.then( res => {
				this.newsData = res.data
			})
	},
	methods: {
		loadMoreNews() {
			this.viewedNewsCount += 9
		},
		resetMoreNews() {
			this.viewedNewsCount = 9
		}
	},
	computed: {
		getSelectorYear() { return (this.selectorYear) ? Number(this.selectorYear.title.substring(0, 4)) : 0 },
		getSelectorMonths() {
			return (this.selectorMonths) ? this.months.findIndex( v => v === this.selectorMonths) : 0
		},
		getFilteredNews() {
			return (this.newsData.length) ? this.newsData.filter( val => {
				if (this.getSelectorMonths !== 12) {
					if (
						Number(val.date.split('.')[2]) == this.getSelectorYear
						&& Number(val.date.split('.')[1]) == this.getSelectorMonths
					) { return true }
				} else {
					if ( Number(val.date.split('.')[2]) == this.getSelectorYear ) return true
				}
			}) : []
		},
		getCountedNews() {
			return (this.getFilteredNews.length) ? this.getFilteredNews.filter( (v, i) => i < this.viewedNewsCount) : []
		},
		isAllNewsViewed() {
			return this.getFilteredNews.length <= this.viewedNewsCount
		}
	},
}
</script>

<style lang="less">
#app {
	font-family: 'Noto Sans', Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	color: black;
}
</style>
