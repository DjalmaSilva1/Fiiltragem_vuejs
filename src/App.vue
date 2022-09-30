<template>
  <div id="app" class="container mt-3">
    <!-- filtro -->
    <b-form inline>
      <b-form-input
        id="inline-form-input-name"
        class="mb-2 mr-sm-2 mb-sm-0"
        placeholder="Nome ou E-mail"
        v-model="search"
      ></b-form-input>

      <b-form-select
        class="mb-2 mr-sm-2 mb-sm-0"
        v-model="selected"
        :options="options"
      ></b-form-select>

      <b-button title="Limpar filtro" v-b-tooltip.hover @click="clearFilter"
        ><b-icon-trash class="icon"></b-icon-trash
      ></b-button>
    </b-form>

    <b-row>
      <b-col md="6" sm="12">
        <!-- tabela -->
        <b-table
          class="mt-3"
          striped
          hover
          :items="filteredItems"
          :fields="fields"
        >
          <template #cell(isActive)="data">
            <template v-if="data.item.isActive">Ativo</template>
            <template v-else>Inativo</template>
          </template>
        </b-table>
      </b-col>
      <b-col md="6" sm="12">
        <!-- lista -->
        <ul class="mt-3">
          <li v-for="(item, key) in filteredItems" :key="key">
            {{ item.name }} - {{ item.email }}
          </li>
        </ul>
      </b-col>
    </b-row>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      fields: [
        {
          key: "name",
          label: "Nome",
        },
        {
          key: "email",
          label: "E-mail",
        },
        {
          key: "isActive",
          label: "Status",
        },
      ],
      items: [
        {
          isActive: true,
          name: "Letícia Araujo Pereira",
          email: "LeticiaAraujoPereira@dayrep.com",
        },
        {
          isActive: false,
          name: "Marina Santos Araujo",
          email: "MarinaSantosAraujo@dayrep.com",
        },
        {
          isActive: false,
          name: "Felipe Lima Fernandes",
          email: "FelipeLimaFernandes@dayrep.com",
        },
        {
          isActive: true,
          name: "Thaís Lima Castro",
          email: "ThaisLimaCastro@rhyta.com",
        },
        {
          isActive: true,
          name: "Renan Melo Barros",
          email: "RenanMeloBarros@teleworm.us",
        },
        {
          isActive: true,
          name: "Matilde Pereira Carvalho",
          email: "MatildePereiraCarvalho@rhyta.com",
        },
        {
          isActive: true,
          name: "Gabriel Ferreira Gomes",
          email: "GabrielFerreiraGomes@jourrapide.com",
        },
      ],
      search: "",
      selected: null,
      options: [
        { value: null, text: "Selecione um status" },
        { value: true, text: "Ativo" },
        { value: false, text: "Inativo" },
      ],
    };
  },

  computed: {
    filteredItems() {
      let items = [];
      items = this.items.filter((item) => {
        return (
          item.name.toLowerCase().indexOf(this.search.toLowerCase()) > -1 ||
          item.email.toLowerCase().indexOf(this.search.toLowerCase()) > -1
        );
      });

      items = items.filter((item) => {
        if (this.selected == null) return item;
        return item.isActive === this.selected;
      });

      return items;
    },
  },

  methods: {
    clearFilter() {
      this.search = "";
      this.selected = null;
    },
  },
};
</script>
