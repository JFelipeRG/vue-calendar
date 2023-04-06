<script>
export default {
  name: "NavMenu",
  data() {
    return {
      actualYear: 0,
      countries: {
        "AN": "Andalucía",
        "AR": "Aragón",
        "AS": "Asturias",
        "CB": "Cantabria",
        "CE": "Ciudad de Ceuta",
        "CL": "Castilla y León",
        "CM": "Castile-La Mancha",
        "CN": "Islas Canarias",
        "CT": "Cataluña",
        "EX": "Extremadura",
        "GA": "Galicia",
        "IB": "Illes Balears",
        "MC": "Murcia Region",
        "MD": "Comunidad de Madrid",
        "ML": "Ciudad de Melilla",
        "NC": "Comunidad Foral de Navarra",
        "PV": "País Vasco",
        "RI": "La Rioja",
        "VC": "Comunitat Valenciana"
      }
    }
  },
  computed: {
    getActualYear() {
      const selectedYear = this.actualYear
      this.$emit("changeYear", selectedYear)

      return this.actualYear
    }
  },
  beforeMount() {
    // Obtain actual year
    const date = new Date()
    this.actualYear = date.getFullYear()
  },
  methods: {
    newCountrie({ target }) {
      const selectedCountrie = target.value

      this.$emit("changeCountrie", selectedCountrie)
    }
  }
}
</script>

<template>
  <div class="container">
    <nav>
      <div class="year">
        <span @click="--this.actualYear">⬅</span>
        {{ getActualYear }}
        <span @click="++this.actualYear">➡</span>
      </div>
      <select @change="newCountrie($event)" name="countries" class="countries">
        <option value="none">-- Selecciona una opción --</option>
        <option v-for="(value, key, index) in countries" :value="key" :key="index">
          {{ value }}
        </option>
      </select>
    </nav>
  </div>
</template>

<style scoped>
nav {
  margin: 1.2rem 10px;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 20px;
}

.year {
  font-size: 1.8rem;
  user-select: none;
}

.year span {
  cursor: pointer;
}

.countries {
  font-size: 1.3rem;
  padding: 5px;
  border: none;
  outline: none;
}
</style>
