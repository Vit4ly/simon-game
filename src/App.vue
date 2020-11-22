<template>
  <div id="app">
    <div class="wrapper">
      <h1>Simon Says</h1>
      <div class="game-board">
        <div class="simon">
          <ul>
            <li
              v-for="({color, style},ind) in colors"
              :key="ind"
              class="tile"
              :class="[color,{ hoverable: isHover, activeClass}]"
              :data-tile="ind + 1"
              @click="getUsersValue(ind)"
            ></li>
          </ul>
        </div>
      </div>
      <div class="game-info">
        <h2>Round: <span>{{ score }}</span></h2>
        <button @click="start">Start</button>
        <p data-action="lose">Sorry, you lost after <span>{{ score }}</span> rounds!</p>
      </div>
      <div class="game-options">
        <h2>Game Options:</h2>
        <div
          v-for="(value, ind) in radio"
          :key="ind">
          <input
            type="radio"
            :id="value"
            name="mode"
            :value="value"
            v-model="options"
          >
          <label for="value">
            {{ value }}
          </label>
        </div>
      </div>
      <div data-action="sound"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data: () => ({
    isHover: false,
    score: 0,
    options: 'Normal',
    getArr: [],
    gameValue: [],
    colors: [
      {
        color: 'red',
        style: false,
      },
      {
        color: 'blue',
        style: false,
      },
      {
        color: 'yellow',
        style: false,
      },
      {
        color: 'green',
        style: false,
      },
    ],
    radio: ['Normal', 'Sound Only', 'Light Only', 'Free Board'],
  }),
  methods: {
    newArr() {
      const max = this.colors.length;
      for (let i = 0; i <= this.score; i += 1) {
        this.gameValue.push(Math.floor(Math.random() * max + 1));
      }
    },
    getUsersValue(ind) {
      this.getArr.push(ind);
      console.log(this.getArr);
    },
    start() {
      this.isHover = true;
      this.newArr();
      this.score += 1;
      console.log(this.gameValue);
    },
  },
  computed: {},
};
</script>

<style scoped lang="scss">
body {
  font-family: Arial, serif;
  color: #333;
  -webkit-user-select: none; /* Chrome/Safari */
  -moz-user-select: none; /* Firefox */
  -ms-user-select: none; /* IE10+ */
  -o-user-select: none;
  user-select: none;
}

h1 {
  margin: 1em 0 2em;
  text-align: center;
}

ul {
  list-style: none;
}

ul, li {
  padding: 0;
  margin: 0;
}

p[data-action="lose"] {
  display: none;
}

.active {
  opacity: 1 !important;
}

.clearfix {
  width: 100%;
  clear: both;
}

.wrapper {
  width: 540px;
  margin: 0 auto;
}

.container {
  width: 305px;
}

.simon {
  background: #fff;
  position: relative;
  float: left;
  margin-right: 3em;
  width: 302px;
  height: 295px;
  -webkit-border-radius: 150px 150px 150px 150px;
  border-radius: 150px 150px 150px 150px;
  -moz-box-shadow: 2px 1px 12px #aaa;
  -webkit-box-shadow: 2px 1px 12px #aaa;
  -o-box-shadow: 2px 1px 12px #aaa;
  box-shadow: 2px 1px 12px #aaa;
}

.tile {
  opacity: 0.6;
  -webkit-transition: opacity 250ms ease;
  -moz-transition: opacity 250ms ease;
  -ms-transition: opacity 250ms ease;
  -o-transition: opacity 250ms ease;
  transition: opacity 250ms ease;
}

.tile.lit {
  opacity: 1;
}

.red, .blue, .yellow, .green {
  height: 290px;
  -webkit-border-radius: 150px 150px 150px 150px;
  border-radius: 150px 150px 150px 150px;
  position: absolute;
  text-indent: 10000px;
}

.red:hover, .blue:hover, .yellow:hover, .green:hover {
  border: 2px solid black
}

.red {
  background: #FF5643;
  clip: rect(0px, 300px, 150px, 150px);
  width: 296px;
}

.blue {
  background: dodgerblue;
  clip: rect(0px, 150px, 150px, 0px);
  width: 300px;
}

.yellow {
  background: #FEEF33;
  clip: rect(150px, 150px, 300px, 0px);
  width: 300px;
}

.green {
  background: #BEDE15;
  clip: rect(150px, 300px, 300px, 150px);
  width: 296px;
}

.game-info {
  margin-top: 90px;
}

.game-info button {
  width: 5em;
  box-sizing: border-box;
  font-size: 1.4em;
  //-webkit-border-radius: 10px 10px 10px 10px;
  border-radius: 10px 10px 10px 10px;
  background: #6DABE8;
  border: none;
  padding: 0.3em 0.6em;
}

.game-info button:hover {
  background: #78BCFF;
}

.game-options h2 {
  margin-top: 30px;
  margin-bottom: 0;
}

.game-options input[type="radio"] {
  margin-right: 10px;
}

.hoverable:hover {
  cursor: pointer;
}

</style>
