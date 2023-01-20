<template>
    <header>
        <nav class="navbar navbar-expand-lg bg-body-tertiary">
            <div class="container-fluid">
                <a class="navbar-brand" href="#"><img src="/img/logo3.png" alt="" id="logo"></a>
                <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
                    <span class="navbar-toggler-icon"></span>
                </button>
                <div class="collapse navbar-collapse" id="navbarSupportedContent">
                    <ul class="navbar-nav me-auto mb-2 mb-lg-0 my-links-list">
                        <li class="nav-item" v-for="(link ,i) in navLinks" :key="i">
                            <router-link :to="{name : link.routeName}"><span>{{link.label}}</span></router-link>
                        </li>
                    </ul>
                </div>
            </div>
        </nav>
    </header>
</template>

<script>
    export default {
        name: 'AppHeader',
        data(){
            return {
                navLinks: [
                    {
                        label: 'Home',
                        routeName: 'home'
                    },
                    {
                        label: 'Projects',
                        routeName: 'projects'
                    },
                ]
            }
        }
        
    }
</script>

<style lang="scss" scoped>
nav{
    #logo{
        width: 75px;
    }
    .my-links-list{
        li{
            padding: 0 1rem;
            font-size: 1.1rem;
            font-weight: bold;
            span{
                color: black;
            }
        }
    }
}
</style>