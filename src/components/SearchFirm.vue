<template>
  <div class="select__firm">
    <div class="select__header">
      <input
        type="text"
        placeholder="Введите название организации"
        class="select__current select__input"
        v-if="index.length === 0"
        v-on:input="searchSelect"
        v-on:click="changeSelect"
        v-model="selectValue"
      />

      <p class="select__current select__span" v-if="index.length > 0">
        {{ firms[index].value }}
      </p>
    </div>
    <button class="select__btn" v-on:click="clearSelect">
      <svg
        width="57"
        height="45"
        viewBox="0 0 30 28"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          d="M5 8.16669H25"
          stroke="#5E5E5E"
          stroke-width="1.75"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
        <path
          d="M12.5 12.8333V19.8333"
          stroke="#5E5E5E"
          stroke-width="1.75"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
        <path
          d="M17.5 12.8333V19.8333"
          stroke="#5E5E5E"
          stroke-width="1.75"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
        <path
          d="M6.25 8.16669L7.5 22.1667C7.5 22.7855 7.76339 23.379 8.23223 23.8166C8.70107 24.2542 9.33696 24.5 10 24.5H20C20.663 24.5 21.2989 24.2542 21.7678 23.8166C22.2366 23.379 22.5 22.7855 22.5 22.1667L23.75 8.16669"
          stroke="#5E5E5E"
          stroke-width="1.75"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
        <path
          d="M11.25 8.16667V4.66667C11.25 4.35725 11.3817 4.0605 11.6161 3.84171C11.8505 3.62292 12.1685 3.5 12.5 3.5H17.5C17.8315 3.5 18.1495 3.62292 18.3839 3.84171C18.6183 4.0605 18.75 4.35725 18.75 4.66667V8.16667"
          stroke="#5E5E5E"
          stroke-width="1.75"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
      </svg>
    </button>
  </div>
</template>

<script>
export default {
  name: "SearchFirm",
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
    changeSelect() {
      this.$emit("changeSelect");
    },
    searchSelect() {
      this.$emit("searchSelect", this.selectValue);
    },
    clearSelect() {
      this.$emit("clearSelect");
      this.selectValue = "";
    },
  },
};
</script>


<style>
.select__firm {
  display: flex;
  cursor: pointer;
}
.select__btn {
  background-color: white;
}
.select__header {
  display: flex;
  border: 2px solid #ccc;
  cursor: pointer;
  justify-content: space-between;
  width: 50%;
  border-radius: 8px;
  transition: border 1s ease;
}

.select__current {
  font-size: 20px;
  line-height: 2;
  padding: 8px;
  margin: 0px;
  align-self: center;
  font-weight: 500;
}
input {
  padding: 0;
  border: 0px;
  width: 100%;
}
.select__btn {
  padding: 0;
  border: 0;
  width: 60px;
  background-size: 80%;
  background-repeat: no-repeat;
  background-position: center center;
  height: 60px;
  cursor: pointer;
  transition: outline 1s ease;
}
.select__header:hover,
.select__header:focus {
  border-color: #e1670e;
}
.select__btn:hover path {
  stroke: #e1670e;
}
.select__btn path {
  transition: stroke 1s ease;
}
.select__btn:focus-visible {
  outline: 1px solid #e1670e;
}
</style>
