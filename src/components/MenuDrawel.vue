<template>
      <v-list >
        <v-autocomplete v-model="model" :items="nodos" :search-input.sync="search" label="Nodos actuales" prepend-icon="mdi-magnify"> 
        </v-autocomplete>
        <!-- <v-autocomplete v-model="model" :items="nodos" :search-input.sync="search" label="Nodos" placeholder="Buscar Nodo" prepend-icon="mdi-city"></v-autocomplete> -->
        <!-- <v-text-field solo chips label="Search" multiple append-icon="mdi-magnify"><i class="mdi-magnify"></i></v-text-field> -->
        <div v-for="item in items" :key='item'> 
          <v-row v-if="item.heading" :key="item.heading" align="center">
            <v-col cols="6">
              <v-subheader v-if="item.heading">
                {{ item.heading }}
              </v-subheader>
            </v-col>
            <v-col cols="6" class="text-center">
              <a href="#!" class="body-2 black--text">EDIT</a>
            </v-col>
          </v-row>
          <v-list-group v-else-if="item.children" :key="item.text" v-model="item.model" :prepend-icon="item.model ? item.icon : item['icon-alt']" append-icon="">
            <template v-slot:activator>
              <v-list-item-content>
                <v-list-item-title>
                  {{ item.text }}
                </v-list-item-title>
              </v-list-item-content>
            </template>
            <v-list-item v-for="(child, i) in item.children" :key="i" link>
              <v-list-item-action v-if="child.icon">
                <v-icon>{{ child.icon }}</v-icon>
              </v-list-item-action>
              <v-list-item-content>
                <v-list-item-title>
                  {{ child.text }}
                </v-list-item-title>
              </v-list-item-content>
            </v-list-item>
          </v-list-group>
          <v-list-item v-else :key="item.text" link @click="cargarTabDraw(item)">
            <v-list-item-action>
              <v-icon>{{ item.icon }}</v-icon>
            </v-list-item-action>
            <v-list-item-content>
              <v-list-item-title>
                {{ item.text }}
              </v-list-item-title>
            </v-list-item-content>
          </v-list-item>
        </div>
      </v-list>
</template>
<script>
  export default {
    name:'menuDrawel',
    data(){
      return {
        search: null,
        drawer: null,
        tabsActivos:[],
        items: [
          {icon: 'mdi-desktop-mac-dashboard', text: 'Dashboard', name: 'Dashboard', idConfig:null, noAnillos:null,mapAnillo:null},
          { icon: 'mdi-clipboard-check', text: 'Validaciones', name: 'Validaciones', idConfig:null, noAnillos:null,mapAnillo:null},
          { icon: 'mdi-desktop-tower-monitor', text: 'Equipos', name: 'Equipos', idConfig:null, noAnillos:null,mapAnillo:null},
          { icon: 'mdi-access-point-network', text: 'Endpoints', name: 'Endpoints' , idConfig:null, noAnillos:null,mapAnillo:null},
          { icon: 'mdi-account-circle-outline', text: 'Usuarios', name: 'Usuarios', idConfig:null, noAnillos:null,mapAnillo:null},
          { icon: 'mdi-account-key-outline', text: 'Roles', name: 'Roles', idConfig:'', noAnillos:null,mapAnillo:null},
          { icon: 'mdi-history', text: 'Historial' , name: 'Historial', idConfig:'', noAnillos:null,mapAnillo:null},
          // {
        //   icon: 'mdi-chevron-up',
        //   'icon-alt': 'mdi-chevron-down',
        //   text: 'LabelsUsuari',
        //   model: true,
        //   children: [
        //     { icon: 'mdi-plus', text: 'Create label' },
        //   ],
        // },
        // {
        //   icon: 'mdi-chevron-up',
        //   'icon-alt': 'mdi-chevron-down',
        //   text: 'More',
        //   model: false,
        //   children: [
        //     { text: 'Import' },
        //     { text: 'Export' },
        //     { text: 'Print' },
        //     { text: 'Undo changes' },
        //     { text: 'Other contacts' },
        //   ],
        // },
        // { icon: 'mdi-settings', text: 'Settings' },
        // { icon: 'mdi-message', text: 'Send feedback' },
        // { icon: 'mdi-help-circle', text: 'Help' },
        // { icon: 'mdi-cellphone-link', text: 'App downloads' },
        // { icon: 'mdi-keyboard', text: 'Go to the old version' },
        ],
        model: null,
        nodos: [
          {text: 'GDL_CANADA', name: 'GDLCANADA', idConfig:'2', noAnillos:'2',mapAnillo:'GDL_CANADA' },
          {text: 'PACHUCA SOTO', name: 'PACHUCASOTO', idConfig:'3', noAnillos:'3',mapAnillo:'PACHUCA SOTO'},
          {text: 'PACHUCA CENTRO', name: 'PACHUCACENTRO', idConfig:'4', noAnillos:'4',mapAnillo:'PACHUCA CENTRO'},
        ],
      }
    },
    methods:{
          cargarTabDraw(tab) {
            for(var ro=0; ro<this.items.length;ro++){
              if(this.items[ro].text==tab.text){
                var existet = 0;
                for(var ta=0; ta<this.tabsActivos.length;ta++){
                  if(this.tabsActivos[ta] == tab.text){
                    existet=1;
                  }
                }
                if(existet==0){
                  this.tabsActivos.push(tab.text);
                  this.$eventHub.$emit('cargarTab',tab); 
                }
                else{
                  document.getElementById(tab.name + tab.idConfig).click();
                }
              }
            }
          },
          removeTab: function (index) {
              this.tabsActivos.splice(index,1);
          },
      },
      watch: {
        search(val) {
          for(var ro=0; ro<this.nodos.length;ro++){
            if(this.nodos[ro].text==val){
              var existe=0;
              for(var ta=0; ta<this.tabsActivos.length;ta++){
                if(this.tabsActivos[ta] == val){
                  existe=1;
                }
              }
              if(existe==0){
                this.tabsActivos.push(this.nodos[ro].text)
                this.$eventHub.$emit('cargarTab',this.nodos[ro]); 
              }else{
                document.getElementById(this.nodos[ro].name + this.nodos[ro].idConfig).click();
              }
              
            }
          }
          
        },
      },
      created() {
          this.$eventHub.$on('removeTabTotal', (tab) => {
              //this.tabsActivos.splice(tab,1);
              this.removeTab(tab);
          });
      },  
       
  }
</script>