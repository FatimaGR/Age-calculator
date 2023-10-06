<script setup>
import { ref } from "vue";
const years = ref("--");
const months = ref("--");
const days = ref("--");

const day = ref("");
const month = ref("");
const year = ref("");

const today = new Date();
const todayDay = today.getDate();
const todayMonth = today.getMonth() + 1;
const todayYear = today.getFullYear();

// Functions
// Calculate years
const calculateYears = (day, month, year) => {
  if (todayMonth < month){
    years.value = todayYear - year - 1
  } else if (todayMonth == month){
    if (todayDay >= day){
      years.value = todayYear - year;
    } else {
      years.value = todayYear - year - 1
    }
  } else {
    years.value = todayYear - year
  }
}
// Calculate months
const calculateMonths = (day, month) => {
  if (todayMonth < month){
    months.value = 11 - (month - todayMonth)
    if (todayDay >= day){
      months.value += 1
    }
  } else if (todayMonth == month){
    months.value = 11
    if (todayDay >= day){
      months.value = 0
    }
  } else {
    months.value = todayMonth - month
    if (todayDay < day){
      months.value -= 1
    }
  }
}
// Calculate days
const calculateDays = (day) => {
  const numDays = new Date(todayYear, todayMonth, 0).getDate();
  (todayDay >= day) ? days.value = todayDay - day : days.value = numDays - (day - todayDay);
}

const submit = () => {
  calculateYears(day.value, month.value, year.value);
  calculateMonths(day.value, month.value);
  calculateDays(day.value)
}
</script>

<template>
  <main>
    <form @submit.prevent="submit">
      <div class="inputs">
        <p class="option">
          <label for="day">DAY</label>
          <input type="text" id="day" placeholder="DD" v-model="day"/>
        </p>
    
        <p class="option">
          <label for="month">MONTH</label>
          <input type="text" id="month" placeholder="MM" v-model="month"/>
        </p>
    
        <p class="option">
          <label for="year">YEAR</label>
          <input type="text" id="year" placeholder="YYYY" v-model="year"/>
        </p>
      </div>

      <div class="container">
        <div class="line"></div>
        <button @click="incremento">
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
  letter-spacing: -1px;
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
  width: 100%;
  box-sizing: border-box;
  font-weight: 700;
  cursor: pointer;
  letter-spacing: 1px;
}
input:hover, input:focus{
  outline: none;
  border-color: var(--purple);
}
form{
  display: flex;
  flex-direction: column;
  align-items: flex-start;
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
  box-sizing: border-box;
}
main{
  height: auto;
  width: auto;
  padding: 30px;
  box-sizing: border-box;
  background-color: var(--white);
  border-radius: 20px;
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
  cursor: pointer;
}
button:hover{
  background-color: var(--off-black);
}
img{
  width: 30px;
  height: 30px;
}
.results{
  line-height: 1;
}
@media (min-width: 700px){
  h1{
    font-size: 80px;
  }
  main{
    width: 650px;
    border-bottom-right-radius: 145px;
  }
  input{
    max-width: 120px;
  }
  .container{
    justify-content: flex-end;
    height: 45px;
  }
  form{
    gap: 30px;
  }
  button{
    bottom: 25%;
  }
}
</style>
