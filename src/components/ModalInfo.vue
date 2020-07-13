<template>
    <div class=modalOuterWrapper>
        <div class="modalInnerWrapper">
                <div class="closeWrapper" @click="$emit('closeModal')">x</div>
            <div class="imgWrapper">
                <img :src="photo" alt="">
            </div>

            <div class="infoWrapper">
                <h2 class="title">Lorem Ipsum</h2>
                <p class="description">Lorem ipsum dolor sit amet, consectetur adipisicing elit. Id consequatur sint placeat veniam, neque unde quaerat molestiae tempora optio. Quaerat fugit ad voluptates hic eos laudantium exercitationem? Cupiditate, temporibus dolorum.</p>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'ModalInfo',
        props: {
            item: {
                type: Object,
                required: true
            }
        },
        data() {
            return{
                photo: this.item.links[0].href,
                name: this.item.data[0].title
            }
        }
    }
</script>

<style lang="scss" scoped>
    .modalOuterWrapper{
        max-width: 100%;
        height: 100%;
        background-color: rgb(209, 208, 208);
        position: fixed;
        top: 0;
        left: 0;
    }
    .modalInnerWrapper{
        position: relative;
        height: 100%;
        padding: 10px;
        display: flex;
        flex-direction: column;

        .closeWrapper{
            position: absolute;
            top: 0;
            right: 5px;
            font-size: 1.5rem;
            padding: 10px;
            color: #3b3b3b;
            cursor: pointer;

            :hover{
                color: black;
            }
        }
        .imgWrapper{
            margin-top: 15px;
            display: flex;
            justify-content: center;
            align-items: center;
            max-height: 90%;
            width: auto;

            img{
                max-width: 100%;
                height: auto;
                padding: 20px;
            }
        }
        .infoWrapper{
            height: auto;
            width: 100%;
        }
    }
  @media (min-width: 1024px){
      .modalOuterWrapper{
          min-width: 70%;
          max-width: 80%;
          height: 60%;
          top: 50%;
          left: 50%;
          transform: translate(-50%, -50%);

      }
      .modalInnerWrapper{
          flex-direction: row;
          align-items: center;

          .imgWrapper{
              margin: 0;

          }
      }
  }
</style>