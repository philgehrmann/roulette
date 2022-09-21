<template>
  <div class="roulette-table">
    <div class="flex flex-auto w-100 py-4 px-4 md:py-8 md:px-8">
      <div class="roulette-table-wrapper">
        <div class="roulette-table-numbers">
            <div class="re"
          <p v-for="(color, number) in rouletteNumbers" :class="color" :data-color="color" :id="number" v-on:click="setBets(number, color)">
            <span class="black" v-if="number % 2 == 0">
              {{ number }}
            </span>
            <span class="red" v-else>{{ number }}</span>
          </p>
        </div>
      </div>
    </div>
    <div class="roulette-circle-wrapper">
        <div class="roulette-circle">
          <img src="../assets/images/roulette-wheel.svg" />
        </div>
        <div class="roulette-circle-result">
            <p>Die gezogene Zahl ist:</p>
            <p class="resultNumber">{{rouletteResult}}</p>
        </div>
    </div>
    <div class="playarea">
      <button
        class="bg-transparent hover:bg-green-500 text-white-700 font-semibold hover:text-white py-2 px-4 border border-white-500 hover:border-transparent rounded"
        v-on:click="playRoulette()"
      >
        LOS
      </button>
      <p>{{ globalAmount}}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "game-component",
  data() {
    return {
      rouletteNumbers: {
        1: "red",
        2: "black",
        3: "red",
        4: "black",
        5: "red",
        6: "black",
        7: "red",
        8: "black",
        9: "red",
        10: "black",
        11: "black",
        12: "red",
        13: "black",
        14: "red",
        15: "black",
        16: "red",
        17: "black",
        18: "red",
        19: "red",
        20: "black",
        21: "red",
        22: "black",
        23: "red",
        24: "black",
        25: "red",
        26: "black",
        27: "red",
        28: "black",
        29: "black",
        30: "red",
        31: "black",
        32: "red",
        33: "black",
        34: "red",
        35: "black",
        36: "red",
      },
      rouletteNumberColor: "",
      colorResult: "",
      rouletteResult: 0,
      votedNumbers: [],
      votedColor: [],
      bets: [],
      betAmount: 200,
      globalAmount: 400
    };
  },
  mounted() {
    this.initRoulette();
  },
  methods: {
    initRoulette () {
        this.resetRoulette();
    },
    playRoulette () {
       this.rouletteResult =  Math.floor(Math.random() * 36);
       this.rouletteNumberColor = this.rouletteNumbers[this.rouletteResult]
       document.querySelector('.resultNumber').classList.add( this.rouletteNumberColor);
       this.getResults();
    },
    resetRoulette () {
        this.rouletteResult = "n/a";
    },
    setBets (number, color) {
        if(this.checkAmountPossible(this.betAmount)) {
            this.bets.push({bet: {
                clr: color,
                nmbr: number,
                cash: this.betAmount
            }});
            let clickedNumber = document.getElementById(number);
            clickedNumber.classList.add("voted");
            this.removeAmountGlobal(this.betAmount);
        }
        
    
       
    },
    removeAmountGlobal (betAmount) {
        this.globalAmount = this.globalAmount - betAmount;
    },
    checkAmountPossible (bet) {
      
        if (this.globalAmount >= bet) {
          return true
        } else {
          return false
        }
    },
    getResults () {
      this.colorResult = this.rouletteNumbers[this.rouletteResult];

  }
  },
 
};
</script>

<style lang="scss">
.roulette-table {
  margin: 0 auto;
  display: grid;
  grid-template-columns: 30% 70%;
  background: green;
  &-numbers {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    grid-gap: 10px;
    margin: 0 auto;

    p {
      border: 1px solid #202020;
      border-radius: 5px;
      width: 75px;
      height: 75px;
      text-align: center;
      cursor: pointer;

      &.black {
        background: black;
      }
      &.red {
        background: red;
      }
      &.voted {
        pointer-events: none;
        background: green ;
        &::after{
            content:"voted";
        }
   }
    }
    span {
      color: #fff;
    }
  }
}
.playtable {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
}
.roulette-circle {
    &-wrapper {
    display: grid;
    grid-auto-rows: 80% 20%;
    }
    &-result {
        font-size: 2rem;
        color: #fff;
        text-align: center;
    }
}
</style>
