<template>
<div class="wrapper">
<swiper :options="swiperOption" >
<swiper-slide v-for=" item of swiperList "  :key="item.id" >
<img class="swiper-img" :src="item.imgUrl" />
</swiper-slide>
<div class="swiper-pagination" slot="pagination"></div>
<!-- <div class="swiper-button-prev" slot="button-prev"></div>
<div class="swiper-button-next" slot="button-next"></div> -->
<!-- <div class="swiper-scrollbar" slot="scrollbar"></div> -->
</swiper>
</div>
</template>

<script>
export default {
    name: 'homeSwiper',
    data() {
        return {
            swiperOption: {
                pagination: '.swiper-pagination',
                loop: true, // 循环轮播
                autoplay: 3000 // 时间
            },
            swiperList: [
                {
                    id: '001',
                    imgUrl: 'https://source.qunarzz.com/site/images/wap/home/recommend/iphoneplus/dujia_shuqi_banner_20180710.jpg'
                },
                {
                    id: '002',
                    imgUrl: 'https://source.qunarzz.com/site/images/wap/home/recommend/iphoneplus/sc_sqdc_20180727.jpg'
                },
                {
                    id: '003',
                    imgUrl: 'https://source.qunarzz.com/site/images/wap/home/recommend/iphoneplus/20180716_wap_11043.jpg'
                }
            ]
        }
    }
}
</script>

<style lang="stylus" scoped>
// >>> 样式穿透，不受scoped的限制了
.wrapper >>> .swiper-pagination-bullet-active
    background: #fff

.wrapper //在最外层套个div可以
    overflow: hidden
    margin 0 auto 
    width: 50%
    height: 0
    padding-bottom:12.3% //宽高比始终是12.3
    
.swiper-img
    width: 100%
</style>