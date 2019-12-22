<template>
  <div>
    <div class="game-of-life">
      <div v-for="row in rows" :key="row" class="row">
        <div v-for="col in cols" :key="col" class="cell" :class="cells[row - 1][col - 1] ? 'alive' : 'dead'"></div>
      </div>
    </div>
    <p>Alive: {{ alive }} (~{{ aliveRatio }}%)</p>
  </div>
</template>

<script>
  const defaultCells = [
    [0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0],
    [0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0],
    [0,0,0,0,1,1,0,0,0,0,0,1,1,0,0,0,0],
    [0,0,0,0,0,1,1,0,0,0,1,1,0,0,0,0,0],
    [0,0,1,0,0,1,0,1,0,1,0,1,0,0,1,0,0],
    [0,0,1,1,1,0,1,1,0,1,1,0,1,1,1,0,0],
    [0,0,0,1,0,1,0,1,0,1,0,1,0,1,0,0,0],
    [0,0,0,0,1,1,1,0,0,0,1,1,1,0,0,0,0],
    [0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0],
    [0,0,0,0,1,1,1,0,0,0,1,1,1,0,0,0,0],
    [0,0,0,1,0,1,0,1,0,1,0,1,0,1,0,0,0],
    [0,0,1,1,1,0,1,1,0,1,1,0,1,1,1,0,0],
    [0,0,1,0,0,1,0,1,0,1,0,1,0,0,1,0,0],
    [0,0,0,0,0,1,1,0,0,0,1,1,0,0,0,0,0],
    [0,0,0,0,1,1,0,0,0,0,0,1,1,0,0,0,0],
    [0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0],
    [0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0]
  ]

  const mod = (x, y) => (x + y) % y

  export default {
    name: 'ConwaysGameofLife',
    props: {
      cols: { type: Number, default: 17 },
      rows: { type: Number, default: 17 },
      interval: { type: Number, default: 200 },
      initial: { type: Array, default: () => defaultCells }
    },
    data () {
      return {
        cells: this.$props.initial
      }
    },
    computed: {
      alive () {
        return this.cells.flat().reduce((acc, cell) => acc + cell, 0)
      },
      aliveRatio () {
        return Math.round(10000 * this.alive / (this.rows * this.cols)) / 100
      }
    },
    mounted () {
      window.setInterval(() => {
        this.cells = this.nextGeneration()
      }, this.interval);
    },
    methods: {
      nextGeneration () {
        const { cols, rows } = this
        const next = []
        for (let row = 0; row < rows; row++) {
          next[row] = []
          for (let col = 0; col < cols; col++) {
            next[row][col] = this.nextState(row, col)
          }
        }
        return next
      },
      nextState (row, col) {
        const { cells, cols, rows } = this
        const cell = cells[row][col]
        let neighbors = 0
        for (const i of [mod(row - 1, rows), row, mod(row + 1, rows)]) {
          for (const j of [mod(col - 1, cols), col, mod(col + 1, cols)]) {
            if (i !== row || j !== col) {
              neighbors += cells[i][j]
            }
          }
        }
        if (cell === 1) {
          return (neighbors === 2 || neighbors === 3) ? 1 : 0
        } else {
          return (neighbors === 3) ? 1 : 0
        }
      }
    }
  }
</script>

<style lang="scss" scoped>
  .game-of-life {
    display: table;
  }

  .row {
    display: table-row;
  }

  .cell {
    border: 1px dotted #DDD;
    display: table-cell;
    height: 8px;
    width: 8px;

    &.alive {
      background-color: #333;
    }

    &.dead {
      background-color: white;
    }
  }
</style>
