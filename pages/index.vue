<template>
  <div class="body">
    <div class="header">
      <h1>Buscador de libros</h1>
    </div>
    <div class="searcher">
      <input class="textSearcher" placeholder="Enter something to search" v-model="search" autofocus>
      <button class="buttonSearcher" :disabled="!search" v-on:click="searchData">Buscar</button>
    </div>
    <section class="page-contain">
      <a href="#" class="data-card" v-for="book in results">
        <h3>{{book.title}}</h3>
        <h4>{{book.first_publish_year}}</h4>
        <p v-if="book.author_name">{{book.author_name.join(', ')}}</p>
      </a>
    </section>
  </div>
</template>

<script>
export default {
  components: {
  },
  data() {
    return {
      search: '',
      results: []
    }
  },
  methods: {
    async searchData() {
      console.log('Searching')
      const data = await this.$axios.$get("http://openlibrary.org/search.json?q=" + this.search.replace(" ", "+"))
      this.results = data.docs;
    }
  }
}
</script>

<style>
.header {
  text-align: center;
  padding: 20px 0px;
  color: #8b8a8b;
  font-size: 40px;
}
.textSearcher {
  font-size: 16px;
  font-size: max(16px, 1em);
  font-family: inherit;
  padding: 0.25em 0.5em;
  background-color: #fff;
  border: 2px solid #8b8a8b;
  border-radius: 4px;
  width: 30vw;
}
.buttonSearcher {
  background: #753BBD;
  background-image: -webkit-linear-gradient(top, #753BBD, #A754C4);
  background-image: -moz-linear-gradient(top, #753BBD, #A754C4);
  background-image: -ms-linear-gradient(top, #753BBD, #A754C4);
  background-image: -o-linear-gradient(top, #753BBD, #A754C4);
  background-image: linear-gradient(to bottom, #753BBD, #A754C4);
  -webkit-border-radius: 28;
  -moz-border-radius: 28;
  border-radius: 28px;
  font-family: Arial;
  color: #ffffff;
  font-size: 20px;
  padding: 10px 20px 10px 20px;
  text-decoration: none;
  height: 100%;
}
.buttonSearcher:hover {
  background: #A754C4;
  background-image: -webkit-linear-gradient(top, #A754C4, #753BBD);
  background-image: -moz-linear-gradient(top, #A754C4, #753BBD);
  background-image: -ms-linear-gradient(top, #A754C4, #753BBD);
  background-image: -o-linear-gradient(top, #A754C4, #753BBD);
  background-image: linear-gradient(to bottom, #A754C4, #753BBD);
  text-decoration: none;
  transform: scale(1.02);
}
.buttonSearcher:disabled {
  background: #8B8A8B;
}
.textSearcher:focus {
  outline: none;
}
.searcher {
  text-align: center;
}
.card {
  width: 30vw;
  min-height: 100px;
  padding: 15px;
  text-align: center;
  background: #242625;
  border-radius: 10px;
  box-shadow: 10px 10px 20px #1b1c1b, -10px -10px 20px #2d302f;
  color: #FFF;
  margin-top: 40px;
}
.content {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  margin: 30px 30px;
}
.body {
  background-color: #E7F3F1;
  height: 100%;
  min-height: 100vh;
}

* {
  box-sizing: border-box;
}

.page-contain {
  display: flex;
  min-height: 100vh;
  align-items: center;
  justify-content: center;
  background: #E7F3F1;
  padding: 2em;
  font-family: 'Open Sans', sans-serif;
  flex-wrap: wrap;
  justify-content: flex-start;
  align-content: space-between;
  align-items: stretch;
}

.data-card {
  display: flex;
  flex-direction: column;
  width: 20.75em;
  min-height: 20.75em;
  overflow: hidden;
  border-radius: .5em;
  text-decoration: none;
  background: white;
  margin: 1em;
  padding: 2.75em 2.5em;
  box-shadow: 0 1.5em 2.5em -.5em rgba(#000000, .1);
  transition: transform .45s ease, background .45s ease;
}

.data-card > h3 {
  color: #2E3C40;
  font-size: 3.5em;
  font-weight: 600;
  line-height: 1;
  padding-bottom: .5em;
  margin: 0 0 0.142857143em;
  border-bottom: 2px solid #753BBD;
  transition: color .45s ease, border .45s ease;
}

.data-card > h4 {
  color: #627084;
  text-transform: uppercase;
  font-size: 1.125em;
  font-weight: 700;
  line-height: 1;
  letter-spacing: 0.1em;
  margin: 0 0 1.777777778em;
  transition: color .45s ease;
}

.data-card > p {
  opacity: 0;
  color: #FFFFFF;
  font-weight: 600;
  line-height: 1.8;
  margin: 0 0 1.25em;
  transform: translateY(-1em);
  transition: opacity .45s ease, transform .5s ease;
}

.data-card:hover {
  background: #753BBD;
  color: #FFFFFF;
  transform: scale(1.02);
}
.data-card:hover > h3 {
  color: #FFFFFF;
  border-bottom-color: #A754C4;
}

.data-card:hover > h4{
  color: #FFFFFF;
}

.data-card:hover > p{
  opacity: 1;
  transform: none;
}

@keyframes point {
  0% {
    transform: translateX(0);
  }
  100% {
    transform: translateX(.125em);
  }
}
</style>