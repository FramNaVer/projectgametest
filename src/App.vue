<script setup>
import { ref,} from 'vue'

const win_count_player1 = ref(0)
const draw_count_player1 = ref(0)
const loss_count_player1 = ref(0)

const win_count_player2 = ref(0)
const draw_count_player2 = ref(0)
const loss_count_player2 = ref(0)



const control_game = {
	'ค้อน': {
		'ค้อน': 'เสมอ',
		'กระดาษ': 'แพ้',
		'กรรไกร': 'ชนะ',
    'ความรัก': 'แพ้'
	},
	'กระดาษ': {
		'ค้อน': 'ชนะ',
		'กระดาษ': 'เสมอ',
		'กรรไกร': 'แพ้',
    'ความรัก': 'แพ้'
	},
	'กรรไกร': {
		'ค้อน': 'แพ้',
		'กระดาษ': 'ชนะ',
		'กรรไกร': 'เสมอ',
    'ความรัก': 'แพ้'
	}
  
}



const player1_choose = ref('');
const player2_choose = ref('');
const result = ref('');

const choiceImages = {
  'ค้อน': 'https://o.remove.bg/downloads/6ff9bf65-ae04-4c83-a42b-a16353928ce2/png-transparent-rock-paper-scissors-computer-icons-scissors-game-white-face-removebg-preview.png',
  'กระดาษ': 'https://o.remove.bg/downloads/c1a75629-1fee-423c-8047-290fe69a68ad/image-removebg-preview.png',
  'กรรไกร': 'https://o.remove.bg/downloads/e954c3e2-f8f8-4fe7-9462-09b234cb9560/image-removebg-preview.png',
};



function getRandomChoice() {
  const choices = ['ค้อน', 'กระดาษ', 'กรรไกร'];
  return choices[Math.floor(Math.random() * choices.length)];
}

function display_answer() {
  player1_choose.value = getRandomChoice();
  player2_choose.value = getRandomChoice();

  const out_result = control_game[player1_choose.value][player2_choose.value];

  if (out_result === 'ชนะ') {
    win_count_player1.value++;
    loss_count_player2.value++;
    result.value = 'Player 1 ชนะ';
  } else if (out_result === 'แพ้') {
    win_count_player2.value++;
    loss_count_player1.value++;
    result.value = 'Player 2 ชนะ';
  } else {
    draw_count_player1.value++;
    draw_count_player2.value++;
    result.value = 'เสมอ';
  }
}

function reset_round() {
  player1_choose.value = '';
  player2_choose.value = '';
  result.value = '';
  win_count_player1.value = 0;
  draw_count_player1.value = 0;
  loss_count_player1.value = 0;
  win_count_player2.value = 0;
  draw_count_player2.value = 0;
  loss_count_player2.value = 0;
}

</script>

<template>
  <div class="contrainer_all">
    <div class="box_title">
			<div class="text_title">Rock  Paper  Scissors</div>
      </div>

      <div class="contrainer_game">
        <div class="box_1" id="box_play1">
          Player1 {{ player1_choose }}
          <img v-if="player1_choose" :src="choiceImages[player1_choose]" alt="Player 1 Choice" class="box_img"/>
        </div>
        <div class="box_2" id="box_play2">
          Player2 {{ player2_choose }}
          <img v-if="player2_choose" :src="choiceImages[player2_choose]" alt="Player 2 Choice" class="box_img" />
        </div>
      </div>

    <div class="start_buttom">
      <button @click="display_answer" class="buttom_start"> Start Game </button>
    </div>

  <div class="contrainer_all_score"> 
    <div class="contrainer_score">
      <div class="box_score"> Score win Player1 <br> {{ win_count_player1 }}  </div>  
      <div class="box_score"> Score lose Player1 <br> {{ loss_count_player1 }} </div>
      
    </div>
    <div class="contrainer_score">
      <div class="box_score"> Score win Player2 <br> {{ win_count_player2 }}  </div>  
      <div class="box_score"> Score lose Player2 <br> {{ loss_count_player2 }} </div>
      
    </div>
  </div> 
    <div class="box_newgame">
      <button @click="reset_round" class="buttom_new"> Restart </button>
    </div>

  </div>    

</template>

<style>



/*ALl body*/
:root {
  font-family: 'Itim', cursive;
  font-size: 24px;
  line-height: 1.5;
  font-weight: 400;
  color-scheme: light dark;
  color: #242424;
  background-color: #ffffff;
  font-synthesis: none;
  text-rendering: optimizeLegibility;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  -webkit-text-size-adjust: 100%;

}

#app {
  
  margin:  auto;
  padding: 1rem;
  text-align: center;
}

*{
  padding: 10px;
}



.contrainer_all{
  border: 5px solid #333;
  background-color: #6495ED;
  border-radius: 12px;
}


.contrainer_game{
  display: grid;
  grid-template-columns: 1fr 1fr;
  margin-left: 300px;
  margin-right: 250px;
  padding: 20px;
  justify-content: center;
}

.box_img {
  width: 100px;
  height: 100px; 
}


.contrainer_score{
  margin-left: 7.5rem;
  text-align: center;
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
}

.contrainer_all_score{
  margin-left: 50px;
  margin-right: 50px;
}


.text_title{
  width: 500px;
  height: 70px;
  border: 2px solid #ffffff;
  border-radius: 15px;
  margin: auto; 
  display: flex;
  align-items: center;
  justify-content: center;  
  font-size: 1.5rem;

}


.buttom_new{
  padding: 20px;
  width: 7rem;
  height: 2.5rem;
  background-color: #9FE2BF;
  border-radius: 8px;
  border: 1px solid transparent;
  font-size: 1em;
  font-weight: 500;
  font-family: inherit;
  color: #242424;
  cursor: pointer;
  transition: border-color 0.25s;
}

.buttom_new:hover {
  transition: .3s;
  padding: 10px;
  color: red;
}

.buttom_start:hover{
  
  transition: 0.4s;
  padding: 10px;
  border: 2px solid #ffffff;
  color: white;
}


.buttom_start{
  text-align: center;
  padding: 1rem ;
  width: 9rem;
  height: 2.5rem;
  border-radius: 8px;
  border: 1px solid #ffffff;
  font-size: 1em;
  font-weight: 500;
  font-family: inherit;
  color: #242424;
  cursor: pointer;
  transition: border-color 0.3s;
}

.box_newgame,.start_buttom{
  display: flex;
  justify-content: center;
  align-items: center; 
  margin-top: 20px;
}

</style>