<template>
	<div class="human-container">
		<img class="gallows human-abs" src="@/assets/belka4.png" alt />

		<img v-if="manParts >= 1" class="head human-abs" src="@/assets/head.png" alt />

		<img v-if="manParts >= 2" class="tom human-abs" src="@/assets/tom.png" alt />

		<img v-if="manParts >= 3" class="left-hand human-abs" src="@/assets/lh.png" alt />

		<img v-if="manParts >= 4" class="right-hand human-abs" src="@/assets/rhpng.png" alt />

		<img v-if="manParts >= 5" class="left-leg human-abs" src="@/assets/rl5.2.png" alt />

		<img v-if="manParts >= 6" class="right-leg human-abs" src="@/assets/rl5.4.png" alt />
	</div>
</template>

<script>
import { bus } from '../main';

export default {
  props: ['word'],
  data() {
    return {
      manParts: 0,
    };
  },
  created() {
    bus.$on('mistake', () => {
      this.manParts++;
      if (this.manParts >= 6) {
        console.log('loser!');

        bus.$emit('end', [this.word, 'YOU LOST!']);
      }
    });
  },
};
</script>

<style lang="scss">
.human-container {
	position: relative;
	width: 300px;
	height: 300px;
	z-index: 101;
	.human.abs {
		position: absolute;
	}
	.gallows {
		position: absolute;

		width: 203px;
		height: 35px;
		left: 0px;
		top: 36px;
	}
	.head {
		position: absolute;

		width: 45px;
		height: 55px;
		left: 150.5px;
		top: 66px;
	}
	.tom {
		position: absolute;

		width: 39px;
		height: 62px;
		left: 153px;
		top: 120px;
	}
	.left-hand {
		position: absolute;

		width: 50.87px;
		height: 62px;
		left: 112px;
		top: 120px;
	}
	.right-hand {
		position: absolute;

		width: 50.87px;
		height: 62px;
		left: 182.12px;
		top: 120px;
	}
	.left-leg {
		position: absolute;

		width: 16.83px;
		height: 65px;
		left: 145.26px;
		top: 175px;

		background: #6361c4;
		transform: rotate(17.24deg);
	}
	.right-leg {
		position: absolute;

		width: 16.83px;
		height: 65px;
		left: 183.74px;
		top: 175px;

		background: #6361c4;
		transform: matrix(-0.96, 0.3, 0.3, 0.96, 0, 0);
	}
}
</style>
