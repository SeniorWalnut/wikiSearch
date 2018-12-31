<template>
	<div class="SearchWikiList">
		<div class="SearchWikiList__container">
			<div class="SearchWikiList__form SearchWikiList-form" :class="{closed: isClosed}">
				<div class="SearchWikiList__title">Search Wiki</div>
				<input placeholder="Input something to find" v-model.trim="query" @keyup.enter="sendQuery" type="text" class="SearchWikiList-form__input SearchWikiList-form__input"><br>
				<button type="button" @click="sendQuery" class="SearchWikiList-form__button">
					<i v-if="isClosed" class="fas fa-search" @click="isClosed = !isClosed"></i>
					<i v-else class="fas fa-times" @click="isClosed = !isClosed"></i>
				</button>
			</div>
			<div class="SearchWikiList__list" v-for="(page, index) in pages">
				<search-wiki-block :key="index" :page="page"/>
			</div>
		</div>
	</div>
</template>


<script>
import SearchWikiBlock from './SearchWikiBlock';

const url = "https://en.wikipedia.org/w/api.php?&origin=*&action=query&list=search&utf8=&prop=links& format=json&srsearch=";


export default {
	name: "search-wiki-list",

	data() {
		return {
			query: '',
			pages: [],
			isClosed: true,
		}
	},

	methods: {
		sendQuery() {
			this.pages = []
			if (!this.isClosed && this.query.length) {
				this.isClosed = false
				this.finded = true
				this.$http
					.get(url + this.query)
					.then(resp => {
						this.pages = resp.data.query.search
					})
			} 
		}

	},
	components: {
		SearchWikiBlock
	}
}

</script>


<style lang="sass">
	.SearchWikiList 
		padding: 20px
		&__container 
			display: flex
			justify-content: center
			align-items: center
			flex-flow: column

		&__title
			font-family: 'Aleo', serif
			font-size: 56px
			letter-spacing: 5px
			word-spacing: 15px
			margin-right: 10px
			// margin-right: 20px

		&-form
			display: flex
			flex-direction: row
			&.closed 
				.SearchWikiList-form 
					&__input
						width: 0
						border: 0
						padding: 0
						transition: all .5s
					&__button
						margin-left: 0
						transition: all .3s
						
			&__input
				border-radius: 50px
				outline: none
				border: 1px solid #202020
				padding: 12px 50px
				padding-left: 20px
				transition: all .3s
				font-family: 'Roboto Mono', monospace
				&::placeholder
					font-family: 'Aleo', serif

			&__button
				border: none
				background: none
				font-size: 40px
				outline: 0
				cursor: pointer
				margin-left: -60px
				& i:hover
					color: #96CEB4
					font-size: 45px
					transition: all .3s
		&__list 
			margin-top: 20px
</style>