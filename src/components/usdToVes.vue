<template>
  <div class="h-100 d-flex flex-column justify-content-center">
    <div class="container">
      <div class="row">
        <div
          class="
            col-12 col-md-5
            d-flex
            justify-content-center
            align-items-center
          "
        >
          <div
            class="currency-container d-flex flex-column justify-content-center"
          >
            <span>1.00</span>
            <span class="currency-name d-block">USD</span>
          </div>
        </div>
        <div
          class="
            col-12 col-md-2
            d-flex
            align-items-center
            justify-content-center
          "
        >
          <img src="../assets/exchange-arrow.svg" class="exchange-icon" />
        </div>
        <div
          class="
            col-12 col-md-5
            d-flex
            justify-content-center
            align-items-center
          "
        >
          <div
            class="currency-container d-flex flex-column justify-content-center"
          >
            <span>{{ ves }}</span>
            <span class="currency-name d-block">VES</span>
          </div>
        </div>
      </div>
    </div>
    <footer class="text-center p-3 fixed-bottom">
      <span
        >Information brought to you by
        <a
          href="https://openexchangerates.org/"
          style="color: #e74c3c"
          target="_blank"
          >https://openexchangerates.org/</a
        ></span
      >
    </footer>
  </div>
</template>

<script setup>
import axios from "axios";
import { ref, onMounted } from "vue";

const ves = ref("...");

const getData = async function () {
  try {
    const response = await axios(
      "https://openexchangerates.org/api/latest.json?app_id=f3e98d56e1884e46ad48aa8cda13c977&base=USD&symbols=VES"
    );
    ves.value = response.data.rates.VES.toFixed(2);
    console.log(ves.value);
  } catch (error) {
    console.log(error);
  }
};

onMounted(() => {
  console.log(ves.value);
  getData();
});
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Montserrat:wght@100&display=swap");

.currency-container {
  font-family: "Montserrat", sans-serif;
  color: white;
  background-color: #e74c3c;
  height: 300px !important;
  width: 300px !important;
  border-radius: 50%;
  text-align: center;
  font-size: 5em;
  cursor: default;
}

.currency-name {
  font-size: 1.4rem;
  opacity: 0.7;
}

.exchange-icon {
  width: 100px;
}

/* RESPONSIVE RULES */

@media screen and (max-width: 768px) {
  .currency-container {
    height: 200px !important;
    width: 200px !important;
    font-size: 3em;
  }
}
</style>