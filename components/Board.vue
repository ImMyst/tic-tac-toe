<template>
  <div class="game">
    <Score :x-score="xScore" :o-score="oScore" />
    <Button @click="startGame">
      {{ gameStarted ? 'Recommencer' : 'Commencer' }}
    </Button>
    <p v-if="status" class="game-status">{{ status }}</p>
    <div class="game-board">
      <div v-for="(row, i) in board" :key="i">
        <Case
          v-for="casee in row"
          :key="casee"
          :value="cases[casee]"
          @case:clicked="addValue(casee)"
        />
      </div>
    </div>
    <Modal :is-open="isModalOpen" @close:modal="isModalOpen = false">
      {{ modalMessage }}
    </Modal>
  </div>
</template>

<script>
export default {
  data() {
    return {
      gameStarted: false,
      status: '',
      board: [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
      ],
      cases: Array(9).fill(null),
      xIsNext: true,
      xScore: 0,
      oScore: 0,
      isModalOpen: false,
      modalMessage: '',
    }
  },
  methods: {
    startGame() {
      if (!this.gameStarted) {
        this.gameStarted = true
        this.status = 'Suivant: X'
      } else {
        // Reset datas to initial values
        this.gameStarted = false
        this.status = ''
        this.xIsNext = true
        this.cases = Array(9).fill(null)
      }
    },

    addValue(i) {
      if (!this.gameStarted) {
        this.isModalOpen = true
        this.modalMessage = 'Cliquer sur le bouton pour commencer'
        return
      }

      const cases = this.cases.slice()
      if (this.getWinner(cases)) {
        this.isModalOpen = true
        this.modalMessage = 'La partie est finie !'
        return
      }
      if (cases[i]) {
        this.isModalOpen = true
        this.modalMessage = 'Case déjà prise !'
        return
      }
      cases[i] = this.xIsNext ? 'X' : 'O'
      this.cases = cases
      const winner = this.getWinner(cases)
      if (winner) {
        this.isModalOpen = true
        this.modalMessage = `Le gagnant est ${winner} !`
        this.status = `Gagnant: ${winner}`
        winner === 'X' ? this.xScore++ : this.oScore++
        return
      }
      this.xIsNext = !this.xIsNext
      this.status = `Suivant: ${this.xIsNext ? 'X' : 'O'}`
    },
    getWinner(cases) {
      const POSSIBILITIES = [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [0, 4, 8],
        [2, 4, 6],
      ]
      for (let i = 0; i < POSSIBILITIES.length; i++) {
        const [a, b, c] = POSSIBILITIES[i]
        if (cases[a] && cases[a] === cases[b] && cases[a] === cases[c]) {
          return cases[a]
        }
      }
      if (cases.every((casee) => casee !== null)) {
        this.isModalOpen = true
        this.modalMessage = 'Égalité'
        this.status = 'Égalité'
        return
      }
      return null
    },
  },
}
</script>

<style lang="scss" scoped>
.game {
  display: flex;
  flex-direction: column;
  justify-content: center;
  max-width: 50%;
  &-status {
    margin: 2rem 0 0;
    text-align: center;
    font-size: 1.3rem;
  }
  &-board {
    padding-top: 3rem;
    display: flex;
  }
}
</style>