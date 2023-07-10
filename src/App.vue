<script setup>
import { ref, computed } from "vue";

const counter = ref(0);
const listFavNumbers = ref([]);

const increment = () => counter.value++;

const decrement = () => counter.value--;

const reset = () => (counter.value = 0);

const classCounter = computed(() => {
  if (counter.value == 0) return "number--zero";

  if (counter.value < 0) return "number--negative";

  if (counter.value > 0) return "number--postive";
});

const addItem = () => {
  listFavNumbers.value.push(counter.value);
};

const bloquearBtnAdd = computed(() => {
  const numSearch = listFavNumbers.value.find((num) => num === counter.value);
  return numSearch || numSearch === 0;
});
</script>

<template>
  <div class="my-5">
    <div
      class="container d-flex align-items-center justify-content-center h-100"
    >
      <div class="card card--material">
        <div class="card-header card-header--material">
          <span class="fw-bold">Practicas de Vue</span>
        </div>
        <div class="card-body">
          <div class="row">
            <div class="col-md-6">
              <div class="d-flex flex-column align-items-center my-4">
                <h2 class="number" :class="classCounter">
                  {{ counter }}
                </h2>

                <div class="actions">
                  
                  <button @click="increment" class="btn btn--actions">
                   <span class="material-symbols-outlined actions__icon">arrow_upward </span>
                    Aumentar
                  </button>
                  
                    <button @click="decrement" class="btn btn--actions">
                      <span class="material-symbols-outlined actions__icon">arrow_downward</span>
                      Decrementar
                    </button>

                    <button @click="reset" class="btn btn--actions">
                      <span class="material-symbols-outlined actions__icon">refresh </span>
                      Reiniciar
                    </button>

                    <button
                      class="btn btn--actions"
                      @click="addItem()"
                      :disabled="bloquearBtnAdd">
                      <span class="material-symbols-outlined actions__icon">add </span>
                      Agregar
                    </button>
                </div>
              </div>
            </div>
            <div class="col-md-6">
              <div class="row">
                <div class="col-md-12">
                  <h4>Lista de numeros</h4>
                </div>
                <div class="col-md-12">
                  <ul v-if="listFavNumbers.length > 0">
                    <li v-for="(favNumber, index) in listFavNumbers" :key="index">
                      {{ favNumber }}
                    </li>
                  </ul>
                  <div v-else class="empty m-5">
                    <span class="material-symbols-outlined empty__icon">draft</span>
                    <h5>No hay numeros registrados</h5> 
                  </div>
                </div>
              </div>
              
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.number {
  font-size: 12rem;
}
.number--postive {
  color: #4d88f7;
}

.number--negative {
  color: #f74d4d;
}

.number--zero {
  color: #bfbfbf;
}
.card--material {
  min-width: 70%;
  background-color: #f9fbfc;
}

.card-header--material {
  background: transparent;
  border: 0;
}

.actions {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 10px;
}

.btn--actions {
  display: flex;
  flex-direction: column;
  padding: 3rem;
  background-color:#7ca8fb;
  color: white;
  font-weight: bold;
}

.actions__icon {
  font-size: 2.3rem;
}

.empty {
  display: flex;
  flex-direction: column;
  gap: 10px;
  align-items: center;
  justify-content: center;
  text-align: center;
  color: #919191;
}

.empty__icon {
    font-size: 7rem;
    color: #bfbfbf;
}


</style>