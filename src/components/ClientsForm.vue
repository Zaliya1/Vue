<template>
  <section class="clients-section">
    <p class="step">Шаг 3</p>
    <h3>Введите данные пациентов</h3>
    <form id="form2">
      <div class="work-experiences">
        <div
          class="form-row"
          v-for="(client, index) in clientArray"
          :key="index"
        >
          <div class="person">
            <input
              v-model="client.name"
              :name="`clientArray[${index}][name]`"
              type="text"
              required="required"
              class="input-form client-name"
              placeholder="Введите имя"
              v-on:input="
                validateInputs(client.name, index, 'name'), checkInputs()
              "
              v-on:blur="
                validateBlur(client.name, index, 'name'), checkInputs()
              "
            />
            <input
              v-model="client.surname"
              :name="`clientArray[${index}][surname]`"
              type="text"
              required="required"
              class="input-form client-surname"
              placeholder="Фамилия"
              v-on:input="
                validateInputs(client.surname, index, 'surname'), checkInputs()
              "
              v-on:blur="
                validateBlur(client.surname, index, 'surname'), checkInputs()
              "
            />
            <input
              v-model="client.patronymic"
              :name="`clientArray[${index}][patronymic]`"
              type="text"
              required="required"
              class="input-form client-patronymic"
              placeholder="Отчество"
              v-on:input="
                validateInputs(client.patronymic, index, 'patronymic')
              "
              v-on:blur="validateBlur(client.patronymic, index, 'patronymic')"
            />
          </div>
        </div>
      </div>
    </form>
    <div class="buttons">
      <button v-on:click="addClient" type="button" class="client-btn">+</button>
      <button class="select__btn" v-on:click="removeClient">
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
          ></path>
          <path
            d="M12.5 12.8333V19.8333"
            stroke="#5E5E5E"
            stroke-width="1.75"
            stroke-linecap="round"
            stroke-linejoin="round"
          ></path>
          <path
            d="M17.5 12.8333V19.8333"
            stroke="#5E5E5E"
            stroke-width="1.75"
            stroke-linecap="round"
            stroke-linejoin="round"
          ></path>
          <path
            d="M6.25 8.16669L7.5 22.1667C7.5 22.7855 7.76339 23.379 8.23223 23.8166C8.70107 24.2542 9.33696 24.5 10 24.5H20C20.663 24.5 21.2989 24.2542 21.7678 23.8166C22.2366 23.379 22.5 22.7855 22.5 22.1667L23.75 8.16669"
            stroke="#5E5E5E"
            stroke-width="1.75"
            stroke-linecap="round"
            stroke-linejoin="round"
          ></path>
          <path
            d="M11.25 8.16667V4.66667C11.25 4.35725 11.3817 4.0605 11.6161 3.84171C11.8505 3.62292 12.1685 3.5 12.5 3.5H17.5C17.8315 3.5 18.1495 3.62292 18.3839 3.84171C18.6183 4.0605 18.75 4.35725 18.75 4.66667V8.16667"
            stroke="#5E5E5E"
            stroke-width="1.75"
            stroke-linecap="round"
            stroke-linejoin="round"
          ></path>
        </svg>
      </button>
    </div>
    <div class="btn">
      <button
        class="form-btn"
        type="button"
        v-on:click="saveClientForm"
        v-if="check"
      >
        Далее
      </button>
    </div>
  </section>
</template>

<script>
export default {
  name: "ClientsForm",
  data: () => ({
    clientArray: [
      {
        name: "",
        surname: "",
        patronymic: "",
      },
    ],
    check: false,
  }),

  methods: {
    addClient() {
      this.clientArray.push({
        name: "",
        surname: "",
        patronymic: "",
      });
    },
    removeClient() {
      if (this.clientArray.length > 1) {
        this.clientArray.pop();
      }
    },
    checkInputs() {
      this.clientArray.forEach((client) => {
        if (client.name !== "" && client.surname !== "") {
          this.check = true;
        } else {
          this.check = false;
        }
      });
    },
    validateInputs(str, index, key) {
      const regex = /[^а-яА-Я]/g;
      this.clientArray[index][key] = str.replace(regex, "");
    },
    validateBlur(str, index, key) {
      const regex = /[^а-яА-Я]/g;
      this.clientArray[index][key] = str.replace(regex, "");
      //1 буква к верхнему регистру, остальные к маленькому
      let updateName = "";
      for (let i = 0; i < this.clientArray[index][key].length; i++) {
        if (i === 0) {
          updateName += this.clientArray[index][key][i].toUpperCase();
        } else {
          updateName += this.clientArray[index][key][i].toLowerCase();
        }
      }
      this.clientArray[index][key] = updateName;
    },
    saveClientForm() {
      this.$emit("saveClientForm", this.clientArray);
    },
  },
};
</script>

<style>
.client-name,
.client-surname {
  margin-right: 2%;
  margin-bottom: 10px;
}
.client-btn {
  background-color: #a52a2a;
  border: none;
  padding: 5px;
  border-radius: 5px;
  color: white;
  min-height: 38px;
  min-width: 38px;
  cursor: pointer;
  transition: all 1s;
  width: 47px;
  font-size: 32px;
}
.client-btn:hover {
  background-color: #e1670e;
}
.buttons {
  display: flex;
}
</style>
