<template>
	<div class="home" v-bind:style="bgall">
		<div class="intro">
			<h4 class="title">title: {{ apod.title}}</h4>
			<p class="info">{{ apod.explanation }}</p>
			<div class="more">
				<p>author: {{ apod.copyright }}</p>
				<p>date: {{ apod.date }}</p>
			</div>
			
		</div>
	</div>
</template>
<script>

import axios from 'axios';

export default {
	name: 'home',
	data () {
		return {
			apod: ''
		};
	},
	computed: {
		imgUrl: function () {
			return this.apod.url;
		},
		bgall: function() {
			return {
				'background-size': 'cover',
				'background-image': 'url(' + this.apod.url + ')',
				'background-position': 'center center',
				'background-repeat': 'no-repeat'
			};
			
		} 
	},
	components: {

	},

	beforeMount () {
		axios.get('https://api.nasa.gov/planetary/apod?api_key=NkLecWqIRgjAv1brKJLD1gvVekp48jnwv7H3NCeV')
		.then(res => {
			this.apod = res.data;
		})
		.catch(err => {
			console.log(err);
		});
	},
	methods: {

	}
};

</script>
<style >
	.home {
		width: 100%;
		height: 100%;
		position: relative;
	}
	.intro {
		display: block;
		position: absolute;
		width: 80%;
		left: 50%;
		top: 50%;
		color: #fff;
		-webkit-transform: translate(-50%, -50%);
		transform: translate(-50%, -50%);
	}
	.title, .info, .more{
		margin-bottom: 20px;
	}
	.more {
		padding-right: 8px;
		text-align: right;
	}
</style>












