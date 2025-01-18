<template>
  <div>
    <v-dialog v-model="dialog" max-width="700px">
      <v-card>
        <v-card-title>
          <span class="text-h6">Agendamento de transferências</span>
        </v-card-title>

        <v-card-text>
          <v-form ref="form">
            <v-container>
              <v-row dense>
                <v-col cols="12" md="6">
                  <v-text-field
                    label="Conta de origem"
                    v-model="formData.contaOrigem"
                    outlined
                    dense
                    required
                  ></v-text-field>
                </v-col>

                <v-col cols="12" md="6">
                  <v-text-field
                    label="Conta de destino"
                    v-model="formData.contaDestino"
                    outlined
                    dense
                    required
                  ></v-text-field>
                </v-col>

                <v-col cols="12" md="6">
                  <v-text-field
                    label="Valor"
                    v-model="formData.valor"
                    outlined
                    dense
                    type="number"
                    required
                  ></v-text-field>
                </v-col>

                <v-col cols="12" md="6">
                  <v-menu
                    v-if="agendamento"
                    v-model="menu"
                    :close-on-content-click="false"
                    transition="scale-transition"
                    offset-y
                    min-width="auto"
                  >
                    <template v-slot:activator="{ on, attrs }">
                      <v-text-field
                        v-model="formData.agendamento"
                        label="Agendamento"
                        readonly
                        v-bind="attrs"
                        v-on="on"
                        outlined
                        dense
                      ></v-text-field>
                    </template>
                    <v-date-picker
                      v-model="formData.agendamento"
                      no-title
                      @input="menu = false"
                    ></v-date-picker>
                  </v-menu>
                </v-col>
              </v-row>
            </v-container>
          </v-form>
        </v-card-text>

        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn text color="red" @click="cancelar">Cancelar</v-btn>
          <v-btn text color="green" @click="agendar">Agendar</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
</template>

<script>
export default {
  props: {
    agendamento: {
      type: Boolean,
      default: false,
    },
  },

  data() {
    return {
      dialog: true,
      menu: false,
      formData: {
        contaOrigem: "",
        contaDestino: "",
        valor: "",
        agendamento: null,
      },
    };
  },
  methods: {
    cancelar() {
      this.$emit("close");
    },

    agendar() {
      console.log("batendo na request");
      this.$emit("agendar");
    },
  },
};
</script>
