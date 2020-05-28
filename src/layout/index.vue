<template>
    <div :class="classObj" class="app-wrapper">
        <el-container>
            <el-header :height="headerHeight">
                <div :class="{'fixed-header':fixedHeader}">
                    <navbar />
                </div>
            </el-header>
            <el-container>
                <!-- <el-aside width="210px"> -->
                <!-- </el-aside> -->
                <el-main>
                    <div v-if="device==='mobile'&&sidebar.opened" class="drawer-bg" @click="handleClickOutside" />
                    <sidebar class="sidebar-container" />
                    <div class="main-container">
                        <app-main />
                    </div>
                </el-main>
            </el-container>
        </el-container>
    </div>
</template>

<script>
import { Navbar, Sidebar, AppMain } from './components'
import ResizeMixin from './mixin/ResizeHandler'
import Variables from '@/styles/variables.scss'

export default {
    name: 'Layout',
    components: {
        Navbar,
        Sidebar,
        AppMain
    },
    mixins: [ResizeMixin],
    computed: {
        sidebar() {
            return this.$store.state.app.sidebar
        },
        device() {
            return this.$store.state.app.device
        },
        fixedHeader() {
            return this.$store.state.settings.fixedHeader
        },
        classObj() {
            return {
                hideSidebar: !this.sidebar.opened,
                openSidebar: this.sidebar.opened,
                withoutAnimation: this.sidebar.withoutAnimation
                // mobile: this.device === 'mobile' //去除手机适配
            }
        },
        headerHeight() {
            return Variables.headerHeight
        }
    },
    methods: {
        handleClickOutside() {
            this.$store.dispatch('app/closeSideBar', { withoutAnimation: false })
        }
    }
}
</script>

<style lang="scss" scoped>
  @import "~@/styles/mixin.scss";
  @import "~@/styles/variables.scss";

  .app-wrapper {
    @include clearfix;
    position: relative;
    height: 100%;
    width: 100%;

    &.mobile.openSidebar{
      position: fixed;
      top: 0;
    }
    & .el-header{
        padding: 0;
        position: fixed;
        left: 0;
        right: 0;
        top: 0;
    }
    & .el-main{
        padding: 0;
        background-color: #F7FAF8;
        margin-top: $headerHeight;
    }
  }
  .drawer-bg {
    background: #000;
    opacity: 0.3;
    width: 100%;
    top: 0;
    height: 100%;
    position: absolute;
    z-index: 999;
  }

  .fixed-header {
    position: fixed;
    top: 0;
    right: 0;
    z-index: 9;
    width: calc(100% - #{$sideBarWidth});
    transition: width 0.28s;
  }

  .hideSidebar .fixed-header {
    width: calc(100% - 54px)
  }

  .mobile .fixed-header {
    width: 100%;
  }
</style>
