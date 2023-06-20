<script setup>
let years = "--";
let months = "--";
let days = "--";
</script>

<template>
  <main>
    <form action="">
      <div class="inputs">
        <p class="option">
          <label for="day">DAY</label>
          <input type="text" id="day" placeholder="DD"/>
        </p>
    
        <p class="option">
          <label for="month">MONTH</label>
          <input type="text" id="month" placeholder="MM"/>
        </p>
    
        <p class="option">
          <label for="year">YEAR</label>
          <input type="text" id="year" placeholder="YYYY"/>
        </p>
      </div>

      <div class="container">
        <div class="line"></div>
        <button type="submit">
          <img src="./assets/images/icon-arrow.svg"/>
        </button>
      </div>
    </form>

    <section class="results">
      <h1><a>{{ years }}</a> years</h1>
      <h1><a>{{ months }}</a> months</h1>
      <h1><a>{{ days }}</a> days</h1>
    </section>
  </main>
</template>

<style scoped>
h1{
  margin: 0;
  padding: 0;
  font-size: 55px;
  font-style: italic;
  color: var(--off-black);
}
a { 
  color: var(--purple); 
}
label{
  font-size: 14px;
  color: var(--smokey-grey);
  letter-spacing: 2px;
  font-weight: 600;
}
input{
  font-size: 20px;
  color: var(--off-black);
  border: 1px solid var(--light-grey);
  border-radius: 7px;
  padding: 16px;
  width: 90px;
  box-sizing: border-box;
  font-weight: 700;
}
form{
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 100%;
  box-sizing: border-box;
  gap: 60px;
}
.option{
  display: flex;
  flex-direction: column;
  justify-content: left;
  gap: 3px;
}
.inputs{
  display: flex;
  justify-content: space-evenly;
  max-width: 100%;
  gap: 20px;
}
main{
  height: auto;
  width: 375px;
  padding: 30px;
  box-sizing: border-box;
  background-color: var(--white);
  border-radius: 25px;
  border-bottom-right-radius: 85px;
}
.line{
  display: flex;
  height: 2px;
  width: 100%;
  background-color: var(--light-grey);
}
.container{
  display: flex;
  height: 70px;
  width: 100%;
  position: relative;
  justify-content: center;
}
button{
  border: none;
  border-radius: 100%;
  background-color: var(--purple);
  padding: 25px;
  box-sizing: border-box;
  max-width: 70px;
  max-height: 70px;
  display: flex;
  justify-content: center;
  align-items: center;
  position: absolute;
  bottom: 50%;
}
img{
  width: 30px;
  height: 30px;
}
</style>
