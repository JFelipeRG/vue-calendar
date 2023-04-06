<script>
import { monthDictionary } from '../modules/monthDictionary'

export default {
  name: "CalendarMonth",
  props: {
    countrie: String,
    year: Number
  },
  data() {
    return {
      month: 0,
      weekly: ["Lun","Mar","Mie","Jue","Vie","Sab","Dom"]
    };
  },
  computed: {
    totalDays() {
      let totalDays

      if (this.month === 1) {
        totalDays = 28
      } else if (this.month >= 7) {
        totalDays = this.month % 2 === 0 ? 30 : 31
      } else {
        totalDays = this.month % 2 === 0 ? 31 : 30
      }

      return totalDays
    }
  },
  beforeMount() {
    const date = new Date()
    this.month = date.getMonth()
  },
  updated() {
    const days = document.querySelectorAll(".day")

    for (const day of days) {
     day.classList.remove("weekend")
    }

    this.firstDayWeekStart()
  },
  methods: {
    getMonthString(numberPosition) {
      return monthDictionary(numberPosition)
    },

    newMonth({ target }) {
      this.month = Number(target.value)
    },

    firstDayWeekStart() {
      const date = new Date(`${this.year}-${this.month + 1}-1`)
      const startCell = date.getDay()

      const days = document.querySelectorAll(".day")

      if (days[0]) days[0].style = `grid-column-start: ${startCell}`

      this.setWeekendDays(startCell)
    },

    setWeekendDays(actualPosition) {
      const days = document.querySelectorAll(".day")
      actualPosition = actualPosition === 0 ? 1 : actualPosition

      for(const day of days) {
        if(actualPosition === 6 || actualPosition === 7) day.classList.add("weekend")
        actualPosition = actualPosition === 7 ? 1 : ++actualPosition
      }
    }
  }
}
</script>

<template>
  <div class="calendar-container">
    <select name="months" @change="newMonth">
      <option v-for="n in 12" :value="n - 1" :selected="(n - 1) === this.month">
        {{ getMonthString(n - 1) }}
      </option>
    </select>

    <div class="days">
      <div class="week-days" v-for="(value, index) in weekly" :key="index">
        {{ value }}
      </div>
      <div class="day" v-for="n in totalDays" :key="n">
        {{ n }}
      </div>
    </div>
  </div>
</template>

<style scoped>
.calendar-container {
  display: flex;
  gap: 20px;
  flex-direction: column;
  align-items: center;
  height: 60%;
}

select {
  font-size: 1.3rem;
  padding: 5px;
  border: none;
  border-bottom: 2px solid white;
  outline: none;
}

.days {
  flex: 1;
  width: 90%;
  max-width: 500px;
  display: grid;
  grid-template-columns: repeat(7, 1fr);
  gap: 5px;
  grid-template-rows: fit-content(50%) auto;
}

.week-days {
  font-size: 1rem;
  text-align: center;
  background-color: black;
  padding: 5px 0;
}

.day {
  display: grid;
  place-content: center;
  background-color: #eee;
  color: #333;
  font-weight: 700;
}

.weekend {
  border-bottom: 2px solid red;
}
</style>
