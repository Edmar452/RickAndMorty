<script setup>
import { onMounted, reactive, ref } from 'vue';
import ListCaracters from '../components/ListCaracters.vue';


let personagens = reactive(ref());

let pagina = 1

onMounted(() => {
  carregarPersonagens();
});

function carregarPersonagens() {
  fetch("https://rickandmortyapi.com/api/character?page=" + pagina)
    .then(response => response.json())
    .then(response => {
      personagens.value = response.results;
      console.log(personagens);

    });
}

function Proxima() {
  pagina++;
  carregarPersonagens();
  personagens.value = []
}

function Anterior() {
  if (pagina > 1) {
    pagina--;
    carregarPersonagens();
    personagens.value = []
  }
}
</script>


<template>
  <main>
    <div class="container">
      <div class="col-sm-12">
        <div class="card-body row">
          <ListCaracters v-for="personagem in personagens" 
            :key="personagem.name" :name="personagem.name"
            :location="personagem.location.name" 
            :image="personagem.image" 
            :status="personagem.status"
            :gender="personagem.gender" 
            :origin="personagem.origin.name" 
            :episode="personagem.episode" />
        </div>
        <div class="row">
          <div class="col">
            <button @click="Anterior()" class="btn btn-dark">Anterior Pagina</button>
          </div>
          <div class="col text-center paginas">
            <strong>{{ pagina }}</strong>
          </div>
          <div class="col text-end">
            <button @click="Proxima()" class="btn btn-dark">Proxima Pagina</button>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<style>
.btn {
  width: 20rem;
  height: 4rem;
  margin: 2%;
  margin-bottom: 12%;
}

.paginas {
  margin-top: 2%;
}
</style>
