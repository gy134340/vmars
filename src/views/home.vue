<template>
	<div class="home" v-bind:style="bgall">
		<h3 class="caption">每日天文图片</h3>
		<!-- <p class="date">Select date...</p> -->
		<input class="date_input" placeholder="Select date..."></input>
		<div class="intro">
			<h4 class="title">{{ apod.title}}</h4>
			<p class="info">{{ apod.explanation }}</p>
			<div class="more">
				<p>author: {{ apod.copyright || "anonymous" }}</p>
				<p>date: {{ apod.date }}</p>
			</div>
		</div>
	</div>
</template>
<script>
import axios from 'axios';
import Flatpickr from 'flatpickr';

export default {
	name: 'home',
	data () {
		return {
			apod: '',
			dateStr: '2016',
			// date: new Date()
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
		this.getNewImg();
	},
	mounted () {
		let ele = document.querySelectorAll('.date_input')[0];
		new Flatpickr(ele, {
			// altInput: true,
			maxDate: new Date(),
			// dateFormat: 'd.m.Y',
			defaultDate: '2017-01-10',
			onChange: function(selectedDates, dateStr, instance) {
				let date = dateStr;
				this.getNewImg(date);
			},
		});

	},
	methods: {
		getNewImg (date = '2017-01-10') {
			let url = `https://api.nasa.gov/planetary/apod?date=${date}&api_key=NkLecWqIRgjAv1brKJLD1gvVekp48jnwv7H3NCeV`;
			// let url = `https://api.nasa.gov/planetary/apod?date=${date}&api_key=54CTJvu9NJ25fe7z8K9GKOcXVfQMcWqBtILaTszK`;
			axios.get(url)
			.then(res => {
				this.apod = res.data;
			})
			.catch(err => {
				console.log(err);
			});
		}, 
	}
};

</script>
<style lang="scss" scoped>
	.caption {
		margin-top: 60px;
		width: 100%;
		color: #fff;
		margin-bottom: 100px;
		text-align: center;
		position: absolute;

	}
	.home {
		width: 100%;
		height: 100%;
		position: relative;
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
		.date_input {
			/*color: #ccc;
			width: 130px;
			height: 15px;
			position: absolute;
			margin: 30px 0px 0px 30px;
			font-size: 14px;
			display: inline-block;
			
			border-radius: 10px;
			background-color: rgba(88,88,88,0.5);*/
			width: 130px;
			height: 15px;
			position: absolute;
			margin: 30px 0px 0px 30px;
			color: #ccc;
			padding: 8px;
			border: 1px solid #e3e3e3;
		}
		.flatpickr-calendar {
			background-color: #484d5a;
			box-shadow: none;
		}
		.title, .info, .more{
			margin-bottom: 20px;
		}
		.more {
			padding-right: 8px;
			text-align: right;
		}
	}
	
</style>












