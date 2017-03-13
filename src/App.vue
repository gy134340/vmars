<template>
	<div id="app">
		<router-view></router-view>
	</div>
</template>

<script>
import home from './views/home.vue';
export default {
	name: 'app',
	components: {
		home
	}
};
</script>

<style>
@import './assets/reset.css';
#app {
	width: 100%;
	height: 100%;
}
</style>
