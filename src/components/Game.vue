<template>
	<div>
		<div class="game-box">
			<Man class="man" :word="word"></Man>
			<div class="right-sec">
				<h2>YOU MISSED!</h2>
				<div class="letter-box wrong-letters">
					<RedLetter v-for="(lett, index) in wrongLetters" :key="index" :letter="lett"></RedLetter>
				</div>
			</div>
		</div>
		<div class="letter-box">
			<Letter v-for="(lett, index) in word" :key="index" :letter="lett"></Letter>
		</div>
	</div>
</template>

<script>
import { bus } from '../main';

import Man from './Man.vue';
import Letter from './Letter.vue';
import RedLetter from './RedLetter.vue';

export default {
  props: ['word'],
  components: {
    Man,
    Letter,
    RedLetter,
  },
  data() {
    return {
      rightLetters: [],
      wrongLetters: [],
      isGameWon: [],
      pressKey: null,
    };
  },
  created() {
    bus.$on('keyPress', (letter) => {
      if (this.word.match(letter) && letter != undefined) {
        bus.$emit('keyMatched', letter);
        if (this.rightLetters.indexOf(letter) == -1) {
          this.rightLetters.push(letter);
          this.isGameWon = this.word.split('').map(el => this.rightLetters.indexOf(el));
          if (!this.isGameWon.includes(-1)) {
            console.log('winner!');
            bus.$emit('end', [this.word, 'YOU WON!']);
          }
        }
      } else if (
        this.wrongLetters.indexOf(letter) == -1
					&& letter != undefined
      ) {
        this.wrongLetters.push(letter);
        bus.$emit('mistake', letter);
      }
    });
  },
};
</script>

<style lang="scss">
.letter-box {
	display: flex;
	justify-content: center;
	flex-flow: row wrap;
	align-items: center;
	margin-top: 3rem;
}
.failed {
	margin: 0 auto;
	height: auto;
}
.game-box {
	display: flex;
	justify-content: space-between;
}
.wrong-letters {
	margin: 0;
	justify-self: center;
	margin-right: 2rem;
}
.right-sec {
	margin: 2rem;
}
</style>
