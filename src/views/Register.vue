<template>
  <div class="ma-0 pa-0">
    <v-card
      class="mx-auto"
      width="300"
    >
      <v-list>
        <v-list-item>
          <v-list-item-icon>
            <v-icon>mdi-home</v-icon>
          </v-list-item-icon>

          <v-list-item-title>Home</v-list-item-title>
        </v-list-item>

        <!-- start -->
        <v-list-group
          :value="false"
          prepend-icon="mdi-account-circle"
        >
          <template v-slot:activator>
            <v-list-item-title>Users</v-list-item-title>
          </template>

          <v-list-item
            v-for="([title, icon], i) in admins"
            :key="i"
            link
          >
            <v-list-item-icon>
              <v-icon v-text="icon"></v-icon>
            </v-list-item-icon>
            <v-list-item-title v-text="title"></v-list-item-title>
          </v-list-item>
        </v-list-group>
        <!-- start -->

      </v-list>
    </v-card>
  </div>

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
      admins: [
        ['Management', 'mdi-account-multiple-outline'],
        ['Settings', 'mdi-cog-outline'],
      ],
    };
  },
};
</script>

<style scoped>
.border {
  border: 2px dashed orange;
}

.v-list-item--link {
  /* display: flex; */
  /* justify-content: center !important; */
  padding-left: 70px;
}

/* .c_card {
  max-width: 400px !important;
} */
</style>
