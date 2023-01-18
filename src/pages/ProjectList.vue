<template>
    <div class="cards">
        <CardComponent v-for="(project,i) in projects" :key="i" :project="project"></CardComponent>
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
        };
    },
    methods: {
        getProjects() {
            axios.get(`${store.apiUrl}/projects`).then((response) => {
                // console.log(response.data.results);
                this.projects = response.data.results;
            });
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
</style>