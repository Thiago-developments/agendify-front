<template>
  <v-container>
    <v-card style="min-height: 70vh">
      <v-tabs v-model="tab" bg-color="red-lighten-2">
        <v-tab v-for="(tab, index) in tabList" :key="index" :value="index">
          {{ tab.tabName }}</v-tab
        >
      </v-tabs>
      <v-data-table
        v-if="tab == 0"
        :headers="headers"
        :items="users"
        class="elevation-1"
        item-value="name"
      >
        <template v-slot:[`item.actions`]="{ item }">
          <v-btn icon color="blue" @click="editar(item)">
            <v-icon>mdi-pencil</v-icon>
          </v-btn>
        </template>
      </v-data-table>

      <v-row justify="end">
        <v-col cols="auto">
          <v-btn text color="blue" @click="transferir">Transferir</v-btn>
          <v-btn text color="green" @click="agendar">Agendar</v-btn>
        </v-col>
      </v-row>

      <modal-agendamento
        v-if="modalAgendamento"
        :agendamento="flagAgendamento"
        @close="handleModalAgendamento"
        @agendar="handleModalAgendamento"
      />
    </v-card>
  </v-container>
</template>

<script>
import { isEmpty } from "lodash";
export default {
  name: "HomePage",

  data() {
    return {
      headers: [
        { text: "Conta de origem", value: "originAccount" },
        { text: "Conta de destino", value: "destinyAccount" },
        { text: "Valor", value: "money" },
        { text: "Realizado", value: "date" },
        { text: "Agendamento", value: "scheduling", sortable: false },
        { text: "Ações", value: "actions", sortable: false },
      ],

      users: [
        {
          originAccount: "João Pereira",
          destinyAccount: "Thiago Sousa",
          money: 354.04,
          date: "15/01/2025",
          scheduling: "15/01/2025",
        },
      ],

      tabList: [
        { tabName: "Agendamentos" },
        {
          tabName: "Extrato",
        },
      ],

      tab: null,
      modalAgendamento: false,
      flagAgendamento: false,
    };
  },

  methods: {
    editar(item) {
      this.flagAgendamento = !isEmpty(item.scheduling);
      this.handleModalAgendamento();
    },

    transferir() {
      this.flagAgendamento = false;
      this.handleModalAgendamento();
    },

    agendar() {
      this.flagAgendamento = true;
      this.handleModalAgendamento();
    },

    handleModalAgendamento() {
      this.modalAgendamento = !this.modalAgendamento;
    },
  },
};
</script>

<style></style>
