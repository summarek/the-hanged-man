<template>
	<div class="letter">
		<div v-if="isLetterVis" class="letter-inner">{{letter.toUpperCase()}}</div>
	</div>
</template>

<script>
import { bus } from '../main';

export default {
  props: ['letter'],

  data() {
    return {
      isLetterVis: false,
      pressedKey: null,
    };
  },
  created() {
    bus.$on('keyMatched', (data) => {
      if (data == this.letter) {
        this.isLetterVis = true;
      }
    });
  },
  methods: {},
};
</script>

<style lang="scss">
.letter {
	width: 50px;
	height: 50px;
	border-radius: 10px;
	background-color: rgb(65, 59, 59);
	display: flex;
	justify-content: center;
	align-content: center;
	align-items: center;
	margin: 0.4rem;

	&-inner {
		color: white;
		font-size: 2.2rem;
	}
}
</style>
