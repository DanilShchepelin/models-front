<script setup>
import CarTable from "@/components/CarTable.vue";
import FormAddCar from "@/components/FormAddCar.vue";
</script>

<template>
  <header>
    <div class="container">
      <div class="header_title">
        Таблица автомобилей
      </div>
    </div>
  </header>

  <div class="container">
    <div class="content">
      <FormAddCar />
      <CarTable />
    </div>
  </div>

  <div class="container">

  </div>
</template>

<style scoped>
header {
  background: #EDEDED;
}

.container {
  width: 1170px;
  margin: 0 auto;
}

.container .header_title {
  text-align: center;
  color: #18063A;
  font-size: 38px;
  font-weight: 500;
}

.content {
  display: flex;
  align-items: flex-start;
}
</style>
