<template>
  <form
      id="newCar"
      @submit.prevent="checkForm"
      method="post"
  >
    <div class="form_title">
      Добавить новый автомобиль
    </div>

    <p v-if="errors.length">
      <b>Пожалуйста исправьте указанные ошибки:</b>
      <ul>
        <li v-for="error in errors">{{ error }}</li>
      </ul>
    </p>

    <label for="model">Модель</label>
    <input
        type="text"
        id="model"
        v-model="model"
        name="model"
    >

    <label for="number">Номер</label>
    <input
        type="text"
        id="number"
        v-model="number"
        name="number"
    >

    <label for="color">Цвет</label>
    <select
        id="color"
        v-model="color_id"
        name="color"
    >
      <option value="" disabled selected>Выберите цвет</option>
      <option
          v-for="item in colors.data"
          :value="item.id"
      >
        {{ item.name }}
      </option>
    </select>

    <label for="comment">Комментарий</label>
    <textarea
        id="comment"
        v-model="comment"
        name="comment"
    ></textarea>

    <input
        type="submit"
        class="button"
        value="Добавить"
    >
  </form>
</template>

<script>
import axios from "axios";
import CarTable from "@/components/CarTable.vue";
import {resolveDirective} from "vue";

export default {
  name: "FormAddCar",
  data() {
    return {
      errors: [],
      model: null,
      number: null,
      color_id: null,
      comment: null,
      colors: []
    }
  },
  methods: {
    getColors: function (e) {
      axios
          .get('http://127.0.0.1/api/colors/all')
          .then(response => (this.colors = response.data));
    },
    checkForm: function (e) {
      if (
          this.model &&
          this.number &&
          this.color_id &&
          this.comment &&
          this.number.match(/[А-Я]\d{3}[А-Я]{2}\d{2,3}/)
      ) {
        let modelData = {
          model: this.model,
          number: this.number,
          color_id: this.color_id,
          comment: this.comment
        }
        axios
            .post('http://127.0.0.1/api/models', modelData)
            .then(response => {
            });

        this.model = null;
        this.number = null;
        this.color_id = null;
        this.comment = null
        alert('Данные успешно добавлены');
        window.location.href = '/';
      } else {
        this.errors = [];

        if (!this.model) {
          this.errors.push('Необходимо ввести модель')
        }

        if (!this.number || !this.number.match(/[А-Я]\d{3}[А-Я]{2}\d{2,3}/)) {
          this.errors.push('Необходимо ввести номер формата А001АА72')
        }

        if (!this.color_id) {
          this.errors.push('Необходимо ввести цвет')
        }

        e.preventDefault();
      }
    }
  },
  async mounted() {
    await this.getColors();
  }
}
</script>

<style scoped>
.form_title {
  text-align: center;
  margin-top: 20px;
}

form {
  display: flex;
  flex-direction: column;
  width: 300px;
  margin: 0 auto;
}

form label {
  margin-top: 15px;
}

form input, select, textarea {
  /*height: 40px;*/
  width: 100%;
  padding: 10px;
  margin: 0 auto;
  font-size: 18px;
  border: 1px solid #8C7AAE;
  border-radius: 30px;
}

form textarea {
  height: 100px;
  resize: none;
}

form .button {
  /*height: 50px;*/
  width: 200px;
  padding: 10px;
  text-align: center;
  font-size: 20px;
  font-weight: 500;
  background: #EDEDED;
  border-radius: 30px;
  margin: 20px auto 0;
  cursor: pointer;
}

form .button:hover {
  background: #e0dfdf;
}

.form_title {
  color: #18063A;
  font-size: 26px;
  font-weight: 400;
}
</style>