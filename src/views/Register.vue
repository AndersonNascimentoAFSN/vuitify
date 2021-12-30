<template>
  <v-navigation-drawer
    permanent
    expand-on-hover
  >
    <v-list
      nav
      dense
      id="container-items-sidebar"
    >
      <v-list-item-group
        v-model="model"
        active-class="active-item"
        mandatory
        color="#0056A8"
      >

        <v-list-item link>
          <v-list-item-icon>
            <v-icon>mdi-home</v-icon>
          </v-list-item-icon>
          <v-list-item-title>Home</v-list-item-title>
        </v-list-item>

        <v-list-item link>
          <v-list-item-icon>
            <v-icon>mdi-head-question</v-icon>
          </v-list-item-icon>
          <v-list-item-title>FAQ</v-list-item-title>
        </v-list-item>

        <!-- start -->
        <v-list-group
          :value="false"
          prepend-icon="mdi-forum-outline"
          active-class="active-sub-item"
          color="#0056A8"
          link
        >
          <template v-slot:activator>
            <v-list-item-title>PAD</v-list-item-title>
          </template>

          <v-list-item
            v-for="([title, icon], i) in pad"
            :key="i"
            link
            id="container-pad"
          >
            <v-list-item-icon>
              <v-icon v-text="icon"></v-icon>
            </v-list-item-icon>
            <v-list-item-title v-text="title"></v-list-item-title>
          </v-list-item>
        </v-list-group>
        <!-- end -->

        <!-- start -->
        <v-list-group
          :value="false"
          prepend-icon="mdi-account-sync"
          link
        >
          <template v-slot:activator>
            <v-list-item-title>Turnover</v-list-item-title>
          </template>

          <v-list-item
            v-for="([title, icon], i) in turnover"
            :key="i"
            link
          >
            <v-list-item-icon>
              <v-icon v-text="icon"></v-icon>
            </v-list-item-icon>
            <v-list-item-title v-text="title"></v-list-item-title>
          </v-list-item>
        </v-list-group>
        <!-- end -->

        <!-- start -->
        <v-list-group
          :value="false"
          prepend-icon="mdi-strategy"
          link
        >
          <template v-slot:activator>
            <v-list-item-title>Acomp. Estratégico</v-list-item-title>
          </template>

          <v-list-item
            v-for="([title, icon], i) in strategicMonitoring"
            :key="i"
            link
          >
            <v-list-item-icon>
              <v-icon v-text="icon"></v-icon>
            </v-list-item-icon>
            <v-list-item-title v-text="title"></v-list-item-title>
          </v-list-item>
        </v-list-group>
        <!-- end -->

        <v-list-item>
          <v-list-item-icon link>
            <v-icon>mdi-lock</v-icon>
          </v-list-item-icon>
          <v-list-item-title>Permissões</v-list-item-title>
        </v-list-item>

        <v-list-item>
          <v-list-item-icon link>
            <v-icon>mdi-account-group</v-icon>
          </v-list-item-icon>
          <v-list-item-title>Profissionais</v-list-item-title>
        </v-list-item>

      </v-list-item-group>
    </v-list>

  </v-navigation-drawer>
</template>

<script>
export default {
  name: 'Register',

  data() {
    return {
      items: {

      },
      pad: [
        ['Novo PAD', 'mdi-plus-thick'],
        ['Painel', 'mdi-view-dashboard'],
        ['Indicadores', 'mdi-equalizer'],
        ['Visão Time', 'mdi-account-multiple'],
      ],
      turnover: [
        ['Painel', 'mdi-view-dashboard'],
        ['Indicadores', 'mdi-equalizer'],
      ],
      strategicMonitoring: [
        ['Painel', 'mdi-view-dashboard'],
        ['Indicadores', 'mdi-equalizer'],
      ],
    };
  },
};
</script>

<style scoped>
/* .border {
  border: 2px dashed orange;
} */

#container-pad {
  background: #f5f5f5;
  margin: 0;
}

#container-items-sidebar {
}

.active-item {
  color: #0056a8;
}

.active-sub-item {
  color: #dddddd;
}

.v-list-group__items {
  background: #f5f5f5;
}

.v-list-group__items {
  padding-left: 70px;
}
</style>
