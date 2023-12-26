<script setup>
import { ref, computed, onMounted } from 'vue';

// Existing Flexbox code
const childCount = ref(1);
const flexDirection = ref('');
const flexWrap = ref('');
const flexJustifyContent = ref('');
const flexAlignItems = ref('');
const flexContent = ref('');

const flexClass = computed(() => {
    let classes = [
        flexDirection.value,
        flexWrap.value,
        flexJustifyContent.value,
        flexAlignItems.value,
        flexContent.value
    ];

    return classes.join(' ');
});

// New Grid Layout code
const rows = ref(3);
const columns = ref(3);

const updateGrid = () => {
  generateGrid();
};

const gridCells = ref([]);

const generateGrid = () => {
  const cells = [];
  for (let row = 0; row < rows.value; row++) {
    for (let col = 0; col < columns.value; col++) {
      cells.push({ row, column: col });
    }
  }
  gridCells.value = cells;
};

onMounted(() => {
  generateGrid();
});
</script>

<style scoped>
.grid-layout {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 20px;
}

.controls {
  margin-bottom: 10px;
}

.grid {
  display: grid;
  grid-template-columns: repeat(var(--columns, 3), 1fr);
  gap: 10px;
}

.grid-cell {
  border: 1px solid #ccc;
  padding: 10px;
  text-align: center;
}
</style>


<template>
    <div class="container py-5" style="height: 100vh;">
        <div class="row">
            <div class="col-md-4">
                <div class="card mt-3" style="width: 18rem;">
                    <a href="javascript: void(0)" class="text-decoration-none">
                        <div class="card-body">
                            <h5 class="card-title">Flexbox</h5>
                            <p class="card-text">A CSS layout module.</p>
                        </div>
                    </a>
                </div>
            </div>
            <div class="col-md-8">
                <div class="form-group">
                    <label>Child Count:</label>
                    <input type="number" min="1" v-model="childCount" class="form-control">
                </div>
                <div class="form-group">
                    <label>Flex Direction:</label>
                    <select class="form-select" v-model="flexDirection">
                        <option value="">-- Please select --</option>
                        <option value="flex-row">row</option>
                        <option value="flex-row-reverse">row-reverse</option>
                        <option value="flex-column">column</option>
                        <option value="flex-column-reverse">column-reverse</option>
                    </select>
                </div>
                <div class="form-group">
                    <label>Flex Wrap:</label>
                    <select class="form-select" v-model="flexWrap">
                        <option value="">-- Please select --</option>
                        <option value="flex-nowrap">nowrap</option>
                        <option value="flex-wrap">wrap</option>
                        <option value="flex-wrap-reverse">wrap-reverse</option>
                    </select>
                </div>
                <div class="form-group">
                    <label>Justify Content:</label>
                    <select class="form-select" v-model="flexJustifyContent">
                        <option value="">-- Please select --</option>
                        <option value="justify-content-start">flex-start</option>
                        <option value="justify-content-end">flex-end</option>
                        <option value="justify-content-center">center</option>
                        <option value="justify-content-around">space-around</option>
                        <option value="justify-content-evenly">space-evenly</option>
                        <option value="justify-content-between">space-between</option>
                    </select>
                </div>
                <div class="form-group">
                    <label>Align Items:</label>
                    <select class="form-select" v-model="flexAlignItems">
                        <option value="">-- Please select --</option>
                        <option value="align-items-stretch">stretch</option>
                        <option value="align-items-baseline">baseline</option>
                        <option value="align-items-center">center</option>
                        <option value="align-items-start">flex-start</option>
                        <option value="align-items-end">flex-end</option>
                    </select>
                </div>
                <div class="form-group">
                    <label>Align Content:</label>
                    <select class="form-select" v-model="flexContent">
                        <option value="">-- Please select --</option>
                        <option value="align-content-center">center</option>
                        <option value="align-content-start">flex-start</option>
                        <option value="align-content-end">flex-end</option>
                        <option value="align-content-around">space-around</option>
                        <option value="align-content-evenly">space-evenly</option>
                        <option value="align-content-between">space-between</option>
                    </select>
                </div>
                <div class="mt-5">
                    <div style="width: 100%; height: 400px;"
                        class="bg-primary bg-opacity-10 d-flex border border-4 border-warning" :class="flexClass">
                        <div v-for="child in childCount" :key="child"
                            class="p-5 bg-primary text-center d-flex align-items-center justify-content-center fs-1 text-white border border-2 border-dark">
                            {{ child }}
                        </div>
                    </div>
                </div>
            </div>

  <div class="row">
        <div class="col-md-4">
          <!-- Grid Layout Card -->
          <div class="card mt-3" style="width: 18rem;">
            <a href="javascript:void(0)" class="text-decoration-none">
              <div class="card-body">
                <h5 class="card-title">Grid Layout</h5>
                <p class="card-text">Create custom grid layouts.</p>
              </div>
            </a>
          </div>
        </div>
        <div class="col-md-8">
          <div class="grid-layout">
            <div class="controls">
              <label>Rows:</label>
              <input type="number" v-model="rows" min="1" @input="updateGrid" />
              <label>Columns:</label>
              <input type="number" v-model="columns" min="1" @input="updateGrid" />
            </div>
  
            <div class="grid">
              <div v-for="(cell, index) in gridCells" :key="index" class="grid-cell">
                {{ cell.row + 1 }} - {{ cell.column + 1 }}
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    </div>
  </template>
  
 