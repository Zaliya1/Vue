<template>
  <div class="btn">
    <button class="form-btn" v-on:click="saveAll" v-if="!successText">
      Завершить регистрацию
    </button>
    <span class="successText" v-if="successText"
      >Спасибо! Наш менеджер свяжется с вами</span
    >
  </div>
</template>
<script>
export default {
  name: "SendData",
  data() {
    return {
      successText: false,
    };
  },
  props: {
    persons: { type: Array },
    doctorsObject: { type: Object },
  },
  methods: {
    saveAll() {
      this.$emit("saveAll");
      this.successText = true;
    },
  },
};
</script>
<style>
.successText {
  font-size: 20px;
  font-weight: 600;
  padding: 30px 0px;
}
</style>