<script setup>
import { ref } from 'vue'
import NavComp from './components/NavComp.vue'

const produtos = ref([
  { id: 1, nomeProduto: 'camisa', valorProduto: 12.48, quantidade: 1 },
  { id: 2, nomeProduto: 'meia', valorProduto: 1.67, quantidade: 1 },
  { id: 3, nomeProduto: 'calça', valorProduto: 12.90, quantidade: 1 },
  { id: 4, nomeProduto: 'sapato', valorProduto: 589.67, quantidade: 1 },
  { id: 5, nomeProduto: 'bermuda', valorProduto: 23.90, quantidade: 1 },
  { id: 6, nomeProduto: 'boné', valorProduto: 2.25, quantidade: 1 },
  { id: 7, nomeProduto: 'cueca', valorProduto: 5000.99, quantidade: 1 }
])

const carrinho = ref({
  items: [],
  total: 0
})

function limparCarrinho() {
  carrinho.value.items = []
}

function adicionarItem(produto) {
  carrinho.value.items.push({
    id: produto.id,
    nome: produto.nomeProduto,
    valor: produto.valorProduto,
    quantidade: produto.quantidade,
    total: Number((produto.valorProduto * produto.quantidade).toFixed(2)),
  })
}

function incrementarCompra(index) {
  produtos.value[index].quantidade++
}

function decrementarCompra(index) {
  if (produtos.value[index].quantidade > 1) {
    return produtos.value[index].quantidade--
  }
}
</script>

<template>
  <NavComp />
  <main>
    <div class="produtos">
      <div class="card" v-for="(produto, index) in produtos" :key="produto.id">
        <h1>{{ produto.id }} - {{ produto.nomeProduto }}</h1>
        <h2>Quantidade:{{ produto.quantidade }}</h2>
        <h2>Preço: R${{ produto.valorProduto }}</h2>
        <div>
          <button @click="decrementarCompra(index)">-</button>
          <button @click="incrementarCompra(index)">+</button>
          <button @click="adicionarItem(produto)">adicionar</button>
        </div>
      </div>
    </div>
    <div class="carrinho">
      <h2>CARRINHO</h2>
      <div>
        <div class="cardCarrinho" v-for="itemCarrinho in carrinho.items" :key="itemCarrinho.id">
          <h4>{{ itemCarrinho.id }} - {{ itemCarrinho.nome }}</h4>
          <p>Quantidade: {{ itemCarrinho.quantidade }}</p>
          <p>Preço: R${{ itemCarrinho.valor }} (total: R${{ itemCarrinho.total }})</p>
        </div>
      </div>
      <button @click="limparCarrinho()">Limpar Carrinho</button>
    </div>
  </main>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Mukta:wght@200;300;400;500;600;700;800&display=swap');
* {
  margin: 0;
  padding: 0;
  font-family: 'Mukta', sans-serif;
}
main {
  width: 100%;
  display: flex;
}
main .produtos {
  display: flex;
  width: 80%;
  flex-wrap: wrap;
  flex-direction: row;
  justify-content: flex-start;
  align-content: flex-start;
}
main .carrinho {
  width: 20%;
  padding: 20px;
  background-color: #e5e5e5;
}
.card {
  width: 18%;
  border-radius: 10px;
  border: 4px solid gray;
  margin: 10px;
  padding: 20px;
}
.cardCarrinho {
  border-radius: 10px;
  background-color: white;
  margin: 10px;
  padding: 20px;
}

.card button {
  padding: 10px;
}
</style>
