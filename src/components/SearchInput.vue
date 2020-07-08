<template>
            <input
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
  .dark{
      color: #404f55;
      border-bottom: 1px solid #404f55;
      width: 400px;
  }

</style>
