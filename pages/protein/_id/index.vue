<template>
    <div>
      <small>Protein ID: {{ $route.params.id }}</small>
      <hr>
      <div class="container-flex d-flex flex-row">
        <div class="genetics d-flex col-md-6 card">
          <div class="card-body">
            {{ gene }}
          </div>
        </div>
        <div class="genetics d-flex col-md-6 card">
          <div class="card-body">
            <BarChart :data="graph.ChartData" :options="graph.ChartOptions" :height="400" />
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
  grey: 'rgb(201, 203, 207)',
  maroon: 'rgb(128, 0, 0)',
  navy: 'rgb(0, 0, 128)',
  brown: 'rgb(170, 110, 40)',
  olive: 'rgb(128, 128, 0)',
  teal: 'rgb(0, 128, 128)',
  apricot: 'rgb(255, 215, 180)',
  lavender: 'rgb(220, 190, 255)',
  lime: 'rgb(210, 245, 60)',
  cyan: 'rgb(70, 240, 240)',
  magenta: 'rgb(240, 50, 230)',
  pink: 'rgb(250, 190, 212)',
  beige: 'rgb(255, 250, 200)',
  mint: 'rgb(170, 255, 195)',
  
};

import axios from "axios";
import BarChart from "../../../components/BarChart.vue";


export default {
  components:{
    BarChart
  },
  
  async created(){
    const config = {
      headers:{
        Accept: "application/json"
      }
    };

    try {
      const res = await axios.get(`https://eutils.ncbi.nlm.nih.gov/entrez/eutils/efetch.fcgi?db=protein&id=${this.$route.params.id}&retmode=json&rettype=fasta`, config);
      let theGene = res.data.split("\n").slice(1).join("");
      this.gene = res.data.split('\n').join('');
      this.Total = theGene.length;
      this.A = (theGene.match(/\A/g) || []).length;
      this.C = (theGene.match(/\C/g) || []).length;
      this.E = (theGene.match(/\E/g) || []).length;
      this.F = (theGene.match(/\F/g) || []).length;
      this.G = (theGene.match(/\G/g) || []).length;
      this.H = (theGene.match(/\H/g) || []).length;
      this.I = (theGene.match(/\I/g) || []).length;
      this.K = (theGene.match(/\K/g) || []).length;
      this.L = (theGene.match(/\L/g) || []).length;
      this.M = (theGene.match(/\M/g) || []).length;
      this.N = (theGene.match(/\N/g) || []).length;
      this.P = (theGene.match(/\P/g) || []).length;
      this.Q = (theGene.match(/\Q/g) || []).length;
      this.R = (theGene.match(/\R/g) || []).length;
      this.S = (theGene.match(/\S/g) || []).length;
      this.T = (theGene.match(/\T/g) || []).length;
      this.U = (theGene.match(/\D/g) || []).length;
      this.V = (theGene.match(/\V/g) || []).length;
      this.W = (theGene.match(/\W/g) || []).length;
      this.Y = (theGene.match(/\Y/g) || []).length;

      this.graph.ChartData =  {
        labels: ['A', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'K', 'L', 'M', 'N', 'P', 'Q', 'R', 'S', 'T', 'V', 'W', 'Y'],
        datasets: [
          {
            label: 'Amino Acids',
            // backgroundColor: ["red", "orange", "yellow"],
            backgroundColor: [chartColors.red, chartColors.green, chartColors.yellow, chartColors.blue, chartColors.orange, 
                chartColors.purple, chartColors.grey, chartColors.maroon,
                chartColors.navy, chartColors.brown, chartColors.olive, chartColors.teal, chartColors.apricot, chartColors.lavender, chartColors.lime, 
                chartColors.cyan, chartColors.magenta, chartColors.pink, chartColors.beige, chartColors.mint,],
            data: [this.A, this.C, this.D, this.E, this.F, this.G, this.H, this.I, this.K, this.L, this.M, this.N, this.P, this.Q, this.R, this.S, this.T, this.V, this.W, this.Y],
            //data: [5, 3, 4, 2, 6, 8, 7, 5, 4 ,3 , 4, 2 , 4, 5, 9, 7 ,5, 8, 5 ,4 ],
            hoverOffser: 4,
            }
          ]
      };

      this.graph.ChartOptions =  {
        responsive: true,
        legend: {
                display: true,
            },
        title: {
              display: true,
              text: 'Amino Acid Content'
            },
        scales: {
          xAxes: [
            {
              gridLines: {
                display: false
              }
            }
          ],
          yAxes: [
            {
              ticks: {
                beginAtZero: true
              },
              gridLines: {
                display: false
              }
            }
          ]
        }
      };
    }catch (err){
      console.log(err)
    }
  },

  data(){
    return{
        gene: {},
        A: "",
        C: "",
        D: "",
        E: "",
        F: "",
        G: "",
        H: "",
        I: "",
        K: "",
        L: "",
        M: "",
        N: "",
        P: "",
        Q: "",
        R: "",
        S: "",
        T: "",
        V: "",
        W: "",
        Y: "",
        
        get graph(){
          return{
            ChartData:{},
            ChartOptions:{},
          }
        },

        
      
      
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