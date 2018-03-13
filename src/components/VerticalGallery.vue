<template>
    <div class="vertical-gallery" 
         ref="vertical">
        <div class="vertical-prev"
             ref="action"
             v-show="prevShow"
             @click="prevFun">
            <div class="prev-span"></div>
        </div>
        <div class="vertical-content"
             :style="{'height': `${height - actionHeight}px`, 'top': `${actionHeight/2}px`}">
            <div class="vertical-container"
                 ref="verticalContainer"
                 :style="{'top': `${contentTop}px`}">
                <slot></slot>        
            </div>
        </div>
        <div class="vertical-next"
             @click="nextFun"
             v-show="nextShow">
            <div class="next-span"></div>
         </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            height: 'auto',
            actionHeight: 0,
            contentHeight: 0,
            contentTop: 0,
            nextShow: true,
            prevShow: true,
            nextEnd: false
        };
    },
    props:{
        itemHeight: {
            type: Number,
            default: 100
        }
    },
    mounted() {
        const parentStyle = getComputedStyle(this.$refs.vertical.parentNode);
        this.height = parseInt(parentStyle.height, 10);
        const actionStyle = getComputedStyle(this.$refs.action);
        this.actionHeight = parseInt(actionStyle.height, 10) * 2;
        const contentStyle = getComputedStyle(this.$refs.verticalContainer);
        this.contentHeight = parseInt(contentStyle.height, 10);
        this.nextShow = false;
        this.prevShow = false;
        if (this.contentHeight > this.height - this.actionHeight) {
            this.nextShow = true;
        }
    },
    methods: {
        nextFun() {
            let isItemHeight = this.contentHeight + this.contentTop - this.height + this.actionHeight;
            if (isItemHeight > 0 && isItemHeight > this.itemHeight) {
                this.contentTop -= this.itemHeight;
                this.prevShow = true;
            }
            else {
                this.contentTop -= isItemHeight;
                this.nextShow = false;
                this.nextEnd = true;
            }
        },
        prevFun() {
            if (this.contentTop < 0 && this.contentTop + this.itemHeight < 0) {
                this.contentTop += this.itemHeight;
                this.nextShow = true;
            }
            else {
                this.contentTop = 0;
                this.prevShow = false;
            }
        }
    }

};

</script>

<style lang='less'>
    .vertical-gallery {
        position: relative;
        height: 100%;
        color: #666;
        .vertical-next,
        .vertical-prev {
            position: absolute;
            left: 0;
            width: 100%;
            height: 15px;
            background: #000;
            opacity: .5;
            cursor: pointer;
            z-index: 9;
            &:hover {
                opacity: 1;
            }
        }
        .vertical-next {
            bottom: 0;
        }
        .vertical-prev {
            top: 0;
        }
        .next-span,
        .prev-span {
            position: absolute;
            left: 50%;
            top: 50%;
            width: 10px;
            height: 5px;
            background: url('../assets/arrow.png') no-repeat;
            background-size: 100%;
            
        }
        .next-span {
            transform: translate(-50%, -50%);
        }
        .prev-span {
            transform: translate(-50%, -50%) rotate(-180deg);
        }
        .vertical-content {
            position: absolute;
            left: 0;
            width: 100%;
            overflow: hidden;
        }
        .vertical-container {
            position: absolute;
            left: 0;
            top: 0;
            width: 100%;
            transition: all .3s linear;
        }

    }
</style>
