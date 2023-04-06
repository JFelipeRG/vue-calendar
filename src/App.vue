<script>
import NavMenu from './components/NavMenu.vue';
import CalendarMonth from './components/CalendarMonth.vue';

export default {
  components: {
    NavMenu, CalendarMonth
  },
  data() {
    return {
      countrie: "",
      year: 0
    }
  },
  methods : {
    setNewCountrie(selectedCountrie) {
      this.countrie = selectedCountrie
    },
    setNewYear(selectedYear) {
      this.year = selectedYear
    }
  }
}
</script>

<template>
  <div class="container">
    <div>
      <h1>Calendario</h1>
      <NavMenu @changeCountrie="setNewCountrie" @changeYear="setNewYear"></NavMenu>
    </div>
    <CalendarMonth :year="year" :countrie="countrie"></CalendarMonth>
  </div>
</template>

<style scoped>
.container {
  height: 100%;
}

h1 {
  font-size: 3rem;
  text-align: center;
}
</style>
