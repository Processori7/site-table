
<template>
  <v-app>
    <v-data-table
    :items-per-page="-1" 
    :items="courseProgrammChildrens" 
    :headers="headers"
      class="elevation-1"
    ></v-data-table>
    <!-- Навигация -->
    
    <v-bottom-navigation

      color="primary"
      grow
    >
      <v-btn type="button" @click="show_add= !show_add">
        <span>Добавить данные</span>
      </v-btn>
  
      <v-btn type="button" @click="show_change= !show_change">
        <span>Изменить данные</span>
  
      </v-btn>
  
      <v-btn type="button" @click="Del_data">
        <span>Удалить данные</span>
  
      </v-btn>
    </v-bottom-navigation>
    
    <!-- Если show_add:true, появляется форма добавления данных -->
    <div v-if="show_add" >
      <v-text-field v-model="ID" label="Введите ID" v-on:input="ID = $event.target.value"></v-text-field>
      <v-text-field v-model="Code" label="Введите Code" v-on:input="Code = $event.target.value"></v-text-field>
      <v-text-field v-model="Name" label="Введите Name" v-on:input="Name = $event.target.value"></v-text-field>
      <v-text-field v-model="Year" label="Введите Year" v-on:input="Year = $event.target.value"></v-text-field>
      <v-text-field v-model="EduForm" label="Введите EduForm" v-on:input="EduForm = $event.target.value"></v-text-field>
      <v-text-field v-model="EduLevel" label="Введите Edulevel" v-on:input="EduLevel = $event.target.value"></v-text-field>
      <v-text-field v-model="ParentProgramm" label="ParentProgram" v-on:input="ParentProgramm = $event.target.value"></v-text-field>
      <v-btn  type="button" @click="Add_data(ID, Code, Name, Year, EduForm, EduLevel, ParentProgramm)">Добавить данные</v-btn>
</div>
<!-- Если show_change:true, появляется форма изменения данных -->
  <div v-if ='show_change'>
    <v-combobox
    filled
  hide-selected
  outlined
  :items="courseProgrammChildrens" 
  :item-text="item => item.ID" 
  v-model="ID"
  @input="ID = $event.target.value"
  :item-value="item => item.ID"
></v-combobox>
<v-combobox
  filled
  hide-selected
  outlined
  :items="courseProgrammChildrens" 
  item-text="Code"
  item-value="Code"
  v-model="Code"
  v-on:input="[ID, Code, Name, Year, EduForm, EduLevel, ParentProgramm] = [ID, $event.target.value, Name, Year, EduForm, EduLevel, ParentProgramm]"
></v-combobox>
<v-combobox
  filled
  hide-selected
  outlined
  :items="courseProgrammChildrens" 
  item-text="Name" 
  item-value="Name"
  v-model="Name"
  v-on:input="[ID, Code, Name, Year, EduForm, EduLevel, ParentProgramm] = [ID, Code, $event.target.value, Year, EduForm, EduLevel, ParentProgramm]"
></v-combobox>
<v-combobox
  filled
  hide-selected
  outlined
  :items="courseProgrammChildrens" 
  item-text="Year" 
  item-value="Year"
  v-model="Year"
  v-on:input="[ID, Code, Name, Year, EduForm, EduLevel, ParentProgramm] = [ID, Code, Name, $event.target.value, EduForm, EduLevel, ParentProgramm]"
></v-combobox>
<v-combobox
  filled
  hide-selected
  outlined
  :items="courseProgrammChildrens" 
  item-text="EduForm" 
  item-value="EduForm"
  v-model="EduForm"
  v-on:input="[ID, Code, Name, Year, EduForm, EduLevel, ParentProgramm] = [ID, Code, Name, Year, $event.target.value, EduLevel, ParentProgramm]"
></v-combobox>
<v-combobox
  filled
  hide-selected
  outlined
  :items="courseProgrammChildrens" 
  item-text="EduLevel" 
  item-value="EduLevel"
  v-model="EduLevel"
  v-on:input="[ID, Code, Name, Year, EduForm, EduLevel, ParentProgramm] = [ID, Code, Name, Year, EduForm, $event.target.value, ParentProgramm]"
></v-combobox>
<v-combobox
  filled
  hide-selected
  outlined
  :items="courseProgrammChildrens" 
  item-text="ParentProgramm" 
  item-value="ParentProgramm"
  v-model="ParentProgramm"
  v-on:input="[ID, Code, Name, Year, EduForm, EduLevel, ParentProgramm] = [ID, Code, Name, Year, EduForm, EduLevel, $event.target.value]"
