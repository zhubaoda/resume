<style lang="less" scoped>
.wchat {
    height: 100vh;
    width: 100%;
    .swiper {
        width: 100%;
        height: 100%;
    }
}
</style>
<template>
    <div class="wchat" id="wchat">
        <swiper :options="swiperOption" class="swiper">
            <swiper-slide v-for="(slide,index) in swiperSlides">
                <div class="box" v-if="index == 0">
                    <div class="top">
                        <rotates :param="param"></rotates>
                    </div>
                </div>
                <div class="box" v-if="index == 1">
                    <div class="top">
                        <clock :param="param"></clock>
                    </div>
                </div>
                <div class="box" v-if="index == 2">
                    <div class="top">
                        <card :param="param"></card>
                    </div>
                </div>
            </swiper-slide>
            <div class="swiper-pagination" slot="pagination"></div>
        </swiper>
    </div>
</template>
<script>
import rotates from '../components/rotate'
import clock from '../components/clock'
import card from '../components/card'
export default {
    name: 'wchat',
    data() {
        return {
            swiperOption: {
                // autoplay: 3500,
                direction: 'vertical',
                setWrapperSize: true,
                pagination: '.swiper-pagination',
                paginationClickable: true,
                mousewheelControl: true,
                observeParents: true,
            },
            swiperSlides: [1, 2, 3],
            param: {
                w: 300,
                h: 500
            }
        }
    },
    components: {
        rotates,
        clock,
        card
    },
    methods: {
        
    },
    mounted() {
        console.log(document.getElementById('wchat').clientWidth);
        this.param.w = document.getElementById('wchat').clientWidth;
        this.param.h = document.getElementById('wchat').clientHeight;
        // setInterval(() => {
        //     console.log('simulate async data')
        //     let swiperSlides = this.swiperSlides
        //     if (swiperSlides.length < 5) swiperSlides.push(swiperSlides.length + 1)
        // }, 3000000000000)
    }
}
</script>
