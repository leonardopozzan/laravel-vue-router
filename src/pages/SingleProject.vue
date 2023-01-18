<template>
    <section>
        <div class="my-card py-5" v-if="project">
            <div class="img-box">
                <img  v-if="project.image" :src="`${store.imagePath}${project.image}`" alt="">
                <img v-else src="https://picsum.photos/id/20/1920/1080" alt="">
            </div>
            <div>{{ project.name }}</div>
            <div>{{ project.type.workflow }}</div>
            <div>{{ project.framework }}</div>
            <div>{{ project.diff_lvl }}</div>
            <div>{{ project.team }}</div>
            <div>{{ project.git_link }}</div>
            <div>{{ project.description }}</div>
        </div>
        <div v-else>
            <h3 class="text-center" >Loading...</h3>
        </div>
    </section>
</template>

<script>
import axios from 'axios';  
import {store} from '../store'
    export default {
        data(){
            return{
                store,
                project : null
            }
        },
        methods:{
            getPorject(){
                axios.get(`${store.apiUrl}/projects/${this.$route.params.slug}`).then((response)=>{
                    if(response.data.success){
                        this.project = response.data.results;
                    } else {
                        this.$router.push({name: 'not-found'});
                    }
                });
            }
        },
        mounted(){
            setTimeout(this.getPorject,2000);
        }
    }
</script>

<style lang="scss" scoped>
.my-card{
        width: calc(100% / 4 - 20px);
        // margin: 20px 10px;
        .img-box{

        }
    }
</style>