<template>
  <table class="table">
    <thead>
      <tr>
        <th>№</th>
        <th>Модель</th>
        <th>Номер</th>
        <th>Цвет</th>
        <th>Комментарий</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="model in models.data" :key="model.id">
        <td>{{ model.id }}</td>
        <td>{{ model.model }}</td>
        <td>{{ model.number }}</td>
        <td>
          <div>{{model.color?.name}}</div>
        </td>
        <td>{{ model.comment }}</td>
      </tr>
    </tbody>
  </table>
</template>

<script>
import axios from "axios";
export default {
  name: "CarTable",
  data() {
    return {
      models: []
    }
  },
  methods: {
    fetchAllModels() {
      axios
          .get('http://127.0.0.1/api/models')
          .then(response => (this.models = response.data));
    }
  },
  async mounted() {
    await this.fetchAllModels();
  }
}
</script>

<style scoped>
.table {
  width: 700px;
  border: none;
  margin-bottom: 20px;
  border-collapse: collapse;
  margin-top: 30px;
}
.table thead th {
  font-weight: bold;
  text-align: left;
  border: none;
  padding: 10px 15px;
  background: #EDEDED;
  font-size: 14px;
  /*border-top: 1px solid #ddd;*/
}
.table tr th:first-child, .table tr td:first-child {
  /*border-left: 1px solid #ddd;*/
}
.table tr th:last-child, .table tr td:last-child {
  /*border-right: 1px solid #ddd;*/
}
.table thead tr th:first-child {
  border-radius: 20px 0 0 0;
}
.table thead tr th:last-child {
  border-radius: 0 20px 0 0;
}
.table tbody td {
  text-align: left;
  border: none;
  padding: 10px 15px;
  font-size: 14px;
  vertical-align: top;
}
.table tbody tr:nth-child(even) {
  background: #F8F8F8;
}
.table tbody tr:last-child td{
  /*border-bottom: 1px solid #ddd;*/
}
.table tbody tr:last-child td:first-child {
  border-radius: 0 0 0 20px;
}
.table tbody tr:last-child td:last-child {
  border-radius: 0 0 20px 0;
}
</style>