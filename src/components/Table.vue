<template>
  <div>
    <v-data-table
      :headers="headers"
      :items="pads"
      :options.sync="options"
      :server-items-length="totalPads"
      :loading="loading"
      :itemsPerPage=5
      :footer-props="{ itemsPerPageOptions: [5, 10, 15, 20, totalPads]}"
      class="elevation-1"
    >
    </v-data-table>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      config: {
        headers: {
          Authorization: `Bearer ${process.env.VUE_APP_TOKEN}`,
        },
      },
      pads: [],
      totalPads: 0,
      loading: true,
      options: {},
      headers: [
        {
          text: 'Solicitante',
          align: 'start',
          sortable: false,
          value: 'request',
        },
        { text: 'Profissional', value: 'professional' },
        { text: 'Superior Imediato', value: 'immediateSuperior' },
        { text: 'Data da solicitação', value: 'requestDate' },
        { text: 'Prazo de aprovação/rejeição', value: 'rejectionApprovalDeadline' },
      ],
    };
  },
  watch: {
    options: {
      async handler() {
        this.getDataFromApi();
      },
      deep: true,
    },
  },

  methods: {
    getDataFromApi() {
      const {
        itemsPerPage, page, sortBy, sortDesc,
      } = this.options;
      console.log(this.options);
      console.log(process.env.VUE_APP_TOKEN);

      axios
        .get(`http://127.0.0.1:3333/v1/process/status/?questionarioId=1&page=${page}&limit=${itemsPerPage}`, this.config)
        .then((response) => {
          this.loading = true;
          const { data } = response.data;
          console.log(data);
          const dataSerialized = data.data.map((el) => this.serialize(el));
          this.data = dataSerialized;

          this.pads = dataSerialized;
          this.totalPads = Number(data.total);
          this.loading = false;

          if (sortBy.length === 1 && sortDesc.length === 1) {
            this.pads = this.pads.sort((a, b) => {
              const sortA = a[sortBy[0]];
              const sortB = b[sortBy[0]];

              if (sortDesc[0]) {
                if (sortA < sortB) return 1;
                if (sortA > sortB) return -1;
                return 0;
              }
              if (sortA < sortB) return -1;
              if (sortA > sortB) return 1;
              return 0;
            });
          }

          // if (itemsPerPage > 0) {
          //   this.pads = this.pads.slice((page - 1) * itemsPerPage, page * itemsPerPage);
          // }
        });
    },
    serialize(data) {
      return {
        request: data.avaliado.email,
        professional: data.avaliadorSolicitante.email,
        immediateSuperior: data.avaliado.email,
        requestDate: data.created_at,
        rejectionApprovalDeadline: data.aprovacao_rejeicao,
      };
    },
  },
};
</script>
