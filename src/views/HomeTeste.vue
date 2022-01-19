<template>
  <TableTeste
    :headers="headers"
    :items="pads"
    :options="options"
    :itemsLength="totalPads"
    :loading="loading"
  />
</template>

<script>
import axios from 'axios';
import TableTeste from '../components/TableTeste.vue';

export default {
  name: 'HomeTeste',

  components: {
    TableTeste,
  },
  data() {
    return {
      config: {
        headers: {
          Authorization: 'Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1aWQiOjY2MywiZGF0YSI6eyJleHBpcmVzSW4iOiIxMmgiLCJleHAiOjE2NDI2MTUzMjcsImFkIjp7ImlzcyI6Imh0dHA6Ly8xMC4yMC4wLjIzNC9sb2dpbiIsImlhdCI6MTY0MjU5MzcyNywiZXhwIjoxNjQyNjA0NTI3LCJuYmYiOjE2NDI1OTM3MjcsImp0aSI6IlRWd1RrblhwUjEzbVZTSU4iLCJzdWIiOm51bGwsInBydiI6Ijg3ZTBhZjFlZjlmZDE1ODEyZmRlYzk3MTUzYTE0ZTBiMDQ3NTQ2YWEifSwicm9sZSI6ImRldmh1bWFucyJ9LCJpYXQiOjE2NDI1OTM3MjcsImV4cCI6MTY0MjYzNjkyN30.QNyEI9gnY_aD2F-uJQfgxYfx5O0YiZmVX6OhyK0XV8g',
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
      handler() {
        this.getDataFromApi();
        this.$emit('update:options', this.options);
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
