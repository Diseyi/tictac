<template>
  <div class="tic-tac-toe">
    <h1>TicTac Game</h1>
    <p class="label">Current Player {{ currentPlayer }} </p>
    <div class="board">
      <div class="row" v-for="(row, rowIndex) in board" :key="rowIndex">
        <div class="cell" v-for="(cell, cellIndex) in row" :key="cellIndex" @click="makeMove(rowIndex, cellIndex)"
          :class="{ 'cell-x': cell === 'X', 'cell-o': cell === 'O' }" :disabled="cell !== null">
          {{ cell }}
        </div>
      </div>
    </div>
    <p class="label" v-if="winner">{{ winner }} wins!</p>
    <p class="label" v-else-if="isTie">It's a tie!</p>
    <br />
    <button @click="reset">Reset Game</button>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';


export default defineComponent({
  data() {
    return {
      board: [
        ['', '', ''],
        ['', '', ''],
        ['', '', '']
      ],
      currentPlayer: 'X',
      winner: null,
      isTie: false,
      gameOver: false
    };
  },
  methods: {
    makeMove(row: number, col: number) {
      if (!this.board[row][col] && !this.winner) {
        this.board[row][col] = this.currentPlayer;
        if (this.checkWin()) {
          this.winner = this.currentPlayer;
        } else if (this.checkTie()) {
          this.isTie = true;
        } else {
          this.currentPlayer = this.currentPlayer === 'X' ? 'O' : 'X';
        }
      }
    },
    checkWin() {
      for (let i = 0; i < 3; i++) {
        if (
          this.board[i][0] === this.currentPlayer &&
          this.board[i][1] === this.currentPlayer &&
          this.board[i][2] === this.currentPlayer
        ) {
          return true;
        }
        if (
          this.board[0][i] === this.currentPlayer &&
          this.board[1][i] === this.currentPlayer &&
          this.board[2][i] === this.currentPlayer
        ) {
          return true;
        }
      }
      if (
        this.board[0][0] === this.currentPlayer &&
        this.board[1][1] === this.currentPlayer &&
        this.board[2][2] === this.currentPlayer
      ) {
        return true;
      }
      if (
        this.board[0][2] === this.currentPlayer &&
        this.board[1][1] === this.currentPlayer &&
        this.board[2][0] === this.currentPlayer
      ) {
        return true;
      }
      return false;
    },
    checkTie() {
      for (let i = 0; i < 3; i++) {
        for (let j = 0; j < 3; j++) {
          if (!this.board[i][j]) {
            return false;
          }
        }
      }
      return true;
    },
    reset() {
      this.board = [
        ['', '', ''],
        ['', '', ''],
        ['', '', '']
      ];
      this.currentPlayer = 'X';
      this.gameOver = false;
      this.winner = null;
    },
  },
});
</script>
