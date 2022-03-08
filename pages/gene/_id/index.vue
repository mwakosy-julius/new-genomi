<template>
  <div>
    <small>Gene ID: {{ $route.params.id }}</small>
    <hr>
    <div class="row d-flex justify-content-between">
      <div class="genetics col-sm-6 p-0 m-2">
        <div class="card">
          <div class="card-body">
            {{ gene }}
          </div>
          <p class="card-footer"><strong> GC Content: {{ GC }}%</strong></p>
        </div>
      </div>
      <div class="genetics col-sm-5 p-0 m-2">
        <div class="card">
          <div class="card-body">
            <Doughnut :data="ChartData" :options="ChartOptions" :height=400 />
          </div>
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
  data:()=>({
    gene: {},A:{},C:{},G:{},T:{}, GC:{},
    ChartData:{},ChartOptions:{},
  }), 
  
  async fetch(){
    const config = {
      headers:{
        Accept: "application/json"
      }
    };

    try {
      const res = await axios.get(`https://eutils.ncbi.nlm.nih.gov/entrez/eutils/efetch.fcgi?db=nuccore&id=${this.$route.params.id}&retmode=json&rettype=fasta`, config);
      let theGene = res.data.split("\n").slice(1).join("");
      this.gene = res.data.split('\n').join('');
      this.Total = theGene.length;
      this.A = (theGene.match(/\A/g) || []).length;
      this.T = (theGene.match(/\T/g) || []).length;
      this.G = (theGene.match(/\G/g) || []).length;
      this.C = (theGene.match(/\C/g) || []).length;
      this.GC = Math.round((this.G + this.C) / this.Total * 100);
      this.ChartData={
        labels: ['A', 'C', 'G', 'T'],
        datasets: [
          {
            label: 'Nucleotides',
            backgroundColor: [chartColors.red, chartColors.green, chartColors.yellow, chartColors.blue],
            data: [this.A, this.C, this.G, this.T],
            //data: [A, C, G, T],
            //data: [50,65,12,90],
            hoverOffser: 4,
            }
          ]
        };
      this.ChartOptions={
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
      };
        }catch (err){
          console.log(err)
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