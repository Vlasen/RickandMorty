<template>
    <header>
      <img height="100"
        src="../assets/logo.png" 
        class="logo" 
      />
      <span>List of charachters</span>
    </header>
</template>
  
<style>
  header {
    position: fixed;
    width: 100%;
    left: 0;
    top: 0;
    display: flex;
    align-items: center;
    font: 1.0rem Brush Script MT, Brush Script Std;
    font-family: fantasy;
    height: 115px;
    padding: 5px;
    background: black;
    z-index: 1;
  }
  span {
    color: rgb(64, 181, 203);
    margin: 15px 150px 0 auto;
    line-height: 50px;
    font-size: 3.8rem;
    text-shadow: 4px 4px 5px rgb(192, 223, 64);
    -webkit-text-stroke: 1.5px rgb(18, 53, 62);
  }
  .logo {
    margin: 15px 50px 0px 300px;
  }
</style>