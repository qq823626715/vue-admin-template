<template>
    <div class="navbar">
        <!-- <hamburger :is-active="sidebar.opened" class="hamburger-container" @toggleClick="toggleSideBar" />

        <breadcrumb class="breadcrumb-container" /> -->
        <logo />
        <div class="right-menu">
            <div class="avatar-container">
                <div class="avatar-wrapper">
                    <div class="user-box">
                        <el-avatar :src="avatar+'?imageView2/1/w/80/h/80'" :size="40" />
                        <span class="user-name">某某某</span>
                    </div>
                    <el-button type="text" size="medium" icon="el-icon-switch-button" @click.native="logout">退出登录</el-button>
                </div>
            </div>
            <!-- <el-dropdown class="avatar-container" trigger="click">
                <div class="avatar-wrapper">
                    <img :src="avatar+'?imageView2/1/w/80/h/80'" class="user-avatar">
                    <i class="el-icon-caret-bottom" />
                </div>
                <el-dropdown-menu slot="dropdown" class="user-dropdown">
                    <router-link to="/">
                        <el-dropdown-item>
                            Home
                        </el-dropdown-item>
                    </router-link>
                    <a target="_blank" href="https://github.com/PanJiaChen/vue-admin-template/">
                        <el-dropdown-item>Github</el-dropdown-item>
                    </a>
                    <a target="_blank" href="https://panjiachen.github.io/vue-element-admin-site/#/">
                        <el-dropdown-item>Docs</el-dropdown-item>
                    </a>
                    <el-dropdown-item divided @click.native="logout">
                        <span style="display:block;">Log Out</span>
                    </el-dropdown-item>
                </el-dropdown-menu>
            </el-dropdown> -->
        </div>
    </div>
</template>

<script>
import { mapGetters } from 'vuex'
// import Breadcrumb from '@/components/Breadcrumb'
// import Hamburger from '@/components/Hamburger'
import Logo from '@/layout/components/Sidebar/Logo'

export default {
    components: {
        // Breadcrumb,
        Logo
        // Hamburger
    },
    computed: {
        ...mapGetters([
            'sidebar',
            'avatar'
        ])
    },
    methods: {
        toggleSideBar() {
            this.$store.dispatch('app/toggleSideBar')
        },
        async logout() {
            await this.$store.dispatch('user/logout')
            this.$router.push(`/login?redirect=${this.$route.fullPath}`)
        }
    }
}
</script>

<style lang="scss" scoped>
@import "~@/styles/variables.scss";

.navbar {
    height: $headerHeight;
    overflow: hidden;
    position: relative;
    background: #fff;
    box-shadow: 0 1px 4px rgba(0,21,41,.08);

    // .hamburger-container {
    //     line-height: 46px;
    //     height: 100%;
    //     float: left;
    //     cursor: pointer;
    //     transition: background .3s;
    //     -webkit-tap-highlight-color:transparent;

    //     &:hover {
    //         background: rgba(0, 0, 0, .025)
    //     }
    // }

    .breadcrumb-container {
        float: left;
    }

    .right-menu {
        float: right;
        height: 100%;
        line-height: 50px;
        vertical-align: middle;

        &:focus {
            outline: none;
        }

        .right-menu-item {
            display: inline-block;
            padding: 0 8px;
            height: 100%;
            font-size: 18px;
            color: #5a5e66;
            vertical-align: text-bottom;

            &.hover-effect {
                cursor: pointer;
                transition: background .3s;

                &:hover {
                    background: rgba(0, 0, 0, .025)
                }
            }
        }

        .avatar-container {
            margin-right: 40px;

            .avatar-wrapper {
                position: relative;
                height: $headerHeight;
                display: flex;
                flex-direction: row;
                align-items: center;

                .user-box{
                    margin-right: 30px;
                    display: flex;
                    flex-direction: row;
                    align-items: center;
                    color: #808080;
                    font-size: 16px;
                    .user-name{
                        margin-left: 10px;
                        cursor: pointer;
                    }
                }
                .el-button--text{
                    color: #808080;
                    font-size: 16px;
                }
            }
        }
    }
}
</style>
