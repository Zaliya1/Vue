<template>
  <section class="doctor-time-section">
    <div class="doctor-date">
      <p class="step">Шаг 5</p>
      <h3>Введите желаемую дату приема</h3>
      <input
        type="date"
        id="start"
        name="trip-start"
        min="2022-04-01"
        max="2022-04-16"
        class="input-date"
        v-model="doctorDate"
        v-on:change="chooseDoctorDate(doctorDate)"
      />
    </div>

    <ul v-if="doctorDate !== ''" class="doctor-time__list">
      <li
        v-for="(time, index) in this.doctorsObject[nameDoctor].date[doctorDate]"
        v-bind:class="[index === activeIndex ? 'active' : '']"
        :key="time"
        class="doctor-time__item"
        v-on:click="chooseDoctorTime(index)"
      >
        {{ time }}
      </li>
    </ul>
  </section>
</template>
<script>
export default {
  name: "DateOfAppointment",
  data() {
    return {
      doctorDate: "",
      doctorTime: "",
      activeIndex: -1,
    };
  },
  props: {
    nameDoctor: { type: String },
    doctorsObject: { type: Object },
  },
  methods: {
    chooseDoctorDate(doctorDate) {
      this.doctorDate = doctorDate;
    },
    chooseDoctorTime(index) {
      this.doctorTime =
        this.doctorsObject[this.nameDoctor].date[this.doctorDate][index];
      this.$emit("chooseDoctorTime", this.doctorDate, this.doctorTime);
      this.activeIndex = index;
    },
  },
};
</script>
<style>
.doctor-time__list {
  display: flex;
}
.doctor-date__select {
  margin-right: 5%;
  font-size: 20px;
  padding: 4px 28px;
  margin-right: 2%;
  border: 1px solid black;
  border-radius: 27px;
  cursor: pointer;
}
.doctor-time__item {
  font-size: 20px;
  padding: 4px 28px;
  margin-right: 2%;
  border: 1px solid black;
  border-radius: 27px;
  cursor: pointer;
  border-color: #ff9900;
  font-weight: 600;
}
.doctor-date {
  display: flex;
  margin-bottom: 10px;
}
.doctor-date {
  display: flex;
  flex-direction: column;
}
.input-date {
  width: 220px;
  height: 100%;
  font-size: 20px;
  border: 1px solid #e2e2e2;
  padding: 7px 10px;
  color: #000;
  margin: 0;
  border-color: #ff9900;
  cursor: pointer;
  transition: border 1s ease;
}
.doctor-time__item:hover,
.doctor-time__item:focus,
.input-date:hover,
.input-date:focus {
  border-color: #e1670e;
}
.doctor-time__item:hover,
.doctor-time__item:focus {
  border-color: #e1670e;
  background-color: #f7b045;
}
.active {
  background-color: #f7b045;
}
</style>