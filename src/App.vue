<template>
  <section class="todo">
    <div class="container">
      <div class="todo__title">ToDo</div>
      <div class="todo__input">
        <span>New ToDo</span>
        <input v-model="ticker" @keydown.enter="add" autocomplete="off" type="text" />
        <button @click="add" type="button">
          <span>Add ToDo</span>
        </button>
      </div>

      <div class="todo__block-list block-list">
        <div class="block-list__title">ToDo list</div>
        <ul class="block-list__list">
          <li v-for="t in tickers" :key="t.title" @click="select(t)" class="block-list__item">
            <div>{{ t.title }}</div>
            <button @click.stop="deleteTodo(t)">Delete</button>
          </li>
        </ul>
      </div>
    </div>
  </section>
</template>
<script>export default {
  name: "App",

  data() {
    return {
      ticker: "",
      tickers: [],
    };
  },
  beforeMount() {
    fetch('https://jsonplaceholder.typicode.com/todos/')
      .then(response => response.json())
      .then(json => this.tickers = JSON.parse(localStorage.getItem('tickers')) || json)

  },
  methods: {
    saveData() {
      const storageData = JSON.stringify(this.tickers);
      localStorage.setItem('tickers', storageData);
      console.log(localStorage);
    },
    add() {
      const currentTicker = {
        title: this.ticker,
      };
      this.tickers.unshift(currentTicker);
      this.ticker = "";
      this.saveData();
    },

    deleteTodo(tickerToRemove) {
      this.tickers = this.tickers.filter((t) => t != tickerToRemove);
      this.saveData();
    },

  },
}
</script>
<style src="./css/style.min.css"></style>