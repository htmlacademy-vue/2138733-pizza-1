<template>
  <div>
    <header class="header">
      <div class="header__logo">
        <a href="#" class="logo">
          <img
            src="@/assets/img/logo.svg"
            alt="V!U!E! Pizza logo"
            width="90"
            height="40"
          />
        </a>
      </div>
      <div class="header__cart">
        <a href="#">0 ₽</a>
      </div>
      <div class="header__user">
        <a href="#" class="header__login"><span>Войти</span></a>
      </div>
    </header>

    <main class="content">
      <form action="#" method="post">
        <div class="content__wrapper">
          <h1 class="title title--big">Конструктор пиццы</h1>

          <!-- Выбор теста -->
          <div class="content__dough">
            <div class="sheet">
              <h2 class="title title--small sheet__title">Выберите тесто</h2>

              <div class="sheet__content dough">
                <label
                  class="dough__input"
                  v-for="dough in doughs"
                  :key="dough.id"
                  :class="dough.className"
                >
                  <input
                    type="radio"
                    name="dough"
                    value="light"
                    class="visually-hidden"
                  />
                  <b>{{ dough.name }}</b>
                  <span>{{ dough.description }}</span>
                </label>
              </div>
            </div>
          </div>

          <!-- Выбор диаметра пиццы -->
          <div class="content__diameter">
            <div class="sheet">
              <h2 class="title title--small sheet__title">Выберите размер</h2>

              <div class="sheet__content diameter">
                <label
                  class="diameter__input"
                  v-for="size in sizes"
                  :key="size.id"
                  :class="size.className"
                >
                  <input
                    type="radio"
                    name="diameter"
                    value="small"
                    class="visually-hidden"
                  />
                  <span>{{ size.name }}</span>
                </label>
              </div>
            </div>
          </div>

          <!-- Выбор ингредиентов -->
          <div class="content__ingredients">
            <div class="sheet">
              <h2 class="title title--small sheet__title">
                Выберите ингредиенты
              </h2>

              <div class="sheet__content ingredients">
                <div class="ingredients__sauce">
                  <p>Основной соус:</p>

                  <label
                    class="radio ingredients__input"
                    v-for="sauce in pizza.sauces"
                    :key="sauce.id"
                  >
                    <input type="radio" name="sauce" :value="sauce.name" />
                    <span>{{ sauce.name }}</span>
                  </label>
                </div>

                <div class="ingredients__filling">
                  <p>Начинка:</p>

                  <ul class="ingredients__list">
                    <li
                      class="ingredients__item"
                      v-for="ingredient in ingredients"
                      :key="ingredient.id"
                    >
                      <span class="filling" :class="ingredient.className">{{
                        ingredient.name
                      }}</span>

                      <div class="counter counter--orange ingredients__counter">
                        <button
                          type="button"
                          class="counter__button counter__button--minus"
                          disabled
                        >
                          <span class="visually-hidden">Меньше</span>
                        </button>
                        <input
                          type="text"
                          name="counter"
                          class="counter__input"
                          value="0"
                        />
                        <button
                          type="button"
                          class="counter__button counter__button--plus"
                        >
                          <span class="visually-hidden">Больше</span>
                        </button>
                      </div>
                    </li>
                  </ul>
                </div>
              </div>
            </div>
          </div>

          <!-- Готовая пицца -->
          <div class="content__pizza">
            <label class="input">
              <span class="visually-hidden">Название пиццы</span>
              <input
                type="text"
                name="pizza_name"
                placeholder="Введите название пиццы"
              />
            </label>

            <div class="content__constructor">
              <div class="pizza pizza--foundation--big-tomato">
                <div class="pizza__wrapper">
                  <div class="pizza__filling pizza__filling--ananas"></div>
                  <div class="pizza__filling pizza__filling--bacon"></div>
                  <div class="pizza__filling pizza__filling--cheddar"></div>
                </div>
              </div>
            </div>

            <div class="content__result">
              <p>Итого: 0 ₽</p>
              <button type="button" class="button" disabled>Готовьте!</button>
            </div>
          </div>
        </div>
      </form>
    </main>
  </div>
</template>

<script>
import pizza from "@/static/pizza.json";

export default {
  name: "Index",
  data() {
    return {
      pizza,
    };
  },
  computed: {
    doughs() {
      return this.pizza.dough.map((element) => {
        return {
          id: element.id,
          name: element.name,
          className: this.getDoughClass(element),
        };
      });
    },
    sizes() {
      return this.pizza.sizes.map((element) => {
        return {
          id: element.id,
          name: element.name,
          className: this.getSizeClass(element),
        };
      });
    },
    ingredients() {
      return this.pizza.ingredients.map((element) => {
        return {
          id: element.id,
          name: element.name,
          className: this.getIngredientClass(element),
        };
      });
    },
  },
  methods: {
    getDoughClass(dough) {
      let startPostfixIndex = dough.image.lastIndexOf("-") + 1;
      let endPostfixIndex = dough.image.lastIndexOf(".");
      let postfix = dough.image.substring(startPostfixIndex, endPostfixIndex);
      return `dough__input--${postfix}`;
    },
    getSizeClass(size) {
      let postfix;
      switch (size.name) {
        case "23 см":
          postfix = "small";
          break;
        case "32 см":
          postfix = "normal";
          break;
        case "45 см":
          postfix = "big";
          break;
      }
      return `diameter__input--${postfix}`;
    },
    getIngredientClass(ingredient) {
      let startPostfixIndex = ingredient.image.lastIndexOf("/") + 1;
      let endPostfixIndex = ingredient.image.lastIndexOf(".");
      let postfix = ingredient.image.substring(
        startPostfixIndex,
        endPostfixIndex
      );
      return `filling--${postfix}`;
    },
  },
};
</script>

<style scoped></style>
