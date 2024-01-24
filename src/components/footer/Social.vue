<!-- 社交 -->

<template>
    <div class="social" :style="{'font-size': size + 'em'}">
        <!-- github -->
        <a :style="{color: color}" :href="social['github'] || 'https://github.com/manerfan'" target="_blank"><a-icon type="github" /></a>
        <!-- 微信 -->
        <a-popover arrowPointAtCenter>
            <template slot="content"><img style="width: 150px; max-width: 80vw; height: auto;"  alt="ZJY" src="../../assets/wechat.png"/></template>
            <a :style="{color: color}"><a-icon type="wechat" /></a>
        </a-popover>
        <!-- zhihu -->
        <a :style="{color: color}" :href="social['zhihu'] || 'https://twitter.com/manerfan_china'" target="_blank"><a-icon type="zhihu" /></a>
        <!-- linkedin -->
        <a :style="{color: color}" :href="social['linkedin'] || 'https://www.linkedin.com/in/%E6%B0%B8%E6%B0%B8-%E6%A8%8A-705071104/'" target="_blank"><a-icon type="linkedin" /></a>
        <!-- Bilibili -->
        <a :style="{color: color}" :href="social['bilibili'] || 'https://space.bilibili.com/318494938'" target="_blank"><a-icon type="video-camera" /></a>


    </div>
</template>

<script lang="ts">
    import {Component, Vue} from 'vue-property-decorator';
    import {mapGetters} from 'vuex';

    @Component({
        components: {
        },
        props: {
            color: String,
            size: Number,
        },
        computed: {
            ...mapGetters(['social']),
        },
    })
    export default class Social extends Vue {
    }
</script>

<style scoped lang="scss">
    .social {
        &>* {
            margin: 0.5em;
        }
    }
</style>

