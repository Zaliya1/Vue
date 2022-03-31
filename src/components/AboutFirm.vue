<template>
  <div class="info__firm">
    <p class="information">ИНН: {{ firms[index].data.inn }}</p>
    <p class="information">КПП: {{ firms[index].data.kpp }}</p>
    <p class="information">
      Адрес: {{ firms[index].data.address.unrestricted_value }}
    </p>
    <div class="btn">
      <button class="form-btn" type="submit" v-on:click="ActivateStep2">
        Сохранить
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "AboutFirm",
  data() {
    return {
      selectValue: "",
    };
  },
  props: {
    index: { type: String },
    firms: { type: Array },
  },
  methods: {
    ActivateStep2() {
      this.$emit("ActivateStep2");
    },
  },
};
</script>
<style>
.info__firm {
  font-size: 20px;
}

.form-btn:hover,
.form-btn:focus {
  border-color: #e1670e;
  background-color: #f7b045;
}
.information {
  margin-bottom: 5px;
}
</style>
