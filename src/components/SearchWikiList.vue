<template>
	<div class="SearchWikiList">
		<div class="SearchWikiList__container">
			<div class="SeachWikiList__title">SearchWiki</div>
			<form class="SearchWikiList__form SearchWikiList-form">
				<div class="SearchWikiList-form__title">Input something to find:</div>
				<input v-model.trim="query" type="text" class="SearchWikiList-form__input"><br>
				<button type="button" @click="sendQuery" class="SearchWikiList-form__button">Search</button>
			</form>
			<div class="SearchWikiList__list" v-for="page in pages">
				<search-wiki-block :page="page"/>
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
			pages: []
		}
	},
	methods: {
		sendQuery() {
			if (this.query.length) {
				this.$http
					.get(url + this.query)
					.then(resp => (this.pages = resp.data.query.search))
			}
		}
	},
	components: {
		SearchWikiBlock
	}
}

</script>


<style>
	.SearchWikiList {
		width: 100%;
		display: flex;
		justify-content: center;
	}
</style>