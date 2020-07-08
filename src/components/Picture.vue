<template>
    <img :src="photo" alt="title" loading="lazy">
</template>

<script>
    export default {
        name: 'Picture',
        props: {
            picture: {
                type: Object,
                required: true
            }
        },
        data() {
            return{
                photo: this.picture.links[0].href,
                name: this.picture.data[0].title
            };
        },
        computed:{
            imgSource () {
                return this.photo
            }
        }
    }
</script>

<style lang="scss" scoped>
    img{
        width: 100%;
        height: auto;
        cursor: pointer;
    }
    img:hover{
        opacity: 0.9;
        transform: scale(1.01)
    }
</style>