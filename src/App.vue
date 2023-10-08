<script setup>
import { ref } from "vue";
// Results
const years = ref("--");
const months = ref("--");
const days = ref("--");
// User data
const day = ref("");
const month = ref("");
const year = ref("");
// Actual date
const today = new Date();
const todayDay = today.getDate();
const todayMonth = today.getMonth() + 1;
const todayYear = today.getFullYear();
// Errors
const errorMessage = ref("")
const errorRequired = ref(false)
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
const numDay = (theYear, theMonth) => {
  return new Date(theYear, theMonth, 0).getDate();
}
const calculateDays = (day) => {
  if (todayDay >= day){
    days.value = todayDay - day
  } else {
    days.value = numDay(todayMonth, todayYear) - (day - todayDay)
  }
}
// Validates
// Validate day
let dayValidated = ref(true)
const validatingDay = () => {
  dayValidated.value = true
  if (day.value > numDay(month.value, year.value) || 1 > day.value){
    dayValidated.value = false
  }
}
// Validate month
let monthValidated = ref(true)
const validatingMonth = () => {
  monthValidated.value = true
  if (month.value > 12 || 1 > month.value){
    monthValidated.value = false
  }
}
// Validate year
let yearValidated = ref(true)
const validatingYear = () => {
  yearValidated.value = true
  if (year.value.length <= 0 || year.value > todayYear){
    yearValidated.value = false
  }
}
// Submit
const submit = () => {
  validatingDay()
  validatingMonth()
  validatingYear()

  if(day.value.length == 0 || month.value.length == 0 || year.value.length == 0){
    errorMessage.value = "The field is required"
    errorRequired.value = true
  } else if (!dayValidated.value || !monthValidated.value || !yearValidated.value) {
    return ""
  } else {
    calculateYears(day.value, month.value, year.value);
    calculateMonths(day.value, month.value);
    calculateDays(day.value)
  }
}
</script>

<template>
  <main>
    <form @submit.prevent="submit">
      <div class="inputs">
        <p class="option">
          <label for="day" :class="dayValidated ? '' : 'message-error'">DAY</label>
          <input type="text" id="day" placeholder="DD" v-model="day" :class="dayValidated ? '' : 'input-invalid'"/>
          <p v-if="day.length >= 1 & (day>numDay(month,year) || 1>day)" class="message-error">
            Must be a valid date
          </p>
          <p v-if="day.length == 0" class="message-error">{{ errorMessage }}</p>
        </p>
    
        <p class="option">
          <label for="month" :class="monthValidated ? '' : 'message-error'">MONTH</label>
          <input type="text" id="month" placeholder="MM" v-model="month" :class="monthValidated ? '' : 'input-invalid'"/>
          <p v-if="month.length >= 1 & (month>12 || 1>month)" class="message-error">
            Must be a valid month
          </p>
          <p v-if="month.length == 0" class="message-error">{{ errorMessage }}</p>
        </p>
    
        <p class="option">
          <label for="year" :class="yearValidated ? '' : 'message-error'">YEAR</label>
          <input type="text" id="year" placeholder="YYYY" v-model="year" :class="yearValidated ? '' : 'input-invalid'"/>
          <p v-if="year.length >= 1 & year>todayYear" class="message-error">
            Must be in the past
          </p>
          <p v-if="year.length == 0" class="message-error">{{ errorMessage }}</p>
        </p>
      </div>

      <div class="container">
        <div class="line"></div>
        <button>
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
