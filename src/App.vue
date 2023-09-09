<script setup>
import { ref } from 'vue';

const imgpaperLeft = ref(new URL('./assets/love-hands.png', import.meta.url).href);
const imgpaperRight = ref(new URL('./assets/love-hands.png', import.meta.url).href);
const PlayerScore = ref(0);
const ComputerScore = ref(0);
const gameResult = ref('');


const options = ['Rock', 'Paper', 'Scissors', 'Love'];

function getRandomOption() {
  const randomIndex = Math.floor(Math.random() * options.length);
  return options[randomIndex];
}

function startGame() {
  const rd1 = getRandomOption();
  const rd2 = getRandomOption();

 
  const imageMapping = {
    'Rock': 'rock.png',
    'Paper': 'paper.png',
    'Scissors': 'scissors.png',
    'Love': 'love-hands.png',
  };

  imgpaperLeft.value = new URL(`./assets/${imageMapping[rd1]}`, import.meta.url).href;
  imgpaperRight.value = new URL(`./assets/${imageMapping[rd2]}`, import.meta.url).href;


  if (rd1 === rd2) {
    
    gameResult.value = 'Tie!';
  } else if(rd1 === 'Love'){
    gameResult.value =  'Congratulations you wins!';
    PlayerScore.value += 1;
  }else if(rd2 === 'Love'){
    gameResult.value = 'You lose!';
    ComputerScore.value += 1;
  } else if ((rd1 === 'Paper' && rd2 === 'Rock') || (rd1 === 'Scissors' && rd2 === 'Paper') || (rd1 === 'Rock' && rd2 === 'Scissors')) {
    gameResult.value = 'Congratulations you wins!';
    PlayerScore.value += 1;
  } else {
    gameResult.value = 'You lose!';
    ComputerScore.value += 1; 
  }
}

function resetGame() {
  PlayerScore.value = 0;
  ComputerScore.value = 0;
  imgpaperLeft.value = new URL('./assets/love-hands.png', import.meta.url).href; 
  imgpaperRight.value = new URL('./assets/love-hands.png', import.meta.url).href; 
  gameResult.value = '';
}
</script>

<template>
  <div class="image-container">
    <div class="image-frame">
      <h2 class="centered-text">Rock-Paper-Scissors Game</h2>
      
      <h1 class="centered-text">Score: {{ PlayerScore }} - {{ ComputerScore }}</h1>
      <p class="centered-text result">{{ gameResult }}</p>
      <div class="team-names">
        <p class="centered-text team-names" style="color: #ff847c"><b>Player - Computer</b></p>
      </div>
      <div class="game-zone">
        <div class="team-image">
          <img class="left-image" :src="imgpaperLeft" alt="Image Left" style="width: 180px; height: 300px;">
          <img class="right-image" :src="imgpaperRight" alt="Image Right" style="width: 180px; height: 300px;">
        </div>
      </div>
      <div class="button-container">
        <button class="play-button" @click="startGame">Play Game</button>
        <button class="reset-button" @click="resetGame">Reset</button>
      </div>
    </div>
  </div>
</template>



