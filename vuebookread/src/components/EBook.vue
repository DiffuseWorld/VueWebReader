<script setup lang="ts">
import Epub from 'epubjs'
import type { Book, Rendition } from 'epubjs'
import { onMounted, ref } from 'vue'
const DOWN_URL = '/static/5179.epub'
const book = ref<Book>()
const rendition = ref<Rendition>()
const isShow = ref(false)
const showBook = () => {
    book.value = Epub(DOWN_URL)
    // console.log(book.value)
    rendition.value = book.value.renderTo('read', {
        width: window.innerWidth,
        height: window.innerHeight
    })
    rendition.value.display()
}
onMounted(() => {
    showBook()
})

const prevPage = () => {
    if (rendition.value) {
        rendition.value.prev()
    }
}

const nextPage = () => {
    if (rendition.value) {
        rendition.value.next()
    }
}

const toggleTitleAndMenu = () => {
    isShow.value = !isShow.value
}
</script>

<template>
    <div class="ebook">
        <Transition name="slid-down">
            <div class="title-wrapper" v-show="isShow">
                <div class="left">
                    <div class="iconfont icon-fanhui"></div>
                </div>
                <div class="right">
                    <div class="icon-wrapper">
                        <span class="iconfont icon-gouwuche icon"></span>
                    </div>
                    <div class="icon-wrapper">
                        <span class="iconfont icon-yonghu icon"></span>
                    </div>
                    <div class="icon-wrapper">
                        <span class="iconfont icon-shezhi icon"></span>
                    </div>
                </div>
            </div>
        </Transition>

        <div class="read-wrapper" @click="">
            <div id="read">
                <div class="mask">
                    <div class="left" @click="prevPage"></div>
                    <div class="center" @click="toggleTitleAndMenu"></div>
                    <div class="right" @click="nextPage"></div>
                </div>
            </div>
        </div>

        <Transition name="slid-up">
            <div class="menu-wrapper" v-show="isShow">
                <div class="icon-wrapper">
                    <span class="iconfont icon-liebiao"></span>
                </div>
                <div class="icon-wrapper">
                    <span class="iconfont icon-huadongshuru"></span>
                </div>
                <div class="icon-wrapper">
                    <span class="iconfont icon-taiyang"></span>
                </div>
                <div class="icon-wrapper">
                    <span class="iconfont">A</span>
                </div>
            </div>
        </Transition>

    </div>
</template>

<style scoped lang="scss">
@import '@/assets/globa.scss';

.ebook {
    position: relative;

    .title-wrapper {
        position: absolute;
        top: 0;
        left: 0;
        right: 0;
        height: px2rem(48);
        z-index: 101;
        display: flex;
        background-color: white;
        box-shadow: 0 px2rem(8) px2rem(8) rgba(0, 0, 0, .15);

        .left {
            flex: 0 0 px2rem(60);
            @include center;
        }

        .right {
            flex: 1;
            display: flex;
            justify-content: flex-end;

            .icon-wrapper {
                flex: 0 0 px2rem(40);
                @include center;

                .iconfont {
                    font-size: px2rem(22);
                }
            }
        }

        &.slid-down-enter-from,
        &.slid-down-leave-to {
            transform: translate3d(0, -100%, 0);
        }

        &.slid-down-enter-to,
        &.slid-down-leave-from {
            transform: translate3d(0, 0, 0);
        }

        &.slid-down-enter-active,
        &.slid-down-leave-active {
            transition: all .3s linear;
        }
    }

    .read-wrapper {
        .mask {
            position: absolute;
            top: 0;
            left: 0;
            bottom: 0;
            right: 0;
            // background-color: yellow;
            z-index: 100;
            display: flex;

            .left {
                flex: 0 0 px2rem(100);
            }

            .center {
                flex: 1;
            }

            .right {
                flex: 0 0 px2rem(100);
            }
        }
    }

    .menu-wrapper {
        position: absolute;
        bottom: 0;
        left: 0;
        right: 0;
        height: px2rem(48);
        z-index: 101;
        display: flex;
        background-color: white;
        box-shadow: 0 px2rem(-8) px2rem(8) rgba(0, 0, 0, .15);

        .icon-wrapper {
            flex: 1;
            @include center;

            .iconfont {
                font-size: px2rem(24);
            }
        }
        &.slid-up-enter-from,&.slid-up-leave-to{
            transform: translate3d(0,100%,0);
        }
        &.slid-up-enter-to,&.slid-up-leave-from{
            transform: translate3d(0,0,0);
        }
        &.slid-up-enter-active,&.slid-up-leave-active{
            transition: all .3s linear;
        }
    }
}</style>