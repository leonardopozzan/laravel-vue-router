<template>
    <div class="my-card">
        <div class="img-box">
            <img  v-if="project.image" :src="`${store.imagePath}${project.image}`" alt="">
            <img v-else src="https://picsum.photos/id/20/1920/1080" alt="">
        </div>
        <router-link :to="{name : 'single-project', params:{slug: project.slug}}">{{project.name}}</router-link>
        <div>{{ project.type.workflow }}</div>
        <div>{{ project.diff_lvl }}</div>
    </div>
</template>

<script>
import {store} from '../store';
    export default {
        data(){
            return{
                store
            }
        },
        props:{project : Object}
    }
</script>

<style lang="scss" scoped>
.my-card{
        width: calc(100% / 4 - 20px);
        margin: 20px 10px;
        .img-box{

        }
    }
</style>