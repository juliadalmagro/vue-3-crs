<template>
  <v-data-table
    :headers="headers"
    :items="items"
    theme="dark"
    height="300"
    item-value="name"
    @deleteItem="deleteItem"
    :items-per-page="itemsPerPage"
    :page.sync="page"
    :search="search"
  >
    <template v-slot:top>
      <v-toolbar flat>
        <v-toolbar-title>
          {{ title }}
          <v-icon> {{ icon }} </v-icon>
        </v-toolbar-title>
        <v-btn class="mb-2" color="primary" dark @click="abrirDialog">
          Novo Item
          <v-icon> mdi-flower-tulip </v-icon>
        </v-btn>
      </v-toolbar>
      <v-text-field
        v-model="search"
        label="Search"
        prepend-inner-icon="mdi-magnify"
        variant="outlined"
        hide-details
        single-line
      ></v-text-field>
    </template>
    <template v-slot:no-data>
      <span>
        Dados não encontrados
        <v-btn>
          <v-icon> mdi-reload </v-icon>
        </v-btn>
      </span>
    </template>

    <template v-slot:item.actions="{ item }">
      <v-icon class="me-2" size="small" @click="taLigado(item)">
        mdi-pencil
      </v-icon>
      <v-icon class="me-2" size="small" @click="deleteItem(item)">
        mdi-delete
      </v-icon>
    </template>

    <template v-slot:bottom>
      <div class="text-center">
        <v-pagination
          v-model="page"
          :length="pageCount"
          next-icon="mdi-menu-right"
          prev-icon="mdi-menu-left"
        ></v-pagination>
      </div>
    </template>
  </v-data-table>
</template>

<script>
export default {
  name: 'TabelaComponent',
  data () {
    return {
      search: '',
      itemsPerPage: 5,
      page: 1,
    }
  },
  props: {
    headers: {
      type: Array
    },
    items: {
      type: Array,
      default: []
    },
    title: {
      type: String,
    },
    icon: {
      type: String
    }
  },

  computed: {
      totalItems() {
        return this.items.length
      },
      pageCount() {
        return Math.ceil(this.totalItems / this.itemsPerPage)
      },
  },

  methods: {
    abrirDialog() {
      this.$emit('abrirDialog')
    },
    taLigado(item) {
      this.$emit('taLigado', item)
    },
    deleteItem(item) {
      this.$emit('deleteItem', item)
    }
  }
}
</script>
