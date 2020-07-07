<template>
    <div>

    </div>
</template>

<script>
    export default {
        name: Picture,
        props: {
            picture: {
                type: Object,
                required: true
            }
        },
        data() {
            return{
                photo: this.item.links[0].href,
                title: this.item.data[0].title
            };
        }
    }
</script>

<style lang="scss" scoped>

</style>