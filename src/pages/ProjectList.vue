<template>
    <div class="cards">
        <CardComponent v-for="(project,i) in projects" :key="i" :project="project"></CardComponent>
        <button @click="getPage('prev')" :disabled="currentPage == 1">prev</button>
        <button v-for="n in pagination.last_page" @click="getPage(n)" :disabled="currentPage == n">{{ n }}</button>
        <button @click="getPage('next')" :disabled="currentPage == pagination.last_page">next</button>
    </div>
</template>

<script>
import axios from 'axios';  
import CardComponent from '../components/CardComponent.vue';
import {store} from '../store';
export default {
    data() {
        return {
            store,
            projects: [],
            currentPage : 1,
            pagination : {last_page : 1}
        };
    },
    methods: {
        getProjects() {
            const data = {
                params: {'page' : this.currentPage}
            }
            axios.get(`${store.apiUrl}/projects`,data).then((response) => {
                // console.log(response.data.results)
                // console.log(response.data.results);
                this.projects = response.data.results.data;
                this.pagination = response.data.results;
            });
        },
        getPage(page){
            if(page == 'next'){
                this.currentPage++;
            }else if (page == 'prev'){
                this.currentPage--;
            }else{
                this.currentPage = page;
            }
            this.getProjects();
        }
    },
    mounted() {
        this.getProjects();
    },
    components: { CardComponent }
}
</script>

<style lang="scss" scoped>
.cards{
    display: flex;
    align-items: flex-start;
    flex-wrap: wrap;
    
}
button{
    padding: 0.5rem;
}
</style>