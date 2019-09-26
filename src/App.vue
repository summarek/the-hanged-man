<template>
	<div id="app">
		<Game :word="theWord"></Game>
		<GameWinScreen></GameWinScreen>
	</div>
</template>

<script>
import axios from 'axios';
import { log } from 'util';
import Game from './components/Game.vue';
import GameWinScreen from './components/GameWinScreen.vue';
import { bus } from './main';

export default {
  name: 'app',
  components: {
    Game,
    GameWinScreen,
  },
  data() {
    return {
      theWord: null,
      keyCodes: {
        65: 'a',
        66: 'b',
        67: 'c',
        68: 'd',
        69: 'e',
        70: 'f',
        71: 'g',
        72: 'h',
        73: 'i',
        74: 'j',
        75: 'k',
        76: 'l',
        77: 'm',
        78: 'n',
        79: 'o',
        80: 'p',
        81: 'q',
        82: 'r',
        83: 's',
        84: 't',
        85: 'u',
        86: 'v',
        87: 'w',
        88: 'x',
        89: 'y',
        90: 'z',
      },
    };
  },
  methods: {},
  mounted() {
    const proxyurl = 'https://cors-anywhere.herokuapp.com/';
    const url = 'https://random-word-api.herokuapp.com/key?'; // site that doesn’t send Access-Control-*
    axios.get(proxyurl + url).then((response) => {
      axios
        .get(
          `https://random-word-api.herokuapp.com/word?key=${
            response.data
          }&number=1`,
        )
        .then((response) => {
          this.theWord = response.data[0];
        });
    });

    document.addEventListener('keyup', (event) => {
      bus.$emit('keyPress', this.keyCodes[event.which]);
    });
  },
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css?family=Roboto&display=swap");
* {
	padding: 0;
	margin: 0;
	box-sizing: border-box;
}
body {
	font-family: "Roboto", sans-serif;
	width: 100%;
	height: 100vh;
}
</style>
