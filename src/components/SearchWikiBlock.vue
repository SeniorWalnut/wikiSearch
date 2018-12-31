<template>
	<div class="SearchWikiBlock" :style="{borderColor: activeColor}"> 
		<div class="SearchWikiBlock__title">{{title}}</div>
		<div class="SearchWikiBlock__info"><span v-html="info"></span></div>
		<a :style="{color: activeColor}" :href="link" class="SearchWikiBlock__link">Link to page <i class="fas fa-arrow-right"></i></a>
	</div>
</template>

<script>
const colors = [
	"#96CEB4",
	"#FFCC5C",
	"#FF6F69",
	"#FFEEAD",
	"#96CEB4"
]

export default {
	props: {
		page: Object
	},
	data() {
		return {
			title: this.page.title,
			info: this.page.snippet,
			link: "https://en.wikipedia.org/?curid=" + this.page.pageid,
			activeColor: colors[Math.floor(Math.random() * colors.length)]
		}
	}
};
</script>

<style lang="sass">
	.SearchWikiBlock
		padding: 15px
		width: 50%
		// border-right: 3px solid 
		margin: 0 auto
		margin-bottom: 30px 
		&:hover
			border-left: 5px solid
			transition: border-left .4s
		&__title
			font-size: 24px
			padding-bottom: 10px
			font-family: 'Aleo', serif
		&__info
			font-size: 14px
			font-family: Roboto Mono
			padding-bottom: 10px
		&__link
			text-decoration: none
			font-family: Raleway
			// color: #96CEB4
			& i 
				padding-left: 10px
				font-size: 12px
</style>
