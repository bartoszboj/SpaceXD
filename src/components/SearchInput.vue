<template>
            <input
            autocomplete="off"
            id="search"
            name="search"
            :value="value"
            :class="{ dark: dark}"
            @input="handleChange"
            />
</template>

<script>
export default {
  name: 'searchInput',
  props: {
      value: {
          type: String,
          required: true
      },
      dark: {
          type: Boolean,
          default: false
      }
  },
  methods:{
      handleChange(e) {
          this.$emit('input', e.target.value)
      }
  }
};
</script>

<style lang="scss" scoped>

input {
    width: 300px;
    margin-top: 30px;
    height: 30px;
    border: 0;
    font-size: 1.3rem;
    font-family: 'Orbitron';
    text-align: center;
    border-bottom: 1px solid rgb(209, 208, 208);
    color: rgb(209, 208, 208);
    background: none;
    transition: .5s;
  }

  input:focus{
      box-shadow: 0 10px 20px -8px rgba(209, 209, 209, .3)
  }

  input:-webkit-autofill,
  input:-webkit-autofill:hover,
  input:-webkit-autofill:focus,
  input:-webkit-autofill:active {
    transition: background-color 5000s ease-in-out 0s;
    -webkit-text-fill-color: #fff !important;
    font-family: 'Orbitron' !important;
    font-size: 1.3em !important;
    color: #404f55 !important;
  }
  .dark{
      color: #404f55;
      border-bottom: 1px solid #404f55;
      width: 400px;
  }

  @media (max-width: 1024px){

  }
  @media (max-width: 780px){

  }
  @media (max-width: 480px){
      input{
          width: 230px;
      }
      .dark{
          width: 300px;
      }
  }
  @media (max-width: 320px){
      input{
          width: 200px;
      }
      .dark{
          width: 260px;
      }
  }

</style>