></v-combobox>
<v-btn  type="button" @click="Change_data(ID, Code, Name, Year, EduForm, EduLevel, ParentProgramm)">Изменить данные</v-btn>
  </div>
  </v-app>
</template>



<script>
export default {
  data() {
    return {

      // znach:{
      // ID: '',
      // Code: '',
      // Name: '',
      // Year: '',
      // EduForm: '',
      // EduLevel: '',
      // ParentProgramm: '',
      // },

      ID: '',
      Code: '',
      Name: '',
      Year: '',
      EduForm: '',
      EduLevel: '',
      ParentProgramm: '',

      show_add: false,
      show_change: false,

      headers: [
        {
          text: 'Образовательная программа',
          align: 'start',
          sortable: false,
          value: 'name',
        },
        { text: 'ID', value: 'ID' },
        { text: 'Code', value: 'Code' },
        { text: 'Name', value: 'Name' },
        { text: 'Year', value: 'Year' },
        { text: 'EduForm', value: 'EduForm' },
        { text: 'EduLevel', value: 'EduLevel' },
        { text: 'ParentProgramm', value: 'ParentProgramm' }
      ],

      obr_form:[{
        id: 1,
        Name: 'Образовательная форма 1',
      },
      { id: 2,
        Name: 'Образовательная форма 2'},

      {id: 3,
        Name: 'Образовательная форма 3'},

      {id: 4,
        Name: 'Образовательная форма 4'},
      {
        id: 5,
        Name: 'Образовательная форма 5'
      }

    ],

    level_obr:[{
      id: 11,
      Name: 'Уровень образования 1',
    },
    { id: 22,
      Name: 'Уровень образования 2'},
      {
      id: 33,
      Name: 'Уровень образования 3',
    },
    { id: 44,
      Name: 'Уровень образования 4'}
    
    ],

      courseProgrammChildrens: [
        {
          ID: null,
          Code: "",
          Name: "",
          Year: null,
          EduForm: null,
          EduLevel: null,
          ParentProgramm: null,
        },
        
      ],

    };
  },
  methods: {

    // saveData() {
    //   var data = {
    //     ID: this.courseProgrammChildrens.ID,
    //     Code: this.courseProgrammChildrens.Code,
    //     Name: this.courseProgrammChildrens.Name,
    //     Year: this.courseProgrammChildrens.Year,
    //     EduForm: this.courseProgrammChildrens.EduForm,
    //     EduLevel: this.courseProgrammChildrens.EduLevel,
    //     ParentProgramm: this.courseProgrammChildrens.ParentProgramm
    //   };

    Add_data(ID, Code, Name, Year, EduForm, EduLevel, ParentProgramm){
      //alert(ID + " " + Code + " " + Name + " " + Year + " " + EduForm + " " + EduLevel + " " + ParentProgramm);
      // this.$refs.myDataTable.items.push({ ID: ID, Code: Code, Name: Name, Year: Year, EduForm: EduForm, EduLevel: EduLevel, ParentProgramm: ParentProgramm})
      this.courseProgrammChildrens.push({
        ID: ID,
        Code: Code,
        Name: Name,
        Year: Year,
        EduForm: EduForm,
        EduLevel: EduLevel,
        ParentProgramm: ParentProgramm,
      });
      this.show = false;

    },
    
    Change_data(ID, Code, Name, Year, EduForm, EduLevel, ParentProgramm){
      
      alert(this.ID + " " + Code + " " + Name + " " + Year + " " + EduForm + " " + EduLevel + " " + ParentProgramm);
      if (ID && Code && Name && Year && EduForm && EduLevel && ParentProgramm !=='undefined') {
      //   this.courseProgrammChildrens.push({
      //   ID: ID,
      //   Code: Code,
      //   Name: Name,
      //   Year: Year,
      //   EduForm: EduForm,
      //   EduLevel: EduLevel,
      //   ParentProgramm: ParentProgramm,
        
      // })
      
      // this.$refs.dataTable.updateItem()({
      // ID: ID,
      // Code: Code,
      // Name: Name,
      // Year: Year,
      // EduForm: EduForm,
      // EduLevel: EduLevel,
      // ParentProgramm: ParentProgramm
      // })

      
      }
      else{
        alert("Заполните все поля");
      }
    
  },
      
  Del_data(){

  }
}
};
</script>

<style>

.box {
  display: flex;
  align-items: center;
  justify-content: center;
}

.box div {
  width: 150px;
  height: 150px;
  align-items: center;
  justify-content: center;
}
</style>