<template>
  <div id="bannerItem">
    <div v-for="(banners, i) in this.$store.state.mainList" :key="i" >
      <router-link :to="`/brand/${banners.id}`" :a = a>
         <!-- <img :src="require(`../assets/banner/${banners.image}`)" :alt="`${banners.id}`"> -->
         <lazy-image :src="require(`../assets/banner/${banners.image}`)"></lazy-image>
        <div id="BrandName">
          <p>{{banners.name}}</p>
        </div>
        <div id="mvBrandName">
            <p>{{banners.name}}</p>
        </div>
      </router-link>
    </div>
  </div>
</template>

<script>
import LazyImage from '@/LazyImage.vue'
export default {
  components: { LazyImage },
    name : 'MainBanner',
    data(){
      return {
        a : 0,
      }
    },
    computed : {
      imageUrl() {
        require(this.$store.state.mainList.image)
        return this.imageUrl
      }
    },
    created() {
      const main = this.$route.params.id
      this.$store.dispatch('FETCH_MAIN', main)
    }
}
</script>

<style lang="scss" scoped> 
  #bannerItem {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
    padding-top: 2%;
    max-width: 1400px;
    width: 100%;
    margin: 0 auto;
    
    > div {
      width: 49%;
      position: relative;
      // padding: 2% 0 0 0;
      img {
        width: 100%;
        padding: 1% 0;
      }

      #BrandName{
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        background-color: rgba(255, 255, 255, 0.5);
        width: 100%;
        height: 100%;
        opacity: 0;

        &:hover {
          opacity: 1;
        }

        p {
          position: absolute;
          top: 50%;
          left: 50%;
          transform: translate(-50%, -50%);
          width: 100%;
          text-align: center;
          font-size: 3rem;
          color: #333;
          font-weight: 700;
        }
      }

    }
    #mvBrandName {
      p {
        text-align: center;
        font-size: 1.5rem;
        font-weight: 700;
        display: none;
      }
    }
  }

    @media (min-width:250px) and (max-width:1200px) {
      #bannerItem {
        display: block;

        > div {
          width: 100%;

          #BrandName {
            &:hover {
              opacity: 0;
            }
          }
        }

        #mvBrandName {
          p {
            display: block;
          }
        }
      }
    }
</style>