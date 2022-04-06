<template>
  <div>
    <div class="title">
      <h1>Wordle</h1>
    </div>
    <Nuxt />
  </div>
</template>

<style>
* {
  color: #fff;
  font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
}
input{
  color: black
}

body{
  background-color: #121213;
  height: 90vh;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
}

.title{
  text-align: center;
  width: 510px;
  border-bottom: solid 1px #3A3A3C;
}
</style>