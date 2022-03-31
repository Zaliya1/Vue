<template>
  <header class="header">
    <div class="container header__container">
      <a href="/" class="header__link"
        ><img src="@/assets/img/main_logo.svg" alt=""
      /></a>
      <nav class="header__nav">
        <ul class="nav__list">
          <li class="nav__item"><a class="nav__link" href="/">О нас</a></li>
          <li class="nav__item"><a class="nav__link" href="/">Врачи</a></li>
          <li class="nav__item"><a class="nav__link" href="/">Услуги</a></li>
          <li class="nav__item"><a class="nav__link" href="/">Акции</a></li>
          <li class="nav__item"><a class="nav__link" href="/">Отзывы</a></li>
          <li class="nav__item"><a class="nav__link" href="/">Контакты</a></li>
        </ul>
      </nav>
    </div>
  </header>
</template>

<style>
.header__container {
  display: flex;
  justify-content: space-between;
}
.nav__list {
  display: flex;
  justify-content: space-between;
  width: 100%;
}
.header__nav {
  width: 50%;
}
.nav__item {
  font-size: 20px;
}
.nav__link {
  text-decoration: none;
  color: black;
  font-weight: 600;
  transition: color 1s ease;
}
.header {
  padding-top: 20px;
  background-color: #f0ffff;
}
.nav__link:hover,
.nav__link:focus {
  color: #e1670e;
}
</style>