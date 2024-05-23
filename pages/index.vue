<template>
  <template>
    <v-app>
      <v-container>
        <TabelaComponent
          title="Filmes"
          icon="mdi-movie-filter"
          :items="items"
          :headers="headers"
          @abrirDialog="() => ativo = true"
          @taLigado="taLigado"
          @deleteItem="deleteItem"
        />
        <v-dialog
          v-model="ativo"
          max-width="500"
        >
          <v-card
          height="320"
          width="400"
          theme="dark">
            <v-card-title>
              Criar um novo item
            </v-card-title>
            <v-card-text>
              <v-row>
                <v-col>
                  <v-text-field
                  variant="outlined"
                  label="Nome"
                  placeholder="nome"
                  v-model="filmes.nome">
                  </v-text-field>
                </v-col>
                <v-col>
                  <v-text-field
                  variant="outlined"
                  label="Descrição"
                  placeholder="descricao"
                  v-model="filmes.descricao">
                  </v-text-field>
                </v-col>
              </v-row>
              <v-row>
                <v-col>
                  <v-text-field
                  variant="outlined"
                  label="Autor"
                  placeholder="autor"
                  v-model="filmes.autor">
                  </v-text-field>
                </v-col>
                <v-col>
                  <v-text-field
                  variant="outlined"
                  label="Duração minutos"
                  placeholder="duracaoMin"
                  v-model="filmes.duracaoMin">
                  </v-text-field>
                </v-col>
              </v-row>
            </v-card-text>
            <v-card-actions>
              <v-btn 
                variant="outlined" 
                class="text-none"
                @click="createItem()">
                  Criar
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
        <v-dialog
          v-model="ativo2"
          max-width="500"
        >
          <v-card
          height="320"
          width="400"
          theme="dark">
            <v-card-title>
              Editar item
            </v-card-title>
            <v-card-text>
              <v-row>
                <v-col>
                  <v-text-field
                  variant="outlined"
                  label="Nome"
                  placeholder="nome"
                  v-model="filmes.nome">
                  </v-text-field>
                </v-col>
                <v-col>
                  <v-text-field
                  variant="outlined"
                  label="Descrição"
                  placeholder="descricao"
                  v-model="filmes.descricao">
                  </v-text-field>
                </v-col>
              </v-row>
              <v-row>
                <v-col>
                  <v-text-field
                  variant="outlined"
                  label="Autor"
                  placeholder="autor"
                  v-model="filmes.autor">
                  </v-text-field>
                </v-col>
                <v-col>
                  <v-text-field
                  variant="outlined"
                  label="Duração minutos"
                  placeholder="duracaoMin"
                  v-model="filmes.duracaoMin">
                  </v-text-field>
                </v-col>
              </v-row>
            </v-card-text>
            <v-card-actions>
              <v-btn 
                variant="outlined" 
                class="text-none"
                @click="editItem()">
                  Editar
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </v-container>
    </v-app>
    <v-btn 
    @click="mudaPaginaSla()"
    theme="dark">
      Sla
    </v-btn>
  </template>
</template>

<script>

export default { 
  data: () => {
    return {
      ativo: false,
      ativo2: false,
      search: '',
      page: 1,
      itemsPerPage: 5,
      filmes: {
        nome: null,
        descricao: null,
        autor: null,
        duracaoMin: null
      },
      headers: [
        {
          title: 'Id',
          key: 'id',
        },
        {
          title: 'Nome',
          key: 'nome',
        },
        {
          title: 'Descrição',
          key: 'descricao',
        },  
        {
          title: 'Autor',
          key: 'autor',
        },
        {
          title: 'Duração/min',
          key: 'duracaoMin',
        },
        {
          title: 'Ações',
          key: 'actions',
          sortable: false
        }
      ],
      items: [],
    }
  },

  async created() {
    await this.getItems();
  },

  watch: {
    ativo(valor) {
      if (valor == false) {
        this.resetFilmes()
      }
    },
    ativo2(valor) {
      if (valor == false) {
        this.resetFilmes()
      }
    }
  },

  methods: {
    resetFilmes(){
      this.filmes = {
        nome: null,
        descricao: null,
        autor: null,
        duracaoMin: null
      }
      this.ativo = false;
      this.ativo2 = false;
    },

    async createItem() {
      const response = await this.$api.post('/filmes/persist', this.filmes);
      this.resetFilmes();
      await this.getItems();
    },

    taLigado(item) {
      this.filmes = {
        ...item
      }
      this.ativo2 = true;
    },

    async editItem() {
      const response = await this.$api.post(`/filmes/persist/${this.filmes.id}`, this.filmes);
      this.resetFilmes()
      await this.getItems();
    },
    
    mudaPagina(){
      this.$router.push({ path: '/variaveis' });
    },
    mudaPaginaSla(){
      this.$router.push({ path: '/sla' });
    },
    
    async getItems() {
      const response = await this.$api.get('/filmes');
      this.items = response.data;
    },
    
    async deleteItem(item) {
      if (confirm(`Você deseja mesmo deletar o item com id ${item.id}`)) {
        const response = await this.$api.post('/filmes/destroy', { id: item.id });
        if (response.type == 'error') {
          alert(response.message);
        }
      }
      await this.getItems()
    }  
  },
}
  

</script>
