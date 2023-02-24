<template>
	<router-link
		to="/"
		class="logo"
	>
		Users App :)
	</router-link>
</template>

<script>
	export default {
		name: 'UILogo'
	};
</script>

<style lang="scss" scoped>
	.logo {
		display: inline-block;
		color: $color-brand-2;
		font-family: $font-brand-1;
		font-size: 5rem;
		font-weight: bold;
		line-height: 100%;

		@include media('sm') {
			font-size: 4rem;
		}

		&:hover {
			color: $color-white;
		}
	}
</style>
