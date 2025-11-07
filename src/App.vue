<template>
  <div>
    <h1>Minha Biblioteca Pessoal</h1>
    <p>Total de livros: {{ livros.length }}</p>
  </div>
</template>

<script setup>
import { ref } from 'vue'
const livros = ref([])
</script>
