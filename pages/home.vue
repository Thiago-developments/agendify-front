<template>
  <v-container>
    <v-card>
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
        dense
        hide-default-footer
      >
        <template v-slot:[`item.actions`]="{ item }">
          <v-btn icon color="blue" @click="editItem(item)">
            <v-icon>mdi-pencil</v-icon>
          </v-btn>
          <v-btn icon color="red" @click="deleteItem(item)">
            <v-icon>mdi-delete</v-icon>
          </v-btn>
        </template>
      </v-data-table>
    </v-card>
  </v-container>
</template>

<script>
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
        { tabName: "Agendamento de transferências" },
        {
          tabName: "Extrato",
        },
      ],
      tab: null,
    };
  },

  methods: {
    editItem(item) {
      alert(`Editando ${item.name}`);
    },
    deleteItem(item) {
      alert(`Excluindo ${item.name}`);
    },
  },
};
</script>

<style></style>
