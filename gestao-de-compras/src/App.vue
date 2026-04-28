<script setup>
import { ref } from 'vue'

// Variáveis reativas
const novoItem = ref('')
const itens = ref([])

// Adicionar item
function adicionarItem() {
  const valor = novoItem.value.trim()

  if (valor !== '') {
    itens.value.push(valor)
    novoItem.value = ''
  }
}

// Remover item
function removerItem(index) {
  itens.value.splice(index, 1)
}
</script>

<template>
  <div class="container">
    <h1>Gerenciador de Compras</h1>

    <!-- Input + botão -->
    <div class="input-area">
      <input
        v-model="novoItem"
        @keyup.enter="adicionarItem"
        type="text"
        placeholder="Digite um produto"
      />
      <button @click="adicionarItem">Adicionar</button>
    </div>

    <!-- Contador -->
    <p class="contador">Total de itens: {{ itens.length }}</p>

    <!-- Condicional -->
    <div v-if="itens.length > 0">
      <h2>Minha Cesta de Compras</h2>

      <!-- Lista -->
      <ul>
        <li v-for="(item, index) in itens" :key="index">
          {{ item }}
          <button @click="removerItem(index)">Remover</button>
        </li>
      </ul>
    </div>

    <div v-else>
      <p class="vazio">
        Sua cesta está vazia! Adicione produtos para começar.
      </p>
    </div>
  </div>
</template>

<style>
.container {
  max-width: 500px;
  margin: auto;
  font-family: Arial, sans-serif;
}

.input-area {
  display: flex;
  gap: 10px;
  margin-bottom: 15px;
}

input {
  flex: 1;
  padding: 8px;
}

button {
  padding: 8px 12px;
  cursor: pointer;
}

ul {
  list-style: none;
  padding: 0;
}

li {
  display: flex;
  justify-content: space-between;
  margin-bottom: 8px;
  background: #f2f2f2;
  padding: 8px;
}

.contador {
  font-weight: bold;
}

.vazio {
  color: gray;
}
</style>