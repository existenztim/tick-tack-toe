<script setup>
import {ref, computed} from "vue"
let playerXscore = 0
let playerOscore = 0

const player = ref('X')
const board = ref([
  ['', '', ''],
  ['', '', ''],
  ['', '', '']
])

const CalculateWinner = (board) => {
  const winCombinations = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6]
  ]
  for (let i = 0; i < winCombinations.length; i++) {
    const [a, b, c] = winCombinations[i]
    if (board[a] && board[a] === board[b] && board[a] === board[c]) {
		board[a] === "X" ? playerXscore +=1 : playerOscore +=1;
		return board[a]
    }
  }
  return null
}
const winner = computed(() => {
  return CalculateWinner(board.value.flat());
});

const MakeMove = (x, y) => {
	if (winner.value) {
    return;
  }
	if (board.value[x][y]) {
    return;
  }
	board.value[x][y] = player.value;
	player.value = player.value === 'X' ? 'O' : 'X';
}
const ResetGame = () => {
	board.value = [
		['', '', ''],
		['', '', ''],
		['', '', '']
	]
	player.value = 'X'
}
</script>

<template>
  <main class="pt-8 text-center text-yellow-50">
		<h1 class="mb-8 text-3xl font-bold uppercase">Tic Tac Toe</h1>

		<h3 class="text-xl mb-4">Player {{ player }}'s turn</h3>

		<div class="flex justify-center p-4 text-xl">
			<p class ="p-4">
				PLAYER X: {{playerXscore }}
			</p>
			<p class ="p-4">
				PLAYER O: {{playerOscore }}
			</p>
		</div>

		<div class="flex flex-col items-center mb-8">
			<div 
				v-for="(row, x) in board" 
				:key="x"
				class="flex">
				<div 
					v-for="(cell, y) in row" 
					:key="y" 
					@click="MakeMove(x, y)" 
					:class="`border border-white w-24 h-24 hover:bg-gray-700 flex items-center justify-center material-icons-outlined text-4xl cursor-pointer ${cell === 'X' ? 'text-lime-500' : 'text-blue-400'}`">
					{{ cell === 'X' ? 'close' : cell === 'O' ? 'circle' : '' }}
				</div>
			</div>
		</div>

		<div class="text-center">
			<h2 v-if="winner" class="text-3xl font-bold mb-8">Player '{{ winner }}' wins!</h2>
			<button @click="ResetGame" class="px-4 py-2 bg-lime-500 rounded uppercase font-bold hover:bg-blue-400 duration-300">New Round</button>
		</div>	
	</main>
</template>

<style scoped>

</style>
