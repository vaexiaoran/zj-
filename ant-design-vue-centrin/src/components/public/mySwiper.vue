<template>
  <swiper :options="swiperOption" ref="mySwiper" v-bind:style="{ height: sheight, width:swidth }">
    <swiper-slide v-for="(item,index) in swiperData" :key="index" :class='{cutImg:cut}'>
      <div><img v-bind:style="{ height: sheight}" :src="dataType === 'arr'?item:item.url||item.path" alt=""></div>
    </swiper-slide>
    <div class="swiper-pagination" slot="pagination"  v-if="swiperData.length>1" ></div>
    <!--v-if="swiperData.length>1"-->
  </swiper>
</template>

<script type="text/ecmascript-6">
  import { swiper, swiperSlide } from 'vue-awesome-swiper'
  export default {
    props: {
      swiperData: {
        type: Array,
        default: null
      },
      sheight: {
        type: String,
        default: '4rem'
      },
      swidth: {
        type: String,
        default: '100%'
      },
      swidthNumber: {
        type: Number,
        default: 0
      },

      dataType: {
        type: String,
        default: 'json'
      },
      refreshDelay: {
        type: Number,
        default: 20
      },
      cut:{
        type: Boolean,
        default: false
      },
      type:{
        type: Number,
        default: 1
      }
    },
    data() {
      return {
        swiperOption: {
          notNextTick: true,
          autoplay: {
            stopOnLastSlide: false,
            delay:3000,
            disableOnInteraction: false,
          },
          pagination: {
            el: '.swiper-pagination'
          },
          paginationClickable :true,
          loop: true,
        }
      }
    },
    created () {
      if(this.swiperData.length==1){
        this.swiperData.loop=false
      }
    },
    mounted() {
      if(this.swiperData.length==1){
        this.swiper.autoplay.stop();
      }

      if(this.type===2){
        this.$nextTick(() => {
          if(document.querySelectorAll('.swiper-pagination').length>0){
            document.querySelectorAll('.swiper-pagination')[0].style.width=(this.swidthNumber-0.6)+'rem'
            document.querySelectorAll('.swiper-pagination')[0].style.margin='0 .3rem'
          }
          var a=document.querySelectorAll('.swiper-pagination-bullet');
          if(a.length>0){
            for(var i=0;i<a.length;i++){
              a[i].style.width=100/this.swiperData.length+'%'
              a[i].style.borderRadius='0'
              a[i].style.margin='0'
              a[i].style.height='0.02rem'
            }
          }
        })

      }

    },
    methods: {
      destroySwiper(){
        this.swiper.destroy()
      }
    },

    computed: {
      swiper() {
        return this.$refs.mySwiper.swiper
      }
    },
    components: {
      swiper,
      swiperSlide
    },
    watch: {
      swiperData() {
        setTimeout(() => {
          this.swiper.refresh()
        }, this.refreshDelay)
      }
    }
  }
</script>

<style lang='less' scoped>

  /*.cutImg{*/
  /*div{*/
  /*width: 100%;height: 100%;visibility: visible;display: -webkit-box;-webkit-box-pack: center;-webkit-box-align: center;*/
  /*background: #fff;*/
  /*img{*/
  /*width:100%; height:100%;object-fit:cover;*/
  /*}*/
  /*}*/
  /*}*/
  .swiper-pagination{
    width: 100%;

  }



  .swiper-pagination-bullets .swiper-pagination-bullet{
    height: 2px !important;
    border-radius: 0 !important;
    background: #666 !important;
    opacity: .1 !important;
    margin: 0 0 !important;
  }
  .swiper-pagination-bullet-active{
    background: #666 !important;
    opacity: .8 !important;
  }
</style>
