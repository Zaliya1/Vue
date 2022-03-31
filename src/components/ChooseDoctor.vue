<template>
  <section class="doctor-section">
    <ul v-if="directionName !== ''" class="doctor__list">
      <li
        v-for="nameDoctor in doctorsDirection[this.directionName]"
        :key="nameDoctor"
        class="doctor__item"
      >
        <img
          :src="itemImage(doctorsObject[nameDoctor][`info`][2])"
          alt="Фото врача"
          class="doctor__photo"
        />
        <div class="doctor__information">
          <p>{{ nameDoctor }}</p>
          <p>{{ doctorsObject[nameDoctor][`info`][0] }}</p>
          <p>Стаж: {{ doctorsObject[nameDoctor][`info`][1] }}</p>
          <button
            v-on:click="chooseDoctor(nameDoctor)"
            class="doctor__btn"
            v-bind:class="[nameDoctor === activeName ? 'active' : '']"
          >
            Выбрать специалиста
          </button>
        </div>
      </li>
    </ul>
  </section>
</template>

<script>
export default {
  name: "ClientsForm",
  data() {
    return {
      doctorsDirection: {
        Гастроэнтерология: [
          "Имаева Светлана Игоревна",
          "Петрова Аэлита Венеровна",
        ],
        Гинекология: [
          "Абдуллина Алия Маратовна",
          "Альмухаметов Аэлита Рамилевна",
        ],
        Дерматовенерология: [
          "Медведев Петр Николаевич",
          "Валеева Эльза Сергеевна",
        ],
        Диетология: [
          "Шарифуллин Эдуард Васильевич",
          "Чижкова Екатерина Викторовна",
        ],
        Кардиология: ["Хайретдинов Ямиль Мусаевич", "Сидоров Артем Петрович"],
        Стоматология: [
          "Азаматова Гузель Карамовна",
          "Булатов Ильнур Айнурович",
        ],
      },
      doctorsKey: "",
      activeName: "",
      areOptionsVisible: false,
    };
  },
  props: {
    persons: { type: Array },
    doctorsObject: { type: Object },
    directionName: { type: String },
  },
  methods: {
    chooseDirection(valueDirection) {
      this.doctorsKey = valueDirection;
      this.$emit("chooseDirection", valueDirection);
    },
    chooseDoctor(valueDoctor) {
      this.$emit("chooseDoctor", valueDoctor);
      this.activeName = valueDoctor;
      console.log(this.activeName);
    },
    itemImage(fileName) {
      return require(`@/assets/img/${fileName}`);
    },
    selectOption(option) {
      console.log(option);
    },
  },
};
</script>

<style>
.class {
  background-image: url(@/assets/img/4.png);
}
.doctor__item {
  display: flex;
  width: 50%;
  margin-bottom: 10px;
}
.doctor__information {
  display: flex;
  flex-direction: column;
  font-size: 17px;
  justify-content: space-between;
}
.doctor__photo {
  width: 20%;
  margin-right: 5%;
}
.doctor__select {
  width: 32%;
  height: 100%;
  border-radius: 0.7rem;
  font-size: 20px;
  border: 1px solid #e2e2e2;
  padding: 10px 10px;
  color: #000;
  margin: 0;
}
.doctor__option {
  width: 32%;
  height: 100%;
  border-radius: 0.7rem;
  font-size: 20px;
  border: 1px solid #e2e2e2;
  padding: 10px 10px;
  color: #000;
  margin: 0;
}
.doctor__btn {
  color: black;
  font-family: Roboto, sans-serif;
  font-weight: 600;
  padding: 7px 1px;
  cursor: pointer;
  border-color: #ff9900;
  background-color: #fff;
  width: 80%;
  border-width: 2px;
  transition: all 1s ease;
}
.doctor__btn:hover,
.doctor__btn:focus {
  border-color: #e1670e;
  background-color: #f7b045;
}
</style>