<script>
import Alerts from '../components/Alerts.vue'
import Keys from '../components/Keys.vue'
import Rows from '../components/Rows.vue'
import randomWords from 'random-words'

export default{
  name: "Home",
  components: {
    Keys,
    Rows,
    Alerts,
    // GlobalEvents
  },
  beforeMount(){
    const wards = randomWords({exactly:20, maxLength: 5})

    function findWordle(arr) {
        if(arr.some(e => e.length === 5)){
            return arr.find(word => word.length === 5);
        }else{
            return findWordle(arr = randomWords({exactly:2, maxLength: 5}));
        }
    }

    this.wordle = findWordle(wards).toUpperCase();
  },
  data(){
    return {
      isCorrect: false,
      alert: "",
      guesses: [
        ['', '', '', '', ''],
        ['', '', '', '', ''],
        ['', '', '', '', ''],
        ['', '', '', '', ''],
        ['', '', '', '', ''],
        ['', '', '', '', '']
      ],
      currentTile: 0,
      currentRow: 0,
      wordle: ""
    }
  },
  methods: {
    clickHandler(key){
      switch(key){
        case '<<':
        case 'BACKSPACE':
          this.deleteLetter();
          break;
        case 'ENTER':
          let bool = this.validityCheck();
          if(bool){
            let word = this.getWord();
            this.checkAnswer(word);
            this.tileFlip();
          }
          break;
        default:
          this.assignLetter(key);
      }
    },
    assignLetter(key){
      if(this.currentTile < 5 & this.currentRow < 6){
        const assign = document.querySelector(`#guess-${this.currentRow}-tile-${this.currentTile}`);
        this.guesses[this.currentRow][this.currentTile] = key;
        this.currentTile++;
        assign.textContent = key;
      }
    },
    getWord(){
      let word = this.guesses[this.currentRow].join('');
      return word;
    },
    deleteLetter(){
      if(this.currentTile>0){
        const assign = document.querySelector(`#guess-${this.currentRow}-tile-${this.currentTile - 1}`);
        assign.textContent = "";
        this.guesses[this.currentRow][this.currentTile-1] = '';
        this.currentTile--;
      }
    },
    validityCheck(){
      let word = this.getWord();
      if(word.length !== 5){
        this.showAlert("Please enter five numbers");
        return false;
      }
      if(this.currentRow>=6){
        return false;
      }
      return true;
    },
    checkAnswer(word){
      word === this.wordle ? this.showAlert("Excellent!!") : this.showAlert("Nope");
      this.currentRow++;
      this.currentTile = 0;
    },
    showAlert(msg){
      this.alert = msg;
      this.isCorrect = true;
      setTimeout(() => {
        this.isCorrect = false;
      }, 2000)
    },
    tileFlip(){
      console.log(`The answer is: ${this.wordle}`);
      const row = document.querySelector(`#guess-${this.currentRow-1}`).children;
      let checkWordle = this.wordle;
      const guess = [];
      Array.from(row).forEach(tile => {
        guess.push({letter: tile.textContent, color: 'grey-overlay'})
      })

      guess.forEach((guess,i) => {
        if(guess.letter == checkWordle[i]){
          guess.color = 'green-overlay';
          checkWordle = checkWordle.replace(guess.letter, ' ');
          return;
        } else if (checkWordle.includes(guess.letter)) {
          guess.color = 'yellow-overlay';
          checkWordle = checkWordle.replace(guess.letter, ' ');
          return;
        }
      });

      Array.from(row).forEach((tile,i) => {
        setTimeout(() => {
          tile.classList.add('flip');
          tile.classList.add(guess[i].color);
          this.changeKeyColor(guess[i].letter, guess[i].color)
        }, 300*i);
      })
    },
    changeKeyColor(id, color){
      document.getElementById(id).classList.add(color);
    },
    showKey(e){
      let inputVal = e.key.toUpperCase();
      const isLetter = /[A-Z]{1}/.test(inputVal) && inputVal.length === 1;
      if(isLetter || inputVal == 'ENTER' || inputVal == 'BACKSPACE'){
        this.clickHandler(inputVal);
      }
      
    }

  },
  emits: ['assign-letter']
}

</script>

<template>
    <div>
        <Alerts :alert="this.alert" :isCorrect="isCorrect"/>
        <Rows :guesses="guesses" />
        <Keys @click-handler="clickHandler" />
    </div>
</template>

<style scoped>

</style>