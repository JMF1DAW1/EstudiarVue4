<template>
    <div>
        <br>
        <div>
            <button type="button" style="margin:15px" class="btn btn-primary" @click="mostrar100">Mostrar los que tienen mas de 100 </button>
            <button type="button" class="btn btn-primary" @click="mostrarPaginas">Mostrar los que tienen pages </button>
        </div>
        <hr>
        <div v-if="mostrarForks">
            <div v-for="(item, id) in repolist" :key="id">   
                <div v-if="item.forks_count >= 100">
                    <ul class="list-group">
                        <li class="list-group-item d-flex justify-content-between align-items-center">
                            <p><a :href="item.html_url" target="_blank"><abbr :title="item.description">{{ item.full_name}} </abbr></a></p>
                            <span class="badge badge-primary badge-pill"> {{ item.forks_count }} <img src="imagen_fork.png" style="width:8px"></span>
                        </li>
                    </ul>
                </div>  
            </div>
        </div>

        <div v-if="mostrarPages">
            <div v-for="(item, id) in repolist" :key="id">   
                <div v-if="item.has_pages">
                    <ul class="list-group">
                        <li class="list-group-item d-flex justify-content-between align-items-center">
                            <p><a :href="item.html_url" target="_blank"><abbr :title="item.description">{{ item.full_name}} </abbr></a></p>
                            <p> {{ item.has_pages}} </p>
                            <span class="badge badge-primary badge-pill"> {{ item.forks_count }} <img src="imagen_fork.png" style="width:8px"></span>
                        </li>
                    </ul>
                </div>  
            </div>
        </div>
        
    </div>
</template>

<script>
export default {
    name: 'GitHubRepos',
    data: function() {
        return {
            mostrarForks: false,
            mostrarPages: false,
        }
    },
    props: [
        'repolist'
    ],
     methods: {
        mostrar100: function() {
            this.mostrarForks= !this.mostrarForks;
            this.mostrarPages = false;
        }, 
        mostrarPaginas: function() {
            this.mostrarPages = !this.mostrarPages;
            this.mostrarForks = false;
        }
    }
}
</script>

<style scoped>
</style>
