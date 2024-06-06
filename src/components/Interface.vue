<script setup>
import { onMounted, reactive } from "vue";
import axios from "axios";
import CharacterCards from "./_characterCards.vue";
import Pagination from "./Pagination.vue";

const state = reactive({
  showName: false,
  showStatus: false,
  filterName: "",
  filterStatus: "",
  characterResult: [],
  currentPageResult: 1,
  nextPageUrlResult: "",
  prevPageUrlResult: "",
  pagesResult: 0,
});

const filter = async (name, status) => {
  try {
    const response = await axios.get(
      `https://rickandmortyapi.com/api/character/?name=${name}&status=${status}`
    );
    state.characterResult = response.data.results;
    state.nextPageUrlResult = response.data.info.next;
    state.prevPageUrlResult = response.data.info.prev;
    state.pagesResult = response.data.info.pages;
    state.currentPageResult = 1;
  } catch (error) {
    console.error("Error loading data:", error);
  }
  state.filterName = "";
  state.filterStatus = "";
};

const getCharacters = async (url, int) => {
  try {
    const response = await axios.get(url);
    state.characterResult = response.data.results;
    state.nextPageUrlResult = response.data.info.next;
    state.prevPageUrlResult = response.data.info.prev;
    state.pagesResult = response.data.info.pages;

    if (state.nextPageUrlResult) {
      state.currentPageResult += int;
    } else {
      state.currentPageResult += int;
    }
  } catch (error) {
    console.error("Error loading data:", error);
  }
};

const reset = () => {
  filter("", "");
};

onMounted(() => {
  filter("", "");
});
</script>

<template>
  <main>
    <div class="background">
      <img class="img" src="../assets/background.jpg" />
    </div>

    <div class="filtersForm">
      <label class="label">Filters</label>

      <div class="filterBySmth">
        <label class="name">Name</label>
        <svg
          class="svg"
          xmlns="http://www.w3.org/2000/svg"
          width="25"
          height="25"
          viewBox="0 0 24 24"
        >
          <path
            fill="#40b5cb"
            fill-rule="evenodd"
            d="M12 1C5.925 1 1 5.925 1 12s4.925 11 11 11s11-4.925 11-11S18.075 1 12 1M8.707 9.793a1 1 0 0 0-1.414 1.414l4 4a1 1 0 0 0 1.414 0l4-4a1 1 0 0 0-1.414-1.414L12 13.086z"
            clip-rule="evenodd"
            @click="state.showName = !state.showName"
          />
        </svg>
      </div>

      <input type="text" v-if="state.showName" v-model="state.filterName" />

      <div class="filterBySmth">
        <label class="name">Status</label>
        <svg
          class="svg"
          xmlns="http://www.w3.org/2000/svg"
          width="25"
          height="25"
          viewBox="0 0 24 24"
        >
          <path
            fill="#40b5cb"
            fill-rule="evenodd"
            d="M12 1C5.925 1 1 5.925 1 12s4.925 11 11 11s11-4.925 11-11S18.075 1 12 1M8.707 9.793a1 1 0 0 0-1.414 1.414l4 4a1 1 0 0 0 1.414 0l4-4a1 1 0 0 0-1.414-1.414L12 13.086z"
            clip-rule="evenodd"
            @click="state.showStatus = !state.showStatus"
          />
        </svg>
      </div>

      <select v-model="state.filterStatus" v-if="state.showStatus">
        <option disabled value="">Choose one of the options</option>
        <option>Alive</option>
        <option>Dead</option>
        <option>Unknown</option>
      </select>

      <div class="buttonBox">
        <button
          class="submit"
          v-if="state.showStatus || state.showName"
          @click="reset"
        >
          Reset
        </button>
        <button
          class="submit"
          v-if="state.showStatus || state.showName"
          @click="filter(state.filterName, state.filterStatus)"
        >
          Сonfirm
        </button>
      </div>
    </div>

    <CharacterCards :characterResult="state.characterResult" />
    <Pagination
      :currentPage="state.currentPageResult"
      :prevPageUrl="state.prevPageUrlResult"
      :nextPageUrl="state.nextPageUrlResult"
      :pages="state.pagesResult"
      @getCharacters="getCharacters"
    />
  </main>
</template>

<style>
.background {
  position: fixed;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  background-color: black;
}
.img {
  position: fixed;
  left: 15px;
  bottom: 0;
  width: 620px;
}

.filtersForm {
  display: flex;
  flex-direction: column;
  align-items: center;
  position: fixed;
  left: 40px;
  top: 150px;
  height: 500px;
  width: 340px;
}
.label {
  margin-bottom: 15px;
  font-size: 2.8rem;
}
.filterBySmth {
  display: flex;
  align-items: center;
  height: 35px;
  align-self: stretch;
  letter-spacing: 1.5px;
  margin-bottom: 15px;
}
.name {
  font-size: 2.2rem;
  margin-left: 15px;
  text-shadow: 2px 2px 3px rgb(192, 223, 64);
  -webkit-text-stroke: 1.5px rgb(24, 72, 84) !important;
}
input {
  width: 95%;
  height: 40px;
  padding-left: 10px;
  margin-bottom: 20px;
  font-size: large;
  border-radius: 10px;
  letter-spacing: 1.5px;
  background-color: rgb(115, 210, 226);
}
select {
  width: 100%;
  height: 50px;
  padding: 3px 1px 3px 2px;
  font-size: large;
  border-radius: 10px;
  letter-spacing: 1.5px;
  background-color: rgb(115, 210, 226);
}
input:focus,
select:focus {
  border: 2px solid rgb(18, 53, 62);
  box-shadow: 2px 2px 10px rgb(192, 223, 64);
  outline: none;
}
option {
  font-size: large;
  border-radius: 15px;
}
.svg {
  margin-left: 15px;
}
path:hover {
  fill: rgb(115, 210, 226);
}
path:active {
  fill: rgb(28, 124, 141);
}
.buttonBox {
  display: flex;
  align-items: center;
}
.submit {
  width: 120px;
  height: 45px;
  margin: 30px 15px 0 15px;
  border-radius: 30px;
  background-color: rgb(192, 223, 64);
  letter-spacing: 1.5px;
  font-size: large;
}
.submit:hover {
  background-color: rgb(224, 245, 139);
}
.submit:active {
  background-color: rgb(156, 187, 35);
}
/* .v-enter-active,
.v-leave-active {
  transition: opacity 0.5s ease;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
} */
</style>
