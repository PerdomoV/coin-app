<template>
  
  <h1>Crypto Precios</h1>

  <input @keyup="buscarMoneda()" :value="valorBusqueda" />

  <table>
    <thead>
      <tr>
        <th>Moneda</th>
        <th>Precio (eur)</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="coin in monedasFiltradas" :key="coin.id">
        <td><img :src="coin.image"> {{ coin.name }} {{ coin.symbol }}</td>       
        <td>{{ coin.current_price }}</td>       
      </tr>
    </tbody>
  </table>

</template>

<script setup>

  import { onMounted, ref } from 'vue'
  let coins  = []
  let monedasFiltradas = ref([])
  let valorBusqueda;
  let buscarMoneda = () => {
    monedasFiltradas = coins.filter( elemento => elemento.name === valorBusqueda || elemento.symbol === valorBusqueda ) 
  };

  onMounted(() => {
    fetch(
      'https://api.coingecko.com/api/v3/coins/markets?vs_currency=eur&order=market_cap_desc&per_page=100&page=1&sparkline=false&locale=es'
    ).then( 
      res => res.json() 
    ).then( 
    datos => { 
      /* coins = datos; */ 
      monedasFiltradas.value = datos; 
      coins.value = datos;
      console.log('coins: ', coins ); 
    }).catch( error => console.error('Error en fetch: '+error.message) );
  })

</script>


<style>

</style>
