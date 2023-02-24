<template>
  <v-data-table :headers="headers" :items="courseProgrammChildrens"  :search="search" class="elevation-1" fixed-header height="350px">
    <template v-slot:top>
      <div class="box"><v-text-field v-model="search" append-icon="mdi-magnify" label="Поиск" dense outlined single-line hide-details></v-text-field></div>
      <v-toolbar flat color="white">
        <v-toolbar-title>Образование</v-toolbar-title>
        <v-divider class="mx-4" inset vertical></v-divider>
        <v-spacer></v-spacer>
        <v-dialog v-model="dialog" max-width="500px">
          <template v-slot:activator="{ on, attrs }">
            <v-btn color="primary" dark class="mb-2" v-bind="attrs" v-on="on">Добавить</v-btn>
          </template>
          <v-card>
            <v-card-title>
              <span class="headline">{{ formTitle }}</span>
            </v-card-title>
<v-card-text>
              <v-container>
                <v-row>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field v-model="editedItem.Code" label="Code"></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field v-model="editedItem.Name" label="Name"></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field v-model="editedItem.Year" label="Year"></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field v-model="editedItem.EduForm" label="EduForm"></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field v-model="editedItem.EduLevel" label="EduLevel"></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field v-model="editedItem.ParentProgramm" label="ParentProgramm"></v-text-field>
                  </v-col>
                </v-row>
              </v-container>
            </v-card-text>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="blue darken-1" text @click="close">Выход</v-btn>
              <v-btn color="blue darken-1" text @click="save">Сохранить</v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </v-toolbar>
    </template>
    <template v-slot:[`item.actions`]="{ item }">
      <v-icon small class="mr-2" @click="editItem(item)">mdi-pencil</v-icon>
      <v-icon small @click="deleteItem(item)">mdi-delete</v-icon>
    </template>
    <template v-slot:no-data>
      <v-btn color="primary" @click="initialize">Инициализация</v-btn>
    </template>
    <div id="app">
  <v-app id="inspire">
    <v-treeview
      activatable
      :items="items"
    ></v-treeview>
  </v-app>
</div>
  </v-data-table>
</template>
<script>
export default {
  name: "HelloWorld",
  data: () => ({
    search: '',
    dialog: false,
    headers: [
      
      // { text: 'id', value: 'id' },
      { text: 'Code', value: 'Code' },
      { text: 'Name', value: 'Name' },
      { text: 'Year', value: 'Year' },
      { text: 'EduForm', value: 'EduForm' },
      { text: 'EduLevel', value: 'EduLevel' },
      { text: 'ParentProgramm', value: 'ParentProgramm' },
      { text: 'Действия', value: 'actions', sortable: false , width: "100px"},
    ],

  courseProgrammChildrens: [],
    editedIndex: -1,
    editedItem: {
      id: 0,
      Code: '',
      Name: '',
      Year: 0,
      EduForm: 0,
      EduLevel: 0,
      ParentProgramm: 0},

    defaultItem: {
      id: 0,
      Code: 'Новый код',
      Name: 'Текст',
      Year: 0,
      EduForm: 0,
      EduLevel: 0,
      ParentProgramm: 0 } }),

  computed: {
    formTitle() {
      return this.editedIndex === -1 ? "Новый элемент" : "Редактор элемента";
    },
  },
  watch: {
    dialog(val) {
      val || this.close();
    },
  },
  created() {
    this.initialize();
  },
  methods: {
    initialize() {
      this.courseProgrammChildrens = [
      {
      id: 1,
      Code: "ed1",
      Name: "Текст 1",
      Year: 2023,
      EduForm: 3,
      EduLevel: 1,
      ParentProgramm: 2 },

      {
        id: 2,
        Code: "ed2",
        Name: "Текст 2",
        Year: 2023,
        EduForm: 2,
        EduLevel: 1,
        ParentProgramm: 2},

      {
      id: 3,
      Code: "ed3",
      Name: "Текст 3",
      Year: 2023,
      EduForm: 4,
      EduLevel: 1,
      ParentProgramm: 1 },

      {
      id: 4,
      Code: "ed4",
      Name: "Текст 4",
      Year: 2023,
      EduForm: 5,
      EduLevel: 5,
      ParentProgramm: 5},];
    },
    editItem(item) {
      this.editedIndex = this.courseProgrammChildrens.indexOf(item);
      this.editedItem = Object.assign({}, item);
      this.dialog = true;
    },
    deleteItem(item) {
      const index = this.courseProgrammChildrens.indexOf(item);
      confirm("Вы уверены, что хотите удалить этот элемент?") &&
        this.courseProgrammChildrens.splice(index, 1);
    },
    close() {
      this.dialog = false;
      this.$nextTick(() => {
        this.editedItem = Object.assign({}, this.defaultItem);
        this.editedIndex = -1;
      });
    },
    save() {
      if (this.editedIndex > -1) {
        Object.assign(this.courseProgrammChildrens[this.editedIndex], this.editedItem);
      } else {
        this.courseProgrammChildrens.push(this.editedItem);
      }
      this.close();
    },
  },
};
</script>

<style>
.box {
  display: flex;
  align-items: center;
  justify-content: center;
}

</style>