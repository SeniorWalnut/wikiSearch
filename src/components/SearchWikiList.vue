<template>
	<div class="SearchWikiList">
		<div class="SeachWikiList__title">SearchWiki</div>
		<div class="SearchWikiList__container">
			<form class="SearchWikiList__form SearchWikiList-form">
				<div class="SearchWikiList-form__title">Input something to find:</div>
				<input v-model.trim="query" type="text" class="SearchWikiList-form__input"><br>
				<button type="button" @click="sendQuery" class="SearchWikiList-form__button">Search</button>
			</form>
			<div class="SearchWikiList__list">
				<!-- <search-wiki-block /> -->
			</div>
		</div>
	</div>
</template>


<script>
// import SearchWikiBlock from 'SearchWikiBlock';s

const url = "https://en.wikipedia.org/w/api.php?&origin=*&action=query&list=search&utf8=&prop=links&format=json&srsearch=";

export default {
	name: "search-wiki-list",
	data() {
		return {
			query: ''
		}
	},
	methods: {
		sendQuery() {
			if (this.query.length) {
				fetch(url + this.query)
					.then(data => data.json())
					.then(fetched => console.log(fetched))
			}
		}
	}
}

</script>


<style>
	
</style>