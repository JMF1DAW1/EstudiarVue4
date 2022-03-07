<template>
    <div style="padding: 25px">
        <!-- TODO: Crear componente GitHub -->
        <div>
            <input type="text" style="width: 100%"  placeholder="introduce un usuario de github" v-model="user" @keydown.enter="obtenerUsuario">
        </div>

        <div v-if="userValid">
            <div class="row justify-content-center">
                <div class="col-3">
                    <div class="card" style="width: 18rem;">
                        <img class="card-img-top" :src="userData.avatar_url" alt="Card image cap">
                        <div class="card-body">
                            <h5 class="card-title"> {{ userData.login }} </h5>
                            <button type="button" class="btn btn-primary" @click="obtenerRepositorios">Repositorio</button>
                            <a :href="userData.html_url"  target="_blank"> URL de GITHUB</a> 
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <div v-if="mostrarRepo">
            <GitHubRepos :repolist="repos"></GitHubRepos>
        </div>
    </div>
</template>

<script>

import GitHubRepos from "./GitHubRepos.vue"

export default {
    name: 'GitHub',
    components: {
        GitHubRepos
    },
    data: function() {
        return {
            user: "",
            userData: {},
            userValid: false,
            repos: {},
            mostrarRepo: false, 
        }
    },
    methods: {
        obtenerUsuario: function() {
            var userAuth = process.env.VUE_APP_USERNAME || "user";
            var passAuth = process.env.VUE_APP_USERTOKEN || "pass";
            let url = "https://api.github.com/users/" + this.user;
            
            let headers = new Headers();
            headers.set('Authorization', 'Basic ' + btoa(userAuth + ":" + passAuth));

            fetch(url, {method:'GET',
                    headers: headers,
                })
                .then(res => res.json())
                .then(response => {
                    console.log(response);
                    this.userData = response;
                    this.userValid = true;
                })
                .catch((error) => {
                    console.error(error);
                    });
        },
        obtenerRepositorios: function() {
             var userAuth = process.env.VUE_APP_USERNAME || "user";
            var passAuth = process.env.VUE_APP_USERTOKEN || "pass";
            let url = this.userData.repos_url
            
            let headers = new Headers();
            headers.set('Authorization', 'Basic ' + btoa(userAuth + ":" + passAuth));

            fetch(url, {method:'GET',
                    headers: headers,
                })
                .then(res => res.json())
                .then(response => {
                    console.log(response);
                    this.repos = response;
                    this.mostrarRepo = true;
                })
                .catch((error) => {
                    console.error(error);
                    });
        }
    }
}
</script>

<style scoped>
</style>
