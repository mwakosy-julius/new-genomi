<template>
    <div>
      <small>Genome ID: {{ $route.params.id }}</small>
      <hr>
      <div class="container-flex d-flex flex-row">
        <div class="genetics d-flex col-md-6 card">
          <div class="card-body">
            {{ gene }}
          </div>
          <p class="card-footer"><strong> Total Nucleotides: {{ Total }}</strong></p>
          {{graph.ChartData}}
        </div>
        <div class="genetics d-flex col-md-6 card">
          <div class="card-body">
            <Doughnut :data="graph.ChartData" :options="graph.ChartOptions" :height=400 />
          </div>          
        </div>
      </div>
    </div>
</template>
<script>
const chartColors = {
  red: 'rgb(255, 99, 132)',
  orange: 'rgb(255, 159, 64)',
  yellow: 'rgb(255, 205, 86)',
  green: 'rgb(75, 192, 192)',
  blue: 'rgb(54, 162, 235)',
  purple: 'rgb(153, 102, 255)',
  grey: 'rgb(201, 203, 207)'
};

import axios from "axios";
import Doughnut from "../../../components/Doughnut.vue";


export default {
  components:{
    Doughnut
  },

  async created(){
    const config = {
      headers:{
        Accept: "application/json"
      }
    };

    try {
      const res = await axios.get(`https://eutils.ncbi.nlm.nih.gov/entrez/eutils/efetch.fcgi?db=genome&id=${this.$route.params.id}&retmode=json&rettype=fasta`, config);
      let theGene = res.data.split("\n").slice(1).join("");
      this.gene = res.data.split('\n').join('');
      this.Total = theGene.length;
      this.A = (theGene.match(/\A/g) || []).length;;
      this.T = (theGene.match(/\T/g) || []).length;
      this.G = (theGene.match(/\G/g) || []).length;
      this.C = (theGene.match(/\C/g) || []).length;
      this.GC = Math.round((this.G + this.C) / this.Total * 100);
      this.graph.ChartData =  {
              labels: ['A', 'C', 'G', 'T'],
              datasets: [
                {
                  label: 'Nucleotides',
                  backgroundColor: [chartColors.red, chartColors.green, chartColors.yellow, chartColors.blue],
                  //data: [50, 30, 40, 20],
                  data: [this.A, this.C, this.G, this.T],
                  //data: [],
                  hoverOffser: 4,
                  }
                ]
            };
      this.graph.ChartOptions = {
        responsive: true,
              legend: {
                      display: true,
                  },
              title: {
                    display: true,
                    text: 'Nucleotide Content'
                  },responsive: true,
              legend: {
                      display: true,
                  },
              title: {
                    display: true,
                    text: 'Nucleotide Content'
                  },
      }
    }catch (err){
      console.log(err)
    }
  },  
  data(){
    return{
        gene: {},
        Total: "",
        GC: "",
        G: "",
        C: "",
        T: "",
        A: "",
        
        get graph(){
          return {
            ChartData : {
              
            },
            ChartOptions : {
                  
            },
          }
        }
        
    }
      
  },
  

}
</script>

<style>
.genetics {
    border: 0.1rem dotted #ccc;
    margin:1rem 0.5rem;
}
</style>