<template>
    <section>
        <div class="text-center py-3">
            <div class="btn btn-primary" v-if="!project && !show">Loading....</div>
            <button class="btn btn-primary" v-else-if="project && !show" @click="show = !show">Mostra il progetto</button>
            <button class="btn btn-primary" v-else  @click="show = !show">Torna al gioco</button>
        </div>
        <div class="my-card py-5" v-if="show">
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
        <div v-show="!show">
            <h3 class="text-center">Gioca finchè aspetti l'api</h3>
            <GameComponent></GameComponent>
        </div>
    </section>
</template>

<script>
import axios from 'axios';  
import {store} from '../store'
import GameComponent from '../components/GameComponent.vue'
    export default {
        components: {GameComponent},
        data(){
            return{
                store,
                project : null,
                show: false
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
            setTimeout(this.getPorject,3000);
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