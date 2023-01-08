<!-- 经历 -->

<template>
    <div class="content" id="project">
        <ModuleHeader v-if="is_ch" :title="project.header.subtitle" :sub-title="project.header.title"/>
        <ModuleHeader v-if="!is_ch" :title="project.header.title" :sub-title="project.header.subtitle"/>
        <a-timeline>
            <a-timeline-item data-aos="fade-in" v-for="card in project.cards" v-bind:key="card.title + card.subtitle">
                <a-card class="project-card" :bordered="true" style="width: 100%">
                    <template slot="title">
                        <h1 class="title">{{card.title}}</h1>
                        <span v-if="!!card.subtitle" class="sub-title">{{card.subtitle}}</span>
                    </template>
                    <a-row>
                        <a-col :span="16" ><vue-markdown>{{card.md}}</vue-markdown></a-col>
                        <a-col :span="8" style="display: flex;justify-content:center;align-items:center;"><img class="img-style" :src="require('../assets/' + card.img)"/></a-col>
                    </a-row>
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
            project(): Module {
                if ( this.$props.is_ch ) {
                    return this.$store.getters.getModule('project');
                } else {
                    return this.$store.getters.getModule('project_en');
                }
            },
        },
    })
    export default class About extends Vue {
    }
</script>

<style scoped lang="scss">
    @import '../styles/variable';

    .project-card {
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
    
    .img-style {
        width: 60%;
    }
</style>
