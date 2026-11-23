<script setup>
import { ref, computed } from 'vue'

const a = ref(0)
const b = ref(0)
const operacao = ref('+')

const operacoes = [
  { valor: '+', nome: 'Soma (+)' },
  { valor: '-', nome: 'Subtração (−)' },
  { valor: '*', nome: 'Multiplicação (×)' },
  { valor: '/', nome: 'Divisão (÷)' },
]

// Recalculado automaticamente sempre que um valor muda
const resultado = computed(() => {
  const x = Number(a.value)
  const y = Number(b.value)
  if (a.value === '' || b.value === '') return '—'
  switch (operacao.value) {
    case '+': return x + y
    case '-': return x - y
    case '*': return x * y
    case '/': return y === 0 ? 'Divisão por zero' : x / y
  }
})
</script>

<template>
  <main class="calc">
    <h1>Calculadora</h1>
    <div class="linha">
      <input v-model="a" type="number" aria-label="Primeiro número" />
      <select v-model="operacao" aria-label="Operação">
        <option v-for="o in operacoes" :key="o.valor" :value="o.valor">{{ o.nome }}</option>
      </select>
      <input v-model="b" type="number" aria-label="Segundo número" />
    </div>
    <p class="resultado">Resultado: <strong>{{ resultado }}</strong></p>
  </main>
</template>

<style scoped>
.calc { background: #fff; padding: 2rem; border-radius: 12px; box-shadow: 0 4px 16px #0001; }
h1 { margin-top: 0; }
.linha { display: flex; gap: .5rem; }
input, select { padding: .6rem; font-size: 1rem; border: 1px solid #d1d5db; border-radius: 6px; }
input { width: 7rem; }
.resultado { font-size: 1.25rem; margin-bottom: 0; }
</style>
