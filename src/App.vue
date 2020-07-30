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
      <div class="results" v-if="results.length > 1 && !loading && step === 1">
        <Picture
        v-for="(item, index) in results" :key="item.data[0].nasa_id + index"
        :picture="item"
        @click.native="openModal(item)"
        />
      </div>
      <p class="center" v-if="results.length < 1 && step === 1" >hmmm... didn't hear about it</p>
      
      <transition name="bounce">
        <modal-info v-if="modalOpen" :item="modalItem" @closeModal="modalOpen = false"></modal-info>
      </transition>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import debounce from 'lodash.debounce';
import Heading from '@/components/Heading.vue';
import SearchInput from '@/components/SearchInput.vue';
import HeroImage from '@/components/HeroImage.vue';
import Picture from '@/components/Picture.vue';
import ModalInfo from '@/components/ModalInfo.vue';


const URL = 'https://images-api.nasa.gov/';

export default {
  name: 'App',
  data() {
    return {
      loading: false,
      step: 0,
      searchValue: '',
      results: [],
      modalOpen: false,
      modalItem: null,
    };
  },
  components: {
    Heading,
    SearchInput,
    HeroImage,
    Picture,
    ModalInfo
  },
  methods: {
    openModal (item) {
      this.modalOpen = true;
      this.modalItem = item;
    },
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
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@300;400;600;700;800&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@400;600;800&display=swap');
  
  *{
    box-sizing: border-box;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }
  body{
    margin: 0;
    padding: 0;
    font-family: 'Montserrat', sans-serif;
    }
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
    .center{
      position: absolute;
      top: 40%;
      left: 50%;
      transform: translate(-50%, -50%);
      font-size: 1.2rem;
    }
  }

  input:focus, textarea:focus, select:focus{
    outline: none;
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

  .bounce-enter-active {
    animation: bounce-in .4s;
  }
  .bounce-leave-active {
    animation: bounce-in .5s reverse;
  }
  @keyframes bounce-in {
    0% {
      margin-top: 100vh;
      opacity: 0;
    }
    100% {
      margin-top: 0;
      opacity: 1;
    }
  }
  .logo {
    position: absolute;
    top: 0;
    font-size: 1.2rem;
    letter-spacing: 5px;
    font-family: 'Press Start 2P';
    user-select: none;
  }
  .results{
    width: 100%;
    padding: 0;
    margin-top: 40px;
    column-count: 5;
    column-gap: 5px;
  }
  @media (max-width: 1024px){
    .results{
      column-count: 4;
    }
  }
  @media (max-width: 780px){
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
