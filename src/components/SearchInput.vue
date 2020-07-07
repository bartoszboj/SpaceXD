<template>
    <div class="searchWrapper">
        <div class="search">
            <input
            id="search"
            name="search"
            :value="value"
            :class="{ dark: dark}"
            @input="handleChange"
            />
        </div>
    </div>
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
        margin-top: 30px;
        height: 30px;
        border: 0;
        text-align: center;
        border-bottom: 1px solid rgb(209, 208, 208);
        color: rgb(209, 208, 208);
        background: none;
        transition: box-shadow .5s;
  }
  input:focus{
      box-shadow: 0 10px 20px -8px rgba(209, 209, 209, .3)
  }
  .dark{
      color: #1e3d4a;
      border-bottom: 1px solid #1e3d4a;
  }

</style>
