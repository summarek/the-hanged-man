<template>
	<div v-if="isScreenVis" class="ending-screen">
		<h1>{{message}}</h1>
		<h2>THE PASSWORD: {{password.toUpperCase()}}</h2>
		<a href="/">
			<button>Try again!</button>
		</a>
	</div>
</template>

<script>
import { bus } from '../main';

export default {
  props: ['word'],

  data() {
    return {
      isScreenVis: false,
      password: '',
      message: '',
    };
  },
  created() {
    bus.$on('end', (data) => {
      this.password = data[0];
      this.message = data[1];
      this.isScreenVis = true;
    });
  },
  methods: {},
};
</script>

<style lang="scss">
.ending-screen {
	color: white;
	position: absolute;
	display: flex;
	flex-direction: column;
	justify-content: center;
	align-items: center;
	width: 100%;
	height: 100vh;
	background-color: rgb(75, 75, 75);
	top: 0;
	left: 0;
	z-index: 100;
	h1 {
		margin: 1rem;
	}
	button {
		background-color: rgb(19, 72, 133);
		color: white;
		padding: 1rem;
		border: none;
		margin: 1rem;
		border-radius: 5px;
	}
}
</style>
