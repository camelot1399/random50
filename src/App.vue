<template>
  <div id="app">
    <button @click="showTable">Сгенерировать</button>

    <TableCompoennt 
      v-if="shownTable"
      :data="inTableData"
    />
  </div>
</template>

<script>
import TableCompoennt from "@/components/Table";

export default {
  name: 'App',
  data() {
    return {
      shownTable: false,
      inTableData: [],
    }
  },
  components: {
    TableCompoennt
  },
  methods: {
    showTable() {
      this.inTableData = [];  // обнуляем массив на случай повторого нажатия на кнопку: сгенерировать
      this.shownTable = !this.shownTable;
      this.generateTable();
    },
    generateTable() {
      const countRows = 50;   // кол-во сток
      const minPrice = 0.01;  // минимальная цена
      const maxPrice = 1000;  // максимальная цена
      const minCount = 1;     // минимальное кол-во
      const maxCount = 100;   // максимальное кол-во

      console.log(minPrice.toFixed(2));
      console.log(maxPrice.toFixed(2));

      console.log(maxPrice - minPrice);
      

      for (let i = 0; i < countRows; i++) {
        let item = {};
        item.id = i;
        item.name = this.generateLetters();
        item.price = this.getRandomNumber(minPrice, maxPrice).toFixed(2);
        item.count = this.getRandomNumber(minCount, maxCount).toFixed(0);

        this.inTableData.push(item);
      }
    },
    getRandomNumber(min, max) {
      return Math.random() * (max - min) + min;
    },
    generateLetters() {
      let result = '';
      const countLetters = 5;  // кол-во букв
      const russianLetters = 'яюэьыъщшчцхфутсрпонмлкйизжёедгвба';
      const max_position = russianLetters.length - 1;
      
      for(let i = 0; i < countLetters; ++i ) {
          let position = Math.floor(Math.random() * max_position);
          result = result + russianLetters.substring(position, position + 1);
      }

      return result;
    }
  }
}
</script>
