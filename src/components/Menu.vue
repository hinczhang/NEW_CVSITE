<!-- 菜单 -->

<template>
    <a-layout class="layout-menu">
        <!-- 头像 -->
        <div class="header">
            <span class="avatar ant-avatar ant-avatar-circle ant-avatar-image">
                <img draggable="false" src="../assets/avatar.jpg">
            </span>
            <span>{{banner.name|| '张炅焱'}}</span>
        </div>
        <!-- 菜单 -->
        <a-layout-content class="menu">
            <a-menu>
                <!-- 根据配置动态模块的内容和顺序 -->
                <a-menu-item v-if="isLanguageCH&&index%2 === 0" v-for="(m, index) in menus" v-bind:key="m.id">
                    <a-icon :type="m.icon" />
                    <a v-smooth-scroll :href="'#' + m.id" @click="closeMenuDrawer">{{m.name}}</a>
                </a-menu-item>
                <a-menu-item v-if="!isLanguageCH&&index%2 === 1" v-for="(m, index) in menus" v-bind:key="m.id">
                    <a-icon :type="m.icon" />
                    <a v-smooth-scroll :href="'#' + m.v_id" @click="closeMenuDrawer">{{m.name}}</a>
                </a-menu-item>
                <!-- <a-menu-item v-if="ch-en" v-for="(m, index) in menus" v-bind:key="m.id">
                    
                    <div>
                    <a-icon :type="m.icon" />{{ index }}
                    <a v-smooth-scroll :href="'#' + m.id" @click="closeMenuDrawer">{{m.name}}</a>
                    </div>
                </a-menu-item>
                <a-menu-item v-if="!ch-en&&index%2==1" v-for="(m, index) in menus" v-bind:key="m.id">
                    <a-icon :type="m.icon" />
                    <a v-smooth-scroll :href="'#' + m.id" @click="closeMenuDrawer">{{m.name}}</a>
                </a-menu-item> -->
            </a-menu>
            <a-row class="explain">
                语言/Язык/Language: <a-switch class="switch-me" checked-children="EN" un-checked-children="汉" v-model:checked="isLanguageCH" @change="onSwitchchange"></a-switch>
            </a-row>
        </a-layout-content>
        <!-- 菜单页脚 -->
        <a-layout-footer class="footer">
            <!-- 社交 -->
            <a-row type="flex" justify="center" align="middle" :gutter="2">
                <a-col span="24"><Social color="rgb(136,136,136)" :size="1.2"/></a-col>
            </a-row>
            <!-- 版权 -->
            <a-row type="flex" justify="center" align="middle" :gutter="2">
                <a-col span="24"><Copyrights color="rgb(136,136,136)" :size=".6"/></a-col>
            </a-row>
        </a-layout-footer>
    </a-layout>
</template>

<script lang="ts">
    import {Component, Vue} from 'vue-property-decorator';
    import Copyrights from '@/components/footer/Copyrights.vue';
    import Social from '@/components/footer/Social.vue';
    import {mapGetters} from 'vuex';

    @Component({
        components: {
            Copyrights,
            Social,
        },
        computed: {
            ...mapGetters(['banner', 'banner_en', 'menus']),
        },
    })
    export default class Menu extends Vue {
        private isLanguageCH = true;
        private closeMenuDrawer() {
            this.$emit('menuClick');
        }
        private onSwitchchange(checked: boolean | string | number, event: Event) {
            this.$emit('changeLanguage', checked);
        }
    }
</script>

<style scoped lang="scss">
    @import '../styles/variable';
    @import '../styles/switch.scss';
    .layout-menu {
        width: 100%;
        height: 100vh;
        text-align: center;

        .header, .menu, .footer {
            background-color: white !important;
        }

        .header {
            margin: 2rem auto;
            .avatar {
                width: 80px;
                height: 80px;
                line-height: 80px;
            }
            span {
                display: block;
                margin-top: .5rem;
                font-size: 1.2em;
                font-weight: 500;
                color: $--color-gray;
            }
        }

        .menu {
            * {
                font-size: 1em;
            }

            a {
                display: inline;
            }
        }

        .footer {
            padding: 10px;
            margin-bottom: 1rem;
            * {
                color: $--color-gray;
            }

            & > div {
                margin: .5rem auto;
            }
        }
    }
</style>
