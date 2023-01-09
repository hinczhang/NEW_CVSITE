<!-- 经历 -->

<template>
    <div class="content" id="recommend">
        <ModuleHeader v-if="is_ch" :title="recommend.header.subtitle" :sub-title="recommend.header.title"/>
        <ModuleHeader v-if="!is_ch" :title="recommend.header.title" :sub-title="recommend.header.subtitle"/>
        <a-carousel dot-position="left" autoplay>
            <div style="width:100%;height: 100%;align-items: center;" v-for="card in recommend.cards" v-bind:key="card.title + card.subtitle">
                <a-card hoverable class="recommend-card" :bordered="true" style="width: 80%">
                    <template slot="title">
                        <h1 class="title">{{card.title}}</h1> 
                        <span v-if="!!card.subtitle" class="sub-title">{{card.subtitle}}</span>
                    </template>
                    <a-row>
                        <a-col :span="16" ><vue-markdown>{{card.md}}</vue-markdown></a-col>
                        <a-col :span="8">
                            <a-row>
                                <img class="avatar" :src="require('../assets/avatars/' + card.img)"/>
                            </a-row>
                            <a-row style="margin: 0 auto; text-align: center;">
                                <a-button style="margin-top: 7%;" type="primary" shape="round" :href="'./rec/' + card.file">
                                    <a-icon type="download" />
                                </a-button>
                            </a-row>
                        </a-col>
                    </a-row>
                </a-card>
            </div>
        </a-carousel>
    </div>
</template>

<script lang="ts">
    import {Component, Vue} from 'vue-property-decorator';
    import ModuleHeader from '@/components/module/ModuleHeader.vue';
    import {Module} from '@/api/user_interface';
    // tslint:disable-next-line:no-var-requires
    import VueMarkdown from 'vue-markdown';

    @Component({
        props: ['is_ch'],
        components: {
            ModuleHeader,
            VueMarkdown,
        },
        computed: {
            recommend(): Module {
                if ( this.$props.is_ch ) {
                    return this.$store.getters.getModule('recommend');
                } else {
                    return this.$store.getters.getModule('recommend_en');
                }
            },
        },
    })
    export default class About extends Vue {
    }
</script>

<style scoped lang="scss">
    @import '../styles/variable';
    .content{
        background-color:rgb(245, 245, 245);
    }
    .recommend-card {
        .title {
            width: 100%;
            font-size: 1rem;
            overflow: scroll;
            margin: 0;
        }

        .sub-title {
            width: 100%;
            font-size: .5rem;
            display: block;
            margin-top: .5rem;
        }
        margin: 0 auto;
    }
    
    .img-style {
        width: 60%;
    }

    .avatar{
        border-radius: 200px 198px 200px 200px;
        -moz-border-radius: 200px 198px 200px 200px;
        -webkit-border-radius: 200px 198px 200px 200px;
        border: 0px solid #000000;
        height: 60%;
        margin: 0 auto;
    }

    .download{
        font-family: georgia, serif;
        font-size: 20px;
        font-weight: bold;
        word-spacing: 1.8pt;
        color: black;
        
    }

    .ant-carousel :deep(.slick-slide) {
        text-align: center;
        height: 160px;
        line-height: 160px;
        background: #364d79;
        overflow: hidden;
    }

    .ant-carousel :deep(.slick-slide h3) {
        color: #fff;
    }

</style>
