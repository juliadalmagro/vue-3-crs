<template>
  <v-container>
    <v-row 
    v-if="items.length > 0"
    justify="center">
      <v-col
        v-for="(dado, i) in items"
        :key="i"
        cols="12"
        md="5"
      >
        <v-card
          :color="color"
          :variant="variant"
          class="mx-auto"
          theme="dark"
          height="200"
          width="400"
          
        >
          
          <v-card-item>
            <div>
              <div class="text-h6 mb-1">
                <v-card-title
                  class="text-center">
                  Filme: {{dado.nome}}
                </v-card-title>
              </div>
              <!-- <div>
                <v-card-text>
                  Autor: {{ dado.autor }}
                </v-card-text>
              </div> -->
              <div>
                <v-card-text>
                  Descrição: {{ dado.descricao }}
                </v-card-text>
              </div>
              <div>
                <v-card-text>
                  Duração em minutos: {{ dado.duracaoMin }}
                </v-card-text>
              </div>
            </div>
          </v-card-item>

        </v-card>
      </v-col>
    </v-row>
    <h1 v-else> Sem items </h1>
  </v-container>
</template>

<script>

export default {
  data() {
    return {
      items: [],
    }
  },
  async created() {
    await this.getItems();
  },

  methods: {
    async getItems() {
      const response = await this.$api.get('/filmes');
      this.items = response.data; 
      this.ativo = true;
    },
  },

};

</script>
