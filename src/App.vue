<script>

import Gallery from './components/Gallery.vue';

export default {

  name: "App",

  data(){
    return {
      list: [],
      page: 1,
      numberImages: 10,
      searchInput: ''
      }
  },

  created () {
    this.fetchData(this.page, this.numberImages)
  },

  computed: {
      filteredList() {
        return this.list.filter(pic => {
          let list = pic.author.toLowerCase().includes(this.searchInput.toLowerCase())
          console.log(list)
          return list
        })
      }
  },

  methods:{

    fetchData(page, numberImages){
      console.log(page, numberImages)
      fetch(`https://picsum.photos/v2/list?page=${page}&limit=${numberImages}`)
      .then(response => response.json())
      .then((data) =>{

          this.list = data
        });
    },
    nextPage(){

      this.fetchData(this.page+1, this.numberImages)
      this.page= this.page + 1
    },
    prevPage(){

      this.fetchData(this.page-1, this.numberImages)
      this.page = this.page-1
    },
    filterData(){
      console.log('...')
    }

  },
  components:{
    Gallery
  }
}

</script>

<template>


<input type="text" placeholder="Search author" v-model="searchInput" class="form-control" @change="filterData">

<p>{{searchInput}}</p>

    <Gallery v-bind:photos="filteredList"/>

    <p>Current page: {{ page }}</p>

  <div class="footer-buttons">
    <button class="prev-next-button" v-on:click="prevPage()">Prev</button>
    <button class="prev-next-button" v-on:click="nextPage()">Next</button>
    <select class="prev-next-button" v-model="numberImages" @change="fetchData(page, numberImages)">
      <option value=10 >Showing 10 pictures</option>
      <option value=20>Showing 20 pictures</option>
      <option value=50>Showing 50 pictures</option>
      <option value=100>Showing 100 pictures</option>
    </select>
  </div>

   

</template>

<style>

body{
  background: #eeeeee;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 2rem;
}

.footer-buttons{
  margin: 0 auto;
  width: 400px;
  justify-content: space-around;
  display: flex;
  margin-bottom: 3rem;
  
}
.prev-next-button{
  position: relative;
    cursor: pointer;
    display: inline-block;
    overflow: hidden;
    -webkit-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
    -webkit-tap-highlight-color: transparent;
    vertical-align: middle;
    z-index: 1;
    -webkit-transition: .3s ease-out;
    transition: .3s ease-out;

        border: none;
    border-radius: 2px;
    display: inline-block;
    height: 36px;
    line-height: 36px;
    padding: 0 16px;
    text-transform: uppercase;
    vertical-align: middle;
    -webkit-tap-highlight-color: transparent;

    text-decoration: none;
    color: #fff;
    background-color: #26a69a;
    text-align: center;
    letter-spacing: .5px;

}

</style>
