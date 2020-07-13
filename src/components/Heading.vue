<template>
  <div class="headingWrapper">
    <h1 class="claim">SpaceXD</h1>
    <p class="subclaim">
      Explore our amazing galaxy and discover places you'll never go to. Begin your journey now!
    </p>
    <p class="subclaim">
        All you must to is to type anything space-related.
        </p>
  </div>
</template>

<script>
export default {
  name: 'Heading',
};
</script>

<style lang="scss" scoped>
    .headingWrapper {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    text-align: center;
    color: rgb(209, 208, 208);
    text-shadow: 3px 3px 5px black;
    }
    .claim{
        font-size: 50px;
        font-family: 'Press Start 2P', sans-serif;
        margin: 0;
        font-weight: 700;
        letter-spacing: 5px;
    }
    .subclaim{
        font-family: 'Orbitron';
        margin: 20px 0 0 0;
        font-size: 14px;
    }

    @media (max-width: 1024px){

    }
    @media (max-width: 780px){

    }
    @media (max-width: 480px){
        .claim{
          font-size: 35px;
        }
        .subclaim{
          font-size: 16px;
        }
    }
    @media (max-width: 320px){
      .claim{
        font-size: 30px;
      }
      .subclaim{
        font-size: 13px;
      }
    }
</style>
