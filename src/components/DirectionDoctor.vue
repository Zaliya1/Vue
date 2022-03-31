<template>
  <section class="direction-section">
    <p class="step">Шаг 4</p>
    <h3>Выберите специалиста</h3>
    <p
      class="direction__select"
      v-on:click="areOptionsVisible = !areOptionsVisible"
    >
      {{ select }}
    </p>
    <div class="options" v-if="areOptionsVisible">
      <p
        class="option"
        v-for="(name, option) in doctorsDirection"
        :key="name.value"
        v-on:click="selectOption(option)"
      >
        {{ option }}
      </p>
    </div>
  </section>
</template>

<script>
export default {
  name: "ClientsForm",
  data() {
    return {
      doctorsKey: "",
      activeName: "",
      areOptionsVisible: false,
      select: "Выберите направление",
    };
  },
  props: {
    doctorsDirection: { type: Object },
  },
  methods: {
    selectOption(option) {
      this.$emit("selectOption", option);
      this.areOptionsVisible = false;
      this.select = option;
    },
  },
};
</script>

<style>
.direction__select {
  width: 300px;
  position: relative;
  border: 1px solid #ff9900;
  cursor: pointer;
  transition: all 1s ease;
  font-size: 20px;
  padding: 4px;
}
.options {
  border: 1px solid #ff9900;
  position: absolute;
  cursor: pointer;
  background-color: white;
  width: 300px;
  border-top: 0px;
  border-bottom: 0px;
  font-size: 20px;
}
.option:hover,
.direction__select:hover {
  background-color: #f3ecec;
}
.option {
  border-bottom: 1px solid #ff9900;
  padding: 4px;
}
p {
  margin: 0;
}
</style>