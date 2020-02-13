<template>
    <v-card>
        <v-card-title class="text-center justify-center py-6">
            <h1 class="font-weight-bold display-3 basil--text">Dashboard</h1>
        </v-card-title>
        <v-tabs v-model="tab" background-color="transparent" grow next-icon="mdi-arrow-right-bold-box-outline" prev-icon="mdi-arrow-left-bold-box-outline" show-arrows>
            <v-tab v-for="n in items" :key="n" class="d-flex align-center" chips :id="n.nombre + n.idConfig" :noAnillos="n.noAnillos">
                {{ n.texto }} 
                <v-btn color="red" text @click="removeTab(n)"><v-icon >mdi-close-circle-outline</v-icon></v-btn>
            </v-tab>
        </v-tabs>
        <v-tabs-slider color="yellow"></v-tabs-slider>
        <v-tabs-items v-model="tab">
            <v-tab-item v-for="n in items" :key="n">
                <!-- <v-card flat> -->

                    <!-- <v-card-text>{{n.texto }}</v-card-text> -->
                    <!-- <d-row>
                        <d-col lg v-for="(stats, idx) in smallStats" :key="idx" class="mb-3">
                            <SmallStats :id="`small-stats-${idx}`" variation="1" :chart-data="stats.datasets" :label="stats.label" :value="stats.value" :percentage="stats.percentage" :increase="stats.increase" :decrease="stats.decrease" />
                        </d-col>
                    </d-row> -->
                <!-- </v-card> -->
            </v-tab-item>
        </v-tabs-items>


        <!-- <v-card-text class="text-center">
            <v-btn text @click="removeTab(this)">Remove Tab</v-btn>
            <v-divider class="mx-4" vertical></v-divider>
            <v-btn text @click="cargarTab('prueba' + length++, 'prueba',4)">Add Tab</v-btn>
        </v-card-text> -->
  </v-card>
</template>

<script>
    
// import SmallStats from '../components/common/SmallStats.vue';

  export default {
      components:{
          //SmallStats,no mames
      },
      name:'TabsTotal',
      data(){
          return{
              length: 0,
              tabsActivos:[],
              nuevoTab:{
                  text:'',
                  idConfig:'',
                  nombre:'',
                  noAnillos:''
              },
              tab: [],
              items: [],
              text: '',
              cronometro: {
                tiempo: {
                    hora: 0,
                    minuto: 0,
                    segundo: 0,
                },
                listaDeTiempos: [],
                nombre: 'Cronometro',
                tiempoActivo: false,
                intervalo: null,
            },
          }  
      },
      watch: {
        //   length (val) {
        //       this.tab = val - 1
        //   },
          
      },
      methods:{
          cargarTab: function (tab) {
              var nuevoTab = {
                  texto: tab.text,
                  nombre:tab.mapAnillo,
                  noAnillos:tab.noAnillos,
                  idConfig:tab.idConfig
              }
              this.items.push(nuevoTab); 
              this.tabsActivos.push(nuevoTab.nombre)
          },
          removeTab: function (id) {
              var index = this.items.map(function(obj){
                  return obj.texto
              }).indexOf(id.texto)
              this.items.splice(index,1);
              this.$eventHub.$emit('removeTabTotal',index);
          },
          addZero(valor) {
              if (valor < 10) return `0${valor}`;
              return valor;
          },
      },
      created() {
          this.$eventHub.$on('cargarTab', (tab) => {
              var nuevoTab = {
                  nombre:tab.name,
                  texto:tab.text,
                  noAnillos:tab.noAnillos,
                  idConfig:tab.idConfig
              }
              this.items.push(nuevoTab);
          });
      },
      computed: {
    smallStats() {
      return [{
        label: 'Antes',
        value: '100%',
        percentage: 'Terminado',
        increase: true,
        labels: ['Label', 'Label', 'Label', 'Label', 'Label', 'Label'],
        datasets: [{
          label: 'Today',
          fill: 'start',
          borderWidth: 1.5,
          backgroundColor: 'rgba(0, 184, 216, 0.1)',
          borderColor: 'rgb(0, 184, 216)',
          data: [1, 3, 4, 6, 7, 8, 0],
        }],
      }, {
        label: 'Durante',
        value: '48%',
        percentage: 'Activo',
        increase: true,
        labels: ['Label', 'Label', 'Label', 'Label', 'Label', 'Label'],
        datasets: [{
          label: 'Today',
          fill: 'start',
          borderWidth: 1.5,
          backgroundColor: 'rgba(23,198,113,0.1)',
          borderColor: 'rgb(23,198,113)',
          data: [1, 2, 2, 1, 1, 1, 1],
        }],
      }, {
        label: 'Despues',
        value: '0%',
        percentage: '0%',
        increase: false,
        decrease: true,
        labels: ['Label', 'Label', 'Label', 'Label', 'Label', 'Label'],
        datasets: [{
          label: 'Today',
          fill: 'start',
          borderWidth: 1.5,
          backgroundColor: 'rgba(255,180,0,0.1)',
          borderColor: 'rgb(255,180,0)',
          data: [1, 1, 1, 1, 1, 1, 1],
        }],
      }, {
        label: 'Ejecuciones',
        value: '2 de 3',
        percentage: '49%',
        increase: false,
        decrease: true,
        labels: ['Label', 'Label', 'Label', 'Label', 'Label', 'Label'],
        datasets: [{
          label: 'Today',
          fill: 'start',
          borderWidth: 1.5,
          backgroundColor: 'rgba(255,65,105,0.1)',
          borderColor: 'rgb(255,65,105)',
          data: [1, 1, 1, 0, 0, 0, 0],
        }],
      }, {
        label: 'Contador',
        value: `${this.addZero(this.cronometro.tiempo.minuto)}:${this.addZero(this.cronometro.tiempo.minuto)}:${this.addZero(this.cronometro.tiempo.segundo)}`,
        percentage: '2.4%',
        increase: false,
        decrease: true,
        labels: ['Label', 'Label', 'Label', 'Label', 'Label', 'Label'],
        datasets: [{
          label: 'Today',
          fill: 'start',
          borderWidth: 1.5,
          backgroundColor: 'rgb(0,123,255,0.1)',
          borderColor: 'rgb(0,123,255)',
          data: [3, 2, 3, 2, 4, 5, 4],
        }],
      }];
    },
  },      
  }
</script>