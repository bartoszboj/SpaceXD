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
      <SearchInput v-model="searchValue" @input="handleInput" :darken="step === 1"/>
      <div class="results" v-for="(item, index) in results" :key="index">
        <p>{{ item.links[0].href }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import debounce from 'lodash.debounce';
import Heading from '@/components/Heading.vue';
import SearchInput from '@/components/SearchInput.vue';
import HeroImage from '@/components/HeroImage.vue';

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
  },
  methods: {
    handleInput: debounce(function () {
      this.loading = true;
      axios.get(`${URL}search?q=${this.searchValue}&media_type=image`)
        .then((respo) => {
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
    top: 20px;
  }
  
</style>
