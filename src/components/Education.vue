<!-- 经历 -->

<template>
    <div class="content" id="education">
        <ModuleHeader v-if="is_ch" :title="education.header.subtitle" :sub-title="education.header.title"/>
        <ModuleHeader v-if="!is_ch" :title="education.header.title" :sub-title="education.header.subtitle"/>
        <a-timeline>
            <a-timeline-item data-aos="fade-in" v-for="card in education.cards" v-bind:key="card.title + card.subtitle">
                <a-card class="education-card" :bordered="true" style="width: 100%">
                    <template slot="title">
                        <h1 class="title">{{card.title}}</h1>
                        <span v-if="!!card.subtitle" class="sub-title">{{card.subtitle}}</span>
                    </template>
                    <vue-markdown>{{card.md}}</vue-markdown>
                </a-card>
            </a-timeline-item>
        </a-timeline>
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
            education(): Module {
                if ( this.$props.is_ch ) {
                    return this.$store.getters.getModule('education');
                } else {
                    return this.$store.getters.getModule('education_en');
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
    .education-card {
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
    }
</style>
