<template>
  <div id="app">
  		<div class="SearchWikiBlock">
  			<div class="SearchWikiBlock__title">{{title}}</div>
  			<div class="SearchWikiBlock__info">{{info}}</div>
  			<a :href="link" class="SearchWikiBlock__link">Link to page -></a>
  		</div>
  </div>
</template>

<script>
export default {
	props: {
		page: Object
	},
	data() {
		return {
			title: this.page.title,
			info: this.page.snippet,
			link: "https://en.wikipedia.org/?curid=" + this.page.pageid
		}
	}
};
</script>

<style>

</style>
