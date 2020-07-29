<template>
    <div class=modalOuterWrapper>
        <div class="modalInnerWrapper">
                <div class="closeWrapper" @click="$emit('closeModal')">x</div>
            <div class="imgWrapper">
                <img :src="photo" alt="">
            </div>

            <div class="infoWrapper">
                <h2 class="title">{{ name }}</h2>
                <h3 v-if="date" class="additionalInfo"> {{ date }}</h3>
                <h3 v-if="creator" class="additionalInfo">{{ creator }}</h3>
                <h3 v-if="secondaryCreator" class="additionalInfo">{{ secondaryCreator }}</h3>
                <p class="description">{{ description }}</p>
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
                name: this.item.data[0].title,
                date: this.item.data[0].date_created,
                description: this.item.data[0].description,
                creator: this.item.data[0].center,
                secondaryCreator: this.item.data[0].secondary_creator


            }
        }
    }
</script>

<style lang="scss" scoped>
    .modalOuterWrapper{
        width: 100%;
        height: 100%;
        background-color: rgb(209, 208, 208);
        position: fixed;
        top: 0;
        left: 0;
    }
    .modalInnerWrapper{
        position: relative;
        height: 100%;
        width: 100%;
        padding: 10px;
        display: flex;
        flex-direction: column;
        align-items: center;
        overflow: auto;

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
            padding-top: 40px;
            display: flex;
            align-items: center;
            justify-content: center;
            max-width: 90%;

            img{
                object-fit: cover;
                max-width: 100%;
                max-height: 100%;
                 
            }
        }
        .infoWrapper{
            display: flex;
            flex-direction: column;
            width: 90%;

            .additionalInfo{
                font-weight: normal;
                font-size: 15px;
                padding: 0;
                margin: 0;
                font-style: oblique;
            }
            .description{
                text-indent: 1.5em;
            }
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
          justify-content: space-between;

          .imgWrapper{
              padding: 15px;
              height: 100%;
              width: 50%;
              max-width: 50%;
          }
          .infoWrapper{
              height: 100%;
              padding: 20px;
              max-width: 60%;
          }
      }
  }
</style>