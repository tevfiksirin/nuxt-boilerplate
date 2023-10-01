<template>
  <div class="navbar bg-base-100">
    <div class="navbar-start">
      <div class="dropdown">
        <label tabindex="0" class="btn btn-ghost lg:hidden">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="h-5 w-5"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M4 6h16M4 12h8m-8 6h16"
            />
          </svg>
        </label>
        <ul
          tabindex="0"
          class="menu dropdown-content rounded-box menu-sm z-[1] mt-3 w-52 bg-base-100 p-2 shadow"
        >
          <li><a>Item 1</a></li>
          <li>
            <a>Parent</a>
            <ul class="p-2">
              <li><a>Submenu 1</a></li>
              <li><a>Submenu 2</a></li>
            </ul>
          </li>
          <li><a>Item 3</a></li>
        </ul>
      </div>
      <a class="btn btn-ghost text-xl normal-case">daisyUI</a>
    </div>
    <div class="navbar-center hidden lg:flex">
      <ul class="menu menu-horizontal px-1">
        <li><a>Item 1</a></li>
        <li tabindex="0">
          <details>
            <summary>Parent</summary>
            <ul class="p-2">
              <li><a>Submenu 1</a></li>
              <li><a>Submenu 2</a></li>
            </ul>
          </details>
        </li>
        <li><a>Item 3</a></li>
      </ul>
    </div>
    <div class="navbar-end">
      <form>
        <label for="languages">
          <Icon name="prime:language" size="1.5em" />
        </label>
        <select
          id="languages"
          v-model="$i18n.locale"
          class="bg-transparent"
          @change="toggleLocale"
        >
          <option
            v-for="language in $i18n.availableLocales"
            :key="language"
            :value="language"
            :selected="$i18n.locale === language"
            class="dark:bg-slate-800"
          >
            {{ $t("locale." + language) }}
          </option>
        </select>
      </form>
    </div>
  </div>
</template>

<script setup>
const { locale } = useI18n();

// update local storage upon language change
const toggleLocale = () => {
  localStorage.setItem("nuxt-lang", locale.value);
};

// check for stored language on initial load.
onMounted(() => {
  const storedLanguage = localStorage.getItem("nuxt-lang");
  if (storedLanguage) {
    locale.value = storedLanguage;
  }
});
</script>
<style></style>
