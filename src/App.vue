<template>
  
  <h1>Hello World</h1>

  <table>
    <thead>
      <tr>
        <th>Header 1</th>
        <th>Header 2</th>
        <th>Header 3</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="coin in coins" :key="coin.id">
             
      </tr>
    </tbody>
  </table>

</template>

<script>
export default {

  name: 'App',

  data(){
    return {
      coins: []
    };
  },

  async mounted(){
    const res = await fetch(
      'https://api.coingecko.com/api/v3/coins/markets?vs_currency=eur&order=market_cap_desc&per_page=100&page=1&sparkline=false&locale=en' 
    );
    const data = await res.json()
    this.coins = data
  }
  
}
</script>


<style></style>
