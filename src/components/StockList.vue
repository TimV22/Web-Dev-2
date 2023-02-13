<template>
  <div v-if="buttonIsClicked" class="start-div" @click="clickGreenButton">
    <h1 class="start-h1">Let's Start</h1>
  </div>

  <div v-else>
    <h1>Stocks</h1><br>
    <table class="stock-table">
      <thead>
      <tr>
        <th>Name</th>
        <th>Price</th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="stock in stocks" :key="stock.name">
        <td>{{ stock.name }}</td>
        <td :class="{ 'text-red': stock.price < stock.previousPrice, 'text-green': stock.price > stock.previousPrice }">{{ stock.currency }} {{ stock.price }}</td>
      </tr>
      </tbody>
    </table>
    <button class="update-button" @click="updatePrices">Update prices</button>
  </div>

</template>

<script>
export default {
  mounted() {
    setInterval(this.updatePrices, 1000);
  },
  name: "StockList",
  data() {
    return {
      stocks: [
        {name: "BMW", price: 61.05, previousPrice: 0, currency: "€"},
        {name: "Caterpillar", price: 146.49, previousPrice: 0, currency: "$"},
        {name: "AMD", price: 76.5, previousPrice: 0, currency: "$"},
        {name: "Gazprom", price: 4.583, previousPrice: 0, currency: "$"},
      ],
      portfolio: [],
      buttonIsClicked: true
    };
  },
  methods: {
    clickGreenButton() {
      this.buttonIsClicked = false;
    },
    updatePrices() {
      let min = -1;
      let max = 2;
      this.stocks.forEach(stock => {
        stock.previousPrice = stock.price;
        stock.price += (Math.random() * (max - min) + min);
        stock.price = parseFloat(stock.price.toFixed(3));
        if (stock.price < 0) {
          stock.price = 0;
        }
      });
    }
  }
}
</script>

<style scoped>
.start-h1 {
  color: white;
  text-align: center;
  font-weight: bold;
  justify-content: center;
  padding: 1rem;
}

.start-div {
  background-color: green;
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

h1, h2, h3, h4, h5, h6 {
  color: white;
  text-align: center;
  font-weight: bold;
  justify-content: center;
}

.stock-table {
  width: 100%;
  border-collapse: collapse;
  border: 1px solid white;
  color: white;
  text-align: center;
  padding: 3rem;
}

.update-button {
  background-color: green;
  color: white;
  font-weight: bold;
  border: none;
  border-radius: 5px;
  padding: 1rem;
  margin: 3rem;
  display: flex;
  justify-content: center;
  align-items: center;
}

.text-red {
  color: red;
}

.text-green {
  color: green;
}

</style>