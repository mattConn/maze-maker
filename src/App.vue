<script>
import Tile from './components/Tile.vue'

export default {
  components: {
    Tile
  },
  created() {
    this.initMaze();
  },
  data() {
    return {
      mazeWidth: 15,
      showGrid: true, 
      rows: []
    }
  },
  methods: {
    // toggle wall for tile on click
    wallClickHandler(tile, direction) {
      tile[direction] = !tile[direction];
    },
    // init maze
    initMaze(){
      // create rows of tiles
      for(let i = 0; i < this.mazeWidth; i++) {
        let row = [];
        for(let j = 0; j < this.mazeWidth; j++) {
          row.push({
            north: false,
            south: false,
            east: false,
            west: false
          });
        }
        this.rows.push(row);
      }
    },
    // erase and reinit maze
    eraseMaze(){
      this.rows = [];
      this.initMaze();
    },
    // open print dialog
    printMaze(){
      print();
    },
  },
}
</script>

<template>
  <h1 class="app-title">Maze Maker v1.0</h1>
  <!-- toggle grid visibility -->
  <div class="maze-controls">
    <button @click="printMaze">Print</button>
    <button @click="showGrid = !showGrid">Toggle grid</button>
    <button class="is-danger" @click="eraseMaze">Erase maze</button>
  </div>
  <div class="maze">
    <div class="tile-row" v-for="row,i in rows">
      <Tile v-for="tile,j in row"
      :hasBorder="showGrid"
      :north="tile.north"
      :west="tile.west"
      :key="i + '-' + j"
      @wall-click="(direction) => wallClickHandler(tile, direction)"
      ></Tile>
    </div>
  </div>
</template>

<style lang="scss" scoped>
* {
  box-sizing: border-box;

}

.app-title {
  text-align: left;
  margin: 0.25em 0;
  font-size: 2.3em;

  @media print {
    display: none;
  }
}

// buttons for clearing maze and toggling grid
.maze-controls {
  display: flex;
  margin-bottom: 1em;

  @media print {
    display: none;
  }

  button {
    margin-right: 1em;
    background-color: #e7e6e6;

    // for destructive/permanent mutating actions 
    &.is-danger {
      background-color: #ff7777;
      margin: 0 1em;
    }
  }
}

.maze {
  border: solid 1px black;
  .tile-row {
    display: flex;
    flex-direction: row;
    width: 100%;
    height: 100%;
  }
}

</style>