<!--
<template>
  <section class="block-vue">
    <div class="container">
      <div class="block-vue__wrap">
        <div class="block-vue__title">Cryptushka</div>
        <div class="block-vue__detail">
          <div class="block-vue__search-block search-block">
            <input
              v-model="search"
              v-on:keydown.enter="add"
              type="text"
              name="wallet"
              id="wallet"
              class="search-block__input"
              placeholder="Ведите название валюты"
            />
            <div class="search-block__examples-block examples-block">
              <ul class="examples-block__list">
                <li
                  v-for="todo in newJsonTitle.slice(0, 4)"
                  :key="todo.id"
                  class="examples-block__item"
                  @click="addName"
                >{{ todo }}</li>
              </ul>
            </div>
            <div class="search-block__error">Такой тикер уже добавлен</div>
            <button @click="add" type="button" class="search-block__add">
              <span>
                <svg
                  class="-ml-0.5 mr-2 h-6 w-6"
                  xmlns="http://www.w3.org/2000/svg"
                  width="30"
                  height="30"
                  viewBox="0 0 24 24"
                >
                  <path
                    fill="#000"
                    d="M13 7h-2v4H7v2h4v4h2v-4h4v-2h-4V7zm-1-5C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm0 18c-4.41 0-8-3.59-8-8s3.59-8 8-8 8 3.59 8 8-3.59 8-8 8z"
                  />
                </svg>
              </span>
              <span>Добавить</span>
            </button>
          </div>
          <template v-if="tickers.length">
            <div class="block-vue__chart-block chart-block" v-if="sel">
              <div class="chart-block__title">{{ sel.name }} - USD</div>
              <div class="chart-block__сhart сhart">
                <div class="сhart__list">
                  <span
                    v-for="(bar, idx) in normalizeGraph()"
                    :key="idx"
                    :style="{ height: `${bar}%` }"
                  ></span>
                </div>
              </div>
            </div>
          </template>
        </div>
        <div class="block-vue__cards-block cards-block">
          <ul class="cards-block__list">
            <li
              v-for="t in tickers"
              :key="t.name"
              @click="select(t)"
              :class="{
                'border-4': sel === t,
              }"
              class="cards-block__item item"
            >
              <div class="item__inner">
                <div class="item__title">{{ t.name }} - USD</div>
                <div class="item__value">{{ t.price }}</div>
                <button @click.stop="handleDelete(t)" class="item__delete" type="button">
                  <span>
                    <svg
                      class="h-5 w-5"
                      xmlns="http://www.w3.org/2000/svg"
                      viewBox="0 0 20 20"
                      fill="#718096"
                      aria-hidden="true"
                    >
                      <path
                        fill="#000"
                        fill-rule="evenodd"
                        d="M9 2a1 1 0 00-.894.553L7.382 4H4a1 1 0 000 2v10a2 2 0 002 2h8a2 2 0 002-2V6a1 1 0 100-2h-3.382l-.724-1.447A1 1 0 0011 2H9zM7 8a1 1 0 012 0v6a1 1 0 11-2 0V8zm5-1a1 1 0 00-1 1v6a1 1 0 102 0V8a1 1 0 00-1-1z"
                        clip-rule="evenodd"
                      />
                    </svg>
                  </span>
                  <span>Удалить</span>
                </button>
              </div>
            </li>
          </ul>
        </div>
      </div>
    </div>
  </section>
</template>
<script>
export default {
  name: "App",
  data() {
    return {
      ticker: "",
      tickers: [],
      sel: null,
      graph: [],
      //--------
      search: "",
      newJsonList: [],
    };
  },
  computed: {
    newJsonTitle() {
      return this.newJsonList.filter(item => item.indexOf(this.search) !== -1)
    },
  },
  beforeMount() {
    fetch("https://min-api.cryptocompare.com/data/all/coinlist")
      .then((response) => {
        return response.json();
      })
      .then((json) => {
        const newJson = Object.values(json.Data);
        this.newJsonList = newJson.map(newJsonItem => `${newJsonItem.Name}`);
      });


    const currentTicker = {
      name: this.ticker,
      price: "-",
    };
    /*setInterval(async () => {
      const newData = await fetch(
        `https://min-api.cryptocompare.com/data/price?fsym=BTC&tsyms=USD&api_key=b546ad2c2ba177e435a8172d43e2400f8bb40f1063fb7275801a5d1cceeaa80f`
      )
        .then(response => response.json())
        .then(data => console.log(data))
    }, 5000000000);
    */
  },
  methods: {
    addName() {

    },
    add() {
      const currentTicker = {
        name: this.search,
        price: "-",
      };
      setInterval(async () => {
        const f = await fetch(
          `https://min-api.cryptocompare.com/data/price?fsym=${currentTicker.name}&tsyms=USD&api_key=b546ad2c2ba177e435a8172d43e2400f8bb40f1063fb7275801a5d1cceeaa80f`
        )
        const data = await f.json();
        // currentTicker.price = data.USD > 1 ? data.USD.toFixed(2) : data.USD.toPrecision(2);
        this.tickers.find((t) => t.name === currentTicker.name).price =
          data.USD > 1 ? data.USD.toFixed(2) : data.USD.toPrecision(2);
        if (this.sel?.name === currentTicker.name) {
          this.graph.push(data.USD);
        }
      }, 5000);

    },
  },
};
</script>
<style src="./css/style.min.css"></style>
-->
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
            <button @click.stop="deleteTodo(t)">delete</button>
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