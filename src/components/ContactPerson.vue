<template>
  <section class="form-section">
    <p class="step">Шаг 2</p>
    <h3>Введите данные контактного лица</h3>
    <form id="form1" name="user_form" v-on:submit.prevent="saveForm">
      <input
        class="input-form form-name"
        type="text"
        name="user_name"
        placeholder="Ваше имя"
        required="required"
        v-model.trim="inputName"
        v-on:input="validateNameInput(inputName)"
        v-on:blur="validateNameBlur(inputName)"
      />

      <input
        class="input-form form-email"
        type="email"
        name="user_email"
        placeholder="E-mail"
        required="required"
        v-model.trim="inputEmail"
        v-on:input="validateEmail(inputEmail)"
        v-on:blur="validateEmail(inputEmail)"
      />

      <input
        class="input-form form-phone"
        type="tel"
        name="user_phone"
        placeholder="Номер телефона"
        required="required"
        v-model.trim="inputPhone"
        v-on:input="validatePhone(inputPhone)"
        v-on:blur="validatePhone(inputPhone)"
      />

      <input
        class="mess"
        name="user_message"
        placeholder="Ваше сообщение"
        v-model.trim="inputMess"
        v-on:input="validateMess(inputMess)"
        v-on:blur="validateMess(inputMess)"
      />
      <div class="btn">
        <button
          class="form-btn"
          type="submit"
          v-on:click="saveForm"
          v-if="inputName !== '' && inputEmail !== '' && inputPhone !== ''"
        >
          Сохранить
        </button>
      </div>
    </form>
  </section>
</template>

<script>
export default {
  name: "ContactPerson",
  data() {
    return {
      inputName: "",
      inputEmail: "",
      inputPhone: "",
      inputMess: "",
      updateName: "",
    };
  },
  methods: {
    saveForm() {
      this.$emit(
        "saveForm",
        this.inputName,
        this.inputEmail,
        this.inputPhone,
        this.inputMess
      );
    },
    validateEmail(inputEmail) {
      const regex = /[^\w @ - . ! ~ * ']/g;
      this.inputEmail = inputEmail.replace(regex, "");
    },
    validatePhone(inputPhone) {
      const regex = /[^\d\- ( ) +]/g;
      this.inputPhone = inputPhone.replace(regex, "");
    },
    validateMess(inputMess) {
      const regex = /[^а-яА-Я .   , ! ; : " ' - ? ( ) \d]/g;
      this.inputMess = inputMess.replace(regex, "");
    },
    validateNameInput(inputName) {
      const regex = /[^а-яА-Я ]/g;
      this.inputName = inputName.replace(regex, "");
    },
    validateNameBlur(inputName) {
      const regex = /[^а-яА-Я ]/g;
      this.inputName = inputName.replace(regex, "");
      this.updateName = "";
      if (!this.inputName.includes(" ")) {
        //если ввели только имя, пишем имя с большой буквы
        for (let i = 0; i < this.inputName.length; i++) {
          if (i === 0) {
            this.updateName += this.inputName[i].toUpperCase();
          } else {
            this.updateName += this.inputName[i].toLowerCase();
          }
        }
        this.inputName = this.updateName;
      } else {
        //если ввели только имя и фамилию, пишем имя с большой буквы, пробел, фамилию с большой буквы
        let arr = this.inputName.split(" ");
        for (let n = 0; n < arr.length; n++) {
          for (let i = 0; i < arr[n].length; i++) {
            if (i === 0) {
              this.updateName += arr[n][i].toUpperCase();
            } else {
              this.updateName += arr[n][i].toLowerCase();
            }
          }
          this.updateName += " ";
        }
        this.updateName = this.updateName.replace(/ $/g, ""); //удаление пробела в конце после строки 102
        this.inputName = this.updateName;
      }
    },
  },
};
</script>

<style>
.input-form {
  width: 32%;
  height: 100%;
  border-radius: 0.7rem;
  font-size: 20px;
  border: 1px solid #e2e2e2;
  padding: 10px 10px;
  color: #000;
  margin: 0;
}
.form-name,
.form-email {
  margin-right: 2%;
  margin-bottom: 10px;
}

.mess {
  width: 100%;
  border-radius: 0.7rem;
  font-size: 20px;
  border: 1px solid #e2e2e2;
  padding: 10px 10px;
  color: #000;
  margin-bottom: 10px;
}
.form-btn {
  display: block;
  font-size: 20px;
  color: #fff;
  font-family: Roboto, sans-serif;
  font-weight: 500;
  background-color: #ff9900;
  border-radius: 5rem;
  padding: 12px 38px;
  cursor: pointer;
  border-color: #ff9900;
}
.btn {
  width: 100%;
  display: flex;
  justify-content: center;
}
</style>