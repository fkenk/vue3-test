<template>
  <v-container class="grid-container">
    <v-text-field
      v-model="sizeX"
      label="Size X"
      type="number"
    />
    <v-text-field
      v-model="sizeY"
      label="Size Y"
      type="number"
    />

    <div
      class="grid"
      :style="{ width: gridWidth + 'px', height: gridHeight + 'px' }"
    >
      <div
        v-for="(row, y) in grid"
        :key="y"
        class="row"
      >
        <div
          v-for="(cell, x) in row"
          :key="x"
          class="cell"
          :class="{ 'cell--blue': cell === 1 }"
          @mouseover="toggleCellColor(x, y)"
        />
      </div>
    </div>
  </v-container>
</template>

<script>
import { ref, computed, watch } from 'vue';

export default {
  setup() {
    const sizeX = ref(64);
    const sizeY = ref(64);

    const grid = ref(createGrid(sizeX.value, sizeY.value));

    watch([sizeX, sizeY], ([newSizeX, newSizeY]) => {
      grid.value = resizeGrid(grid.value, newSizeX, newSizeY);
    });

    function createGrid(x, y) {
      return Array.from({ length: y }, () => Array.from({ length: x }, () => 0));
    }

    function resizeGrid(oldGrid, newSizeX, newSizeY) {
      const newGrid = createGrid(newSizeX, newSizeY);

      for (let y = 0; y < newSizeY; y++) {
        for (let x = 0; x < newSizeX; x++) {
          if (y < oldGrid.length && x < oldGrid[0].length) {
            newGrid[y][x] = oldGrid[y][x];
          }
        }
      }

      return newGrid;
    }

    function toggleCellColor(x, y) {
      grid.value[y][x] = grid.value[y][x] === 0 ? 1 : 0;
    }

    const gridWidth = computed(() => sizeX.value * (36+3) + 3);
    const gridHeight = computed(() => sizeY.value * (36+3) + 3);

    return { sizeX, sizeY, grid, toggleCellColor, gridWidth, gridHeight };
  }
};
</script>

<style lang="scss" scoped>
.grid-container {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.grid {
  display: flex;
  padding: 3px;
  gap: 3px;
  flex-direction: column;
  background-color: #222;
  margin: 20px;
}

.row {
  display: flex;
  gap: 3px;
}

.cell {
  width: 36px;
  height: 36px;
  background-color: white;

  &--blue {
    background-color: blue;
  }
}
</style>
