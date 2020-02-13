<template>
  <v-app id="inspire">
    <v-navigation-drawer v-model="drawer" :clipped="$vuetify.breakpoint.lgAndUp" app>
      <menuDrawel></menuDrawel>
    </v-navigation-drawer>
    
    <v-app-bar :clipped-left="$vuetify.breakpoint.lgAndUp" app style="border_top:15px;" >
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      <div class="d-flex align-center">
        <!-- <v-img alt="Vuetify Logo" class="shrink mr-2" contain src="https://cdn.vuetifyjs.com/images/logos/vuetify-logo-dark.png" transition="scale-transition" width="40"/>
        <v-img alt="Vuetify Name" class="shrink mt-1 hidden-sm-and-down" contain min-width="100" src="https://cdn.vuetifyjs.com/images/logos/vuetify-name-dark.png" width="100"/> -->
        <v-img alt="TotalPlay" class="shrink mr-2" contain min-width="50%" src="https://www.totalplay.com.mx/images/logos/total_play_logo.png" transition="scale-transition" width="50%"/>
      </div>
      <v-spacer />
      <!-- <v-text-field flat solo-inverted hide-details prepend-inner-icon="mdi-magnify" label="Search" class="hidden-sm-and-down"/>
      
      <v-btn icon>
        <v-icon>mdi-apps</v-icon>
      </v-btn> -->
      
      <v-btn icon color="indigo" class="border-right">
        <v-badge color="error" overlap>
          <template slot="badge">
            5
          </template>
          <v-icon color="tertiary">mdi-bell</v-icon>
        </v-badge>
      </v-btn>
      
      <v-menu offset-y>
        <template v-slot:activator="{ on }">
          <v-btn x-large class="ma-2" elevation="0" v-on="on">
            <v-avatar size="40px" class="mx-1">
                <img src="//ssl.gstatic.com/s2/oz/images/sge/grey_silhouette.png" alt="">
              </v-avatar>
            <span class="hidden-sm-and-down" style="color:#1976d2;">Usuario</span>
          </v-btn>
        </template>

        <v-list >
          <v-list-item
            v-for="n in 5" :key="n" @click="() => {}">
            <v-list-item-title>Option {{ n }}</v-list-item-title>
          </v-list-item>
        </v-list>
      </v-menu>
    </v-app-bar>
    <v-content>
      <v-container fluid>
        <tabsTotal></tabsTotal>
      </v-container>
    </v-content>
    <v-btn bottom color="blue" dark fab fixed right @click="dialog = !dialog">
      <v-icon>mdi-plus</v-icon>
    </v-btn>
    <v-dialog v-model="dialog" width="800px">
      <v-card>
        <v-card-title class="grey darken-2">
          Create contact
        </v-card-title>
        <v-container>
          <v-row class="mx-2">
            <v-col class="align-center justify-space-between" cols="12">
              <v-row align="center" class="mr-0">
                <v-avatar
                  size="40px"
                  class="mx-3"
                >
                  <img
                    src="//ssl.gstatic.com/s2/oz/images/sge/grey_silhouette.png"
                    alt=""
                  >
                </v-avatar>
                <v-text-field
                  placeholder="Name"
                />
              </v-row>
            </v-col>
            <v-col cols="6">
              <v-text-field
                prepend-icon="mdi-account-card-details-outline"
                placeholder="Company"
              />
            </v-col>
            <v-col cols="6">
              <v-text-field
                placeholder="Job title"
              />
            </v-col>
            <v-col cols="12">
              <v-text-field
                prepend-icon="mdi-mail"
                placeholder="Email"
              />
            </v-col>
            <v-col cols="12">
              <v-text-field
                type="tel"
                prepend-icon="mdi-phone"
                placeholder="(000) 000 - 0000"
              />
            </v-col>
            <v-col cols="12">
              <v-text-field
                prepend-icon="mdi-text"
                placeholder="Notes"
              />
            </v-col>
          </v-row>
        </v-container>
        <v-card-actions>
          <v-btn
            text
            color="primary"
          >More</v-btn>
          <v-spacer />
          <v-btn
            text
            color="primary"
            @click="dialog = false"
          >Cancel</v-btn>
          <v-btn
            text
            @click="dialog = false"
          >Save</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-app>
</template>

<script>
  import menuDrawel from '@/components/MenuDrawel.vue';
  import tabsTotal from '@/components/TabsTotal.vue';

  export default {
    components:{
      menuDrawel,
      tabsTotal,
    },
    props: {
      source: String,
    },
    data: () => ({
      dialog: false,
      drawer: null,
      notifications: [
      'Mike, John responded to your email',
      'You have 5 new tasks',
      'You\'re now a friend with Andrew',
      'Another Notification',
      'Another One'
    ],
      itemslog: ['Foo', 'Bar', 'Fizz', 'Buzz'],
      items2: [
          {
            action: 'local_activity',
            title: 'Attractions',
            items: [
              { title: 'List Item' },
            ],
          },
          {
            action: 'restaurant',
            title: 'Dining',
            active: true,
            items: [
              { title: 'Breakfast & brunch' },
              { title: 'New American' },
              { title: 'Sushi' },
            ],
          },
          {
            action: 'school',
            title: 'Education',
            items: [
              { title: 'List Item' },
            ],
          },
          {
            action: 'directions_run',
            title: 'Family',
            items: [
              { title: 'List Item' },
            ],
          },
          {
            action: 'healing',
            title: 'Health',
            items: [
              { title: 'List Item' },
            ],
          },
          {
            action: 'content_cut',
            title: 'Office',
            items: [
              { title: 'List Item' },
            ],
          },
          {
            action: 'local_offer',
            title: 'Promotions',
            items: [
              { title: 'List Item' },
            ],
          },
        ],
    }),
  }
</script>