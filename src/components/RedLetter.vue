<template>
	<div class="letter-two">
		<div v-if="isRedLetterVis" class="letter-two-inner">{{letter.toUpperCase()}}</div>
	</div>
</template>

<script>
import { bus } from '../main';

export default {
  props: ['letter'],

  data() {
    return {
      isRedLetterVis: true,
      pressedKey: null,
    };
  },

  methods: {},
};
</script>

<style lang="scss">
.letter-two {
	width: 30px;
	height: 50px;
	border-radius: 10px;
	display: flex;
	justify-content: center;
	align-content: center;
	align-items: center;

	&-inner {
		color: rgb(59, 59, 207);
		font-size: 2.2rem;
	}
}
</style>
