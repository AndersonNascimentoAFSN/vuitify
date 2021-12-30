<template>
  <!-- <v-container> -->
  <div class="ma-0 pa-0">
    <!-- <v-card> -->
    <v-navigation-drawer
      permanent
      expand-on-hover
    >
      <v-list
        nav
        dense
      >
        <v-list-item-group
          v-model="model"
          active-class="border"
          mandatory
          color="indigo"
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

          <v-list-item>
            <v-list-item-icon link>
              <v-icon>mdi-forum-outline</v-icon>
            </v-list-item-icon>
            <v-list-item-title>PAD</v-list-item-title>
          </v-list-item>

          <v-list-item>
            <v-list-item-icon link>
              <v-icon>mdi-account-sync</v-icon>
            </v-list-item-icon>
            <v-list-item-title>TurnOver</v-list-item-title>
          </v-list-item>

          <v-list-item>
            <v-list-item-icon link>
              <v-icon>mdi-strategy</v-icon>
            </v-list-item-icon>
            <v-list-item-title>Acomp. Estratégico</v-list-item-title>
          </v-list-item>

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
    <!-- </v-card> -->
  </div>

  <!-- </v-container> -->

  <!-- <v-col cols="4">
      <v-car
        class="mx-auto"
        min-width="400"
      >
        <v-list>
          <v-list-item-group
            v-model="model"
            active-class="border"
            mandatory
            color="indigo"
          >
            <v-list-item
              v-for="(item, i) in items"
              v-bind:key="i"
            >

              <v-list-item-content>
                <v-list-item-title v-text="item.text"></v-list-item-title>
              </v-list-item-content>

              <v-list-item-icon>
                <v-icon v-text="item.icon"></v-icon>
              </v-list-item-icon>

            </v-list-item>
          </v-list-item-group>
        </v-list>
      </v-car>
    </v-col> -->
</template>

<script>
export default {
  name: 'Register',

  data() {
    return {
      items: [
        {
          icon: 'mdi-wifi',
          text: 'Wifi',
        },
        {
          icon: 'mdi-bluetooth',
          text: 'Bluetooth',
        },
        {
          icon: 'mdi-chart-donut',
          text: 'Data Usage',
        },
      ],
      model: 1,
    };
  },
};
</script>

<style scoped>
.border {
  border: 2px dashed orange;
}

/* .c_card {
  max-width: 400px !important;
} */
</style>
