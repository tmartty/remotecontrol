<template>
	<q-page class="flex flex-center">
		<div class="container">
			<h2>TESTING</h2>
			<br>
			<b>time</b>
			{{ acceleration.timestamp }}
			<br>
			<b>refresh rate</b>
			{{ updateFrequency }}ms
			<br>
			<br>
			<b>Accelerometer <br>(raw)</b>
			<br>
			X: {{ acceleration.x }}
			<br>
			Y: {{ acceleration.y }}
			<br>
			Z: {{ acceleration.z }}
			<br>
			<br>
			<b>Accelerometer <br>(5 decimals)</b>
			<br>
			X: {{ acceleration.x.toFixed(5) }}
			<br>
			Y: {{ acceleration.y.toFixed(5) }}
			<br>
			Z: {{ acceleration.z.toFixed(5) }}
			<br>
			<h2>{{ tapped }}</h2>
			<h2>{{ s }}</h2>
		</div>
	</q-page>
</template>

<style>
</style>

<script>
export default {
	name: 'Home',
	data() {
		return {
			acceleration: null,
			updateFrequency: 100,
			spotify: null
		}
	},
	mounted() {
		navigator.accelerometer.getCurrentAcceleration(this.onSuccess, this.onError);
		var options = { frequency: this.updateFrequency };  // Update every 3 seconds
		navigator.accelerometer.watchAcceleration(this.onSuccess, this.onError, options);
	},
	methods: {
		onSuccess(acceleration) {
			this.acceleration = acceleration
		},
		onError() {
			alert('Error!');
		}
	},
	computed: {
		tapped: function () {
			if (this.acceleration) {
				if (
					this.acceleration.x < 0 &&
					// this.acceleration.y > 8.5 &&
					this.acceleration.z < 0
					) {
					var audio = new Audio('statics/beep.mp3');
					audio.play();
					return 'BOOM'
				} else {
					return '_____'
				}
			}
		}
	}
}
</script>