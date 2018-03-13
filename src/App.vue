<template>
    <div id="app">
        <div class="image-gallery">
             <vertical-gallery :itemHeight='120'>
                <div class="item"
                      v-for="(item, index) in imgs">
                    <img class="img-item" :src="item" alt="" />      
                </div>
             </vertical-gallery>
        </div>
    </div>
</template>

<script>
import VerticalGallery from './components/VerticalGallery';

export default {
    name: 'App',
    data() {
        return {
            imgs: [
                require('./assets/2.jpeg'),
                require('./assets/3.jpeg'),
                require('./assets/4.jpeg'),
                require('./assets/2.jpeg'),
                require('./assets/3.jpeg'),
                require('./assets/4.jpeg')
            ]
        }
    },
    components: {
        VerticalGallery
    }
    // beforeCreate() {
    //     console.log('--beforeCreate--');
    //     console.log(this.imgs);
    //     console.log(this.$el)
    // },
    // created() {
    //     console.log('--created--');
    //     console.log(this.imgs);
    //     console.log(this.$el);
    // },
    // beforeMount() {
    //     console.log('--beforeMount--');
    //     console.log(this.imgs);
    //     console.log(this.$el);
    // },
    // mounted() {
    //     console.log('--mounted--');
    //     console.log(this.imgs);
    //     console.log(this.$el);
    // }

};

</script>

<style lang="less">
html,
body {
    width: 100%;
    margin: 0;
}
#app {
    margin: 0 auto;
    width: 80%;
    min-height: 100%;
    .image-gallery {
        width: 200px;
        height: 500px;
        margin: 0 auto;
    }
    .item {
        height: 120px;
        box-sizing: border-box;
        padding: 2px 0;
        text-align: center;
    }
    .img-item {
        height: 100%;
        max-width: 100%;
    }
}
</style>
