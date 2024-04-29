<script setup>
const personagem = defineProps(["name","status", "episode", "gender", "origin", "location", "image"])

let statusColor = ''
let status = personagem.status;
let circle = document.getElementsByClassName("bi-circle-fill")

switch(personagem.status){
    case "Alive":
        status = "Vivo";
        circle = "green";
        statusColor = "green";
        break;
    case "Dead":
        status = "Morto";
        circle = "darkred";
        statusColor = "darkred";
        break;
    case 'unknown':
        status = "Desconhecido";
        circle = "gray";
        statusColor = 'gray';
        break;
    default:
        statusColor = 'black'; 
}


let origem = personagem.origin
let LocalizaçãoAtual = personagem.location

if (personagem.origin == 'unknown' || personagem.location == 'unknown'){
    origem = "Desconhecida"
    LocalizaçãoAtual = "Desconhecida"
}



</script>

<template>
    <div class="col-md-4">
        <div class="card p-2 mb-3">
            <img :src="personagem.image" height="180rem" style="margin: auto;" alt="">
            <p class="text-center">Nome: {{ personagem.name }}</p>
            <p class="text-center">Genero: {{ personagem.gender }}</p>
            <p class="text-center">Status: <strong :style="{color: statusColor}">{{ status }}</strong><i class="bi bi-circle-fill" :style="{color:circle}"></i></p>
            <p class="text-center">Origem: {{ origem }}</p>
            <p class="text-center">Localização Atual: {{ LocalizaçãoAtual }}</p>
            <p class="text-center">Numero de aparicoes: <strong>{{ personagem.episode.length }}</strong></p>
        </div>
    </div>
</template>

<style>
.bi-circle-fill{
    margin: 5px;
}

img{
    border-radius: 15px;
}

</style>