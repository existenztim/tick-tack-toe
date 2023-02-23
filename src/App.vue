<script setup>
const CalculateWinner = (board) => {
  const lines = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6]
  ]
  for (let i = 0; i < lines.length; i++) {
    const [a, b, c] = lines[i]
    if (board[a] && board[a] === board[b] && board[a] === board[c]) {
      return board[a]
    }
  }
  return null
}
const winner = computed(() => CalculateWinner(board.value.flat()))
const MakeMove = (x, y) => {
	if (winner.value) return
	if (board.value[x][y]) return
	board.value[x][y] = player.value
	player.value = player.value === 'X' ? 'O' : 'X'
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
  <h1 class="text-4xl text-pink-600">hey</h1>
</template>

<style scoped>

</style>
