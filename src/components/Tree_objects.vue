<template>
    <v-treeview
      :items="items"
    ></v-treeview>
  </template>

<script>
export default {
  data: () => ({
    items: [
      {
        id: 1,
        name: 'Форма образования :',
        children: [
          { id: 2, name: 'Образовательная форма 1' },
          { id: 3, name: 'Образовательная форма 2' },
          { id: 4, name: 'Образовательная форма 3' },
          { id: 5, name: 'Образовательная форма 4' },
        ],
      },
      {
        id: 6,
        name: 'Уровень образования :',
        children: [
          { id: 7, name: 'Уровень образования 1' },
          { id: 8, name: 'Уровень образования 2' },
          { id: 9, name: 'Уровень образования 3' },

        ],
      },
    ],
  }),
}
</script>