<script setup>
defineProps({
  currentPage: Number,
  prevPageUrl: String,
  nextPageUrl: String,
  pages: Number,
});

const emit = defineEmits(["getCharacters"]);

const getCharacters = (url, int) => {
  emit("getCharacters", url, int);
};
</script>

<template>
  <div class="paginationMain">
    <div class="pagination">
      <button
        class="pagButton"
        @click="getCharacters(prevPageUrl, -1)"
        :disabled="!prevPageUrl"
      >
        Previous
      </button>

      <span class="pagSpan">{{ currentPage }}</span>

      <img
        class="pagImg"
        v-if="currentPage != pages"
        src="../assets/horizontal-dots.svg"
        alt="logo"
      />

      <span class="pagSpan" v-if="currentPage != pages"
        >{{ pages }}

      </span>

      <button
        class="pagButton"
        @click="getCharacters(nextPageUrl, 1)"
        :disabled="!nextPageUrl"
      >
        Next
      </button>
    </div>
  </div>
</template>

<style>
.paginationMain {
  position: fixed;
  width: 81%;
  left: 390px;
  bottom: 12px;
  display: flex;
  justify-content: center;
  background: black;
}
.pagination {
  display: flex;
  align-items: center;
}
.pagSpan {
  font-size: 2.5rem;
  margin: 0;
  padding: 0 10px 0 10px;
  text-shadow: 3px 3px 4px rgb(192, 223, 64);
}
.pagButton {
  font-size: large;
  margin: 0 30px 0 30px;
  width: 120px;
  height: 45px;
  border-radius: 30px;
  background-color: rgb(192, 223, 64);
  letter-spacing: 1.5px;
}
.pagButton:hover {
  background-color: rgb(224, 245, 139);
}
.pagButton:active {
  background-color: rgb(156, 187, 35);
}
.pagButton:disabled {
  background-color: rgb(91, 91, 84);
}
.pagImg {
  margin: 30px 20px 0 20px;
}
</style>
