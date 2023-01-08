<script>
import Tile from './components/Tile.vue'

export default {
  components: {
    Tile
  },
  created() {
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
  },
}
</script>

<template>
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