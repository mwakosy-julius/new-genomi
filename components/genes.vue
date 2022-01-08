<template>
  <div>
    <search v-on:search-text="searchText"/>

    <div class="container-flex d-flex flex-row">
      <nav class="col-md-3 col-lg-2 d-md-block bg-light sidebar sidebar-collapse collapse">
        <div class="position-sticky pt-3">
          <ul class="nav flex-column">
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
      </nav>

      <main class="d-flex col-md-9 ms-sm-auto col-lg-10 px-md-4" role="main">
        <div class="container-fluid">
          <div v-for="(id, index) in list" :key="id" class="gene">
            <nuxt-link :to="'gene/' + id">{{listid[index]}}</nuxt-link>
          </div>
        </div>
      </main>
    </div>
  </div>  
</template>

<script>
import axios from "axios";
import search from "./GeneSearch.vue";

export default {
  components:{
    search
  },
  head(){
    return{
      title: "New Genomi",
      meta:[
        {
          hid: "description",
          name: "description",
          content: "Best place for Gene searching"
        }
      ]
    }
  },
  data(){
    return{
      listid: [],
      list:  [],
    }
  },
  methods: {
    async searchText(text){
      const config = {
      headers:{
        Accept: "application/json"
      }
    };

    try { 

      const res = await axios.get(`https://eutils.ncbi.nlm.nih.gov/entrez/eutils/esearch.fcgi?db=nuccore&term=${text.replace(/ /g, '+')}&rettype=fasta&retmode=json&retmax=10`, config);
      let result = res.data.esearchresult.idlist;
      this.list = result;
      const rep = await axios.get(`https://eutils.ncbi.nlm.nih.gov/entrez/eutils/efetch.fcgi?db=nuccore&id=${result}&rettype=fasta&retmode=json`, config);
      let tempos = []
      let temp = rep.data.split('>').slice(1);
      temp.forEach(element => {
        tempos.push(element.split('\n', 1));
      });
      this.listid = tempos;
    }catch (err){
      console.log(err)
    }
  }
    }
}
</script> 

<style type="text/css">
  body {
  font-size: .875rem;
}
.navbar-brand {
  padding-top: .75rem;
  padding-bottom: .75rem;
  font-size: 1rem;
  background-color: rgba(0, 0, 0, .25);
  box-shadow: inset -1px 0 0 rgba(0, 0, 0, .25);
}

.navbar .navbar-toggler {
  top: .25rem;
  right: 1rem;
}

.navbar .form-control {
  padding: .75rem 1rem;
  border-width: 0;
  border-radius: 0;
}

.form-control-dark {
  color: #fff;
  background-color: rgba(255, 255, 255, .1);
  border-color: rgba(255, 255, 255, .1);
}

.form-control-dark:focus {
  border-color: transparent;
  box-shadow: 0 0 0 3px rgba(255, 255, 255, .25);
}

@media (max-width: 767.98px) {
  .sidebar {
    top: 5rem;
  }
}
.sidebar {
  position: relative;
  top: 0;
  height: 39.0rem;
  bottom: 0;
  left: 0;
  z-index: 100; 
  box-shadow: inset -1px 0 0 rgba(0, 0, 0, .1);
}
.sidebar-sticky {
  position: relative;
  top: 0;
  height: calc(100vh - 48px);
  padding-top: .5rem;
  overflow-x: hidden;
  overflow-y: auto; /* Scrollable contents if viewport is shorter than content. */
}

.sidebar .nav-link {
  font-weight: 500;
  color: #333;
}

.sidebar .nav-link.active {
  color: #2470dc;
}

.sidebar-heading {
  font-size: .75rem;
  text-transform: uppercase;
}
.gene {
    border: 0.1rem dotted #ccc;
    margin:1rem 0.5rem;
    padding: 0.5rem;
}
</style>
