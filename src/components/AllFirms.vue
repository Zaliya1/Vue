<template>
  <ul class="select__body" v-if="openOptions">
    <li
      class="select__item"
      v-on:click="SelectedOption(index)"
      v-for="(firm, index) in firms"
      :key="index"
    >
      <p class="select__info">{{ firm.value }}</p>
      <p class="select__info">{{ firm.data.address.value }}</p>
    </li>
  </ul>
</template>
<script>
export default {
  name: "AllFirms",
  props: {
    firms: { type: Array },
    openOptions: { type: Boolean },
  },
  methods: {
    SelectedOption(index) {
      this.$emit("SelectedOption", index);
    },
  },
};
</script>
<style>
ul {
  list-style-type: none;
  margin: 0;
  padding: 0;
}
.select__info {
  padding: 0px;
  margin: 0px;
}
.select__body {
  width: 50%;
  cursor: pointer;
}

.select__item {
  line-height: 2;
  padding: 8px;
  font-size: 16px;
  border: 1px solid #ccc;
  border-top: 0;
}

.select__item:hover {
  background-color: #f2f2f2;
}
</style>