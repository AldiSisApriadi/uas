<template>
    <div class="game-widget">
      <h2>Game of Tic Tac Toe</h2>
      <div class="game-board">
        <div v-for="(cell, index) in gameBoard" :key="index" @click="handleClick(index)">{{ cell }}</div>
      </div>
      <button @click="resetGame">Restart</button>
      <p>{{ gameStatus }}</p>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        gameBoard: ['', '', '', '', '', '', '', '', ''],
        currentPlayer: 'S',
        isGameEnded: false,
      };
    },
    computed: {
      gameStatus() {
        if (this.isGameEnded) {
          return 'Game Over!';
        }
        return `Player ${this.currentPlayer}'s turn`;
      },
    },
    methods: {
      handleClick(index) {
        if (!this.isGameEnded && this.gameBoard[index] === '') {
          this.gameBoard[index] = this.currentPlayer;
          this.checkWinner();
          this.currentPlayer = this.currentPlayer === 'S' ? 'D' : 'S';
        }
      },
      checkWinner() {
        const winningCombinations = [
          [0, 1, 2], [3, 4, 5], [6, 7, 8], // Rows
          [0, 3, 6], [1, 4, 7], [2, 5, 8], // Columns
          [0, 4, 8], [2, 4, 6], // Diagonals
        ];
        for (const combination of winningCombinations) {
          const [a, b, c] = combination;
          if (this.gameBoard[a] && this.gameBoard[a] === this.gameBoard[b] && this.gameBoard[a] === this.gameBoard[c]) {
            this.isGameEnded = true;
            return;
          }
        }
      },
      resetGame() {
        this.gameBoard = ['', '', '', '', '', '', '', '', ''];
        this.currentPlayer = 'S';
        this.isGameEnded = false;
      },
    },
  };
  </script>
  
  <style scoped>
  .game-widget {
    border: 1px solid #0ee9e9;
    padding: 20px;
    margin-bottom: 20px;
  }
  
  .game-board {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-gap: 10px;
    margin-bottom: 10px;
  }
  
  .game-board div {
    border: 1px solid #0bb3dd;
    height: 50px;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
  }
  
  button {
    margin-top: 10px;
  }
  </style>
  