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
        margin: 0;
        font-weight: 800;
    }
    .subclaim{
        margin: 20px 0 0 0;
        font-size: 14px;
    }
</style>
