<template>
  <div class="app">
    <div :class="[{ flexStart: step === 1 } , 'wrapper']">
      <transition name="slideLogo">
        <p class="logo" v-if="step === 1">SpaceXD</p>
      </transition>

      <transition name='fade'>
        <HeroImage v-if="step === 0"/>
      </transition>

      <Heading v-if="step === 0"/>
      <SearchInput v-model="searchValue" @input="handleInput" :dark="step === 1"/>
      <ul class="results" v-if="results && !loading && step === 1">
        <Picture
        v-for="(item, index) in results" :key="item.data[0].nasa_id + index"
        :picture="item"
        />
      </ul>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import debounce from 'lodash.debounce';
import Heading from '@/components/Heading.vue';
import SearchInput from '@/components/SearchInput.vue';
import HeroImage from '@/components/HeroImage.vue';
import Picture from '@/components/Picture.vue'


const URL = 'https://images-api.nasa.gov/';

export default {
  name: 'App',
  data() {
    return {
      loading: false,
      step: 0,
      searchValue: '',
      results: [],
    };
  },
  components: {
    Heading,
    SearchInput,
    HeroImage,
    Picture
  },
  methods: {
    handleInput: debounce(function () {
      this.loading = true;
      axios.get(`${URL}search?q=${this.searchValue}&media_type=image`)
        .then((respo) => {
          console.log(respo.data.collection.items)
          this.results = respo.data.collection.items;
          this.loading = false;
          this.step = 1;
        })
        .catch((error) => {
          console.log(error);
        });
    }, 700),
  },
};
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@300;400;600;700;800&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@400;600;800&display=swap');

  .wrapper {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    position: relative;
    margin: 0;
    padding: 30px;
    width: 100%;
    height: 100vh;

    &.flexStart{
      justify-content: flex-start;
    }
  }
  *{
    box-sizing: border-box;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }

  input:focus, textarea:focus, select:focus{
    outline: none;
  }
  body{
    margin: 0;
    padding: 0;
    font-family: 'Montserrat', sans-serif;
  }

  .fade-enter-active, .fade-leave-active {
    transition: opacity .5s ease;
  }
  .fade-enter, .fade-leave-to {
    opacity: 0;
  }
  .slideLogo-enter-active, .slideLogo-leave-active {
    transition: margin-top .5s ease;
  }
  .slideLogo-enter, .slideLogo-leave-to {
    margin-top: 50%;
  }
  .slideInput-enter-active, .slideInput-leave-active {
    transition: margin-top .5s ease;
  }
  .slideInput-enter, .slideInput-leave-to {
    margin-top: 0;
  }
  .logo {
    position: absolute;
    top: 0;
    font-size: 1.2rem;
    letter-spacing: 5px;
    font-family: 'Press Start 2P';
  }
  .results{
    width: 100%;
    padding: 0;
    margin-top: 40px;
    column-count: 5;
    column-gap: 5px;
    // padding: 0;
    // display: flex;
    // flex-wrap: wrap;
    // justify-content: center;
    // align-items: center;
  }
  @media (max-width: 1200px){
    .results{
      column-count: 4;
    }
  }
  @media (max-width: 800px){
    .results{
      column-count: 3;
    }
  }
  @media (max-width: 480px){
    .results{
      column-count: 2;
    }
  }
  
</style>
