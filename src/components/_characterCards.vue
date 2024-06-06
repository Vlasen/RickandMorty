<script setup>
defineProps(["characterResult"]);
</script>

<template>
  <div class="content">
    <div
      class="characterCards"
      id="characterCards"
      v-for="character in characterResult"
      :key="character.id"
    >
      <img class="image" :src="character.image" :alt="character.name" />

      <div class="charInfo">
        <div class="CharName">{{ character.name }}</div>

        <div class="statusBox">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="20"
            height="20"
            viewBox="0 0 32 32"
          >
            <circle
              v-if="character.status == 'Alive'"
              cx="16"
              cy="16"
              r="8"
              fill="#009e03"
            />
            <circle
              v-if="character.status == 'Dead'"
              cx="16"
              cy="16"
              r="8"
              fill="#990000"
            />
            <circle
              v-if="character.status == 'unknown'"
              cx="16"
              cy="16"
              r="8"
              fill="#bfbfbf"
            />
          </svg>
          <div class="CharStatus">
            {{ character.status }} - {{ character.species }}
          </div>
        </div>

        <div class="CharGender">
          {{ character.gender }}

          <div class="CharLocationBox">
            <div class="CharLocationLabel">Location:</div>
            <div class="CharLocation">{{ character.location.name }}</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style>
.content {
  position: fixed;
  left: 390px;
  top: 130px;
  width: auto;
  height: 75%;
  padding: 20px;
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  overflow-y: scroll;
}
.characterCards {
  width: 510px;
  height: 200px;
  margin: 15px;
  background-color: rgb(42, 42, 42);
  border-radius: 8px;
  overflow: hidden;
  text-shadow: none;
  -webkit-text-stroke: 1.5px rgb(18, 53, 62);
  font-size: x-large;
  font-family: fantasy;
  -webkit-text-stroke: 1px rgb(18, 53, 62);
  letter-spacing: 1px;
}
.image {
  float: left;
  height: 100%;
  margin-right: 15px;
}
.charInfo {
  position: relative;
  float: center;
  display: block;
  height: 100%;
}
.CharName {
  line-height: 25px;
  margin: 10px 0 5px 0;
}
.statusBox {
  display: flex;
  margin: 10px 0 0 5px;
}
.CharStatus {
  font-size: medium;
  font-weight: 100;
  font-family: fantasy;
  margin-left: 5px;
  color: rgb(64, 181, 203);
  -webkit-text-stroke: 0px;
  letter-spacing: 0;
}
.CharGender {
  margin-top: 7px;
  font-size: 1.2rem;
}
.CharLocationBox {
  position: absolute;
  left: 215px;
  bottom: 15px;
  margin-right: 3px;
}
.CharLocationLabel {
  font-size: 1.2rem;
  color: rgb(92, 126, 131);
  margin-top: 8px;
}
.CharLocation {
  font-size: medium;
  font-size: 1.3rem;
}
</style>
