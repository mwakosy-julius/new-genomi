<template>
  <nav class="navbar navbar-dark sticky-top bg-dark flex-md-nowrap p-0 shadow">
    
    <a class="navbar-brand col-md-3 col-lg-2 me-0 px-3" href="../">Genomi</a>
    <button class="navbar-toggler d-md-none position-absolute collapsed" type="button" data-bs-toggle="collapse" data-bs-target="#sidebarMenu" aria-controls="sidebarMenu" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="sidebarMenu">
      <ul class="navbar-nav me-auto mb-2 mb-lg-0">
        <li class="nav-item">
          <nuxt-link class="nav-link active" to="./gene">
            Genes
          </nuxt-link>
        </li>
        <li class="nav-item">
          <nuxt-link class="nav-link" to="./protein">
            Protein
          </nuxt-link>
        </li>
      </ul>
    </div>

    <form @submit.prevent="onsubmit" class="d-flex flex-row w-100">
      <input class="form-control form-control-dark w-100" v-model="text" type="text" placeholder="Search Gene ...." aria-label="Search">
      <div class="navbar-nav">
        <div class="nav-item text-nowrap">
          <input type="submit" class="nav-link px-3 me-0 dark btn" value="submit"/>
        </div>
      </div>
    </form>
  </nav>
</template>

<script>
export default {
    name: "searchGenes",
    data(){
        return{
            text: ""
        }
    },
    methods:{
        onsubmit(){
            this.$emit("search-text", this.text);
            this.text = "";
        }
    }
}
</script>

<style>

</style>