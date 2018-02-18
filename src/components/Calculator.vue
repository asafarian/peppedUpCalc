<template>
  <div class="hello" align="left">
    <h2>Kalorienbedarfsrechner  </h2>
    <h3>
      Grundumsatz
    </h3>
    <div align="left">
      Geschlecht:
      <input id=gm type="radio" v-model="gender" value="w" /> weiblich /
      <input id=gw type="radio" v-model="gender" value="m" /> mänlich

      <p>
        Alter
        <input v-model="age" size=2>
      </p>
      <p>
        Größe
        <input v-model="height" size=3> cm
      </p>
      <p>
        Gewicht
        <input v-model="weight" size=3>
      </p>
      <p>
        Dein Grundumsatz beträgt
        <input v-model="calc_gu" size=7 :readonly="true">
      </p>
    </div>
    <h3>
      Leistungsumsatz
    </h3>
    <p>
      Wie verbringst du deinen Tag ? (Die Summe muss 24 ergeben)
    </p>
    <p>
      Schlaf (0.95)
      <input v-model="ac_sleeping" size=2> h
    </p>
    <p>
      nur sitzen und liegen (1.2)
      <input v-model="ac_sit_lay" size=2> h
    </p>
    <p>
      sitzend / kaum aktiv (1.4)
      <input v-model="ac_sit_low" size=2> h
    </p>
    <p>
      sitzend / zeitweilige gehend und stehend (1.6)
      <input v-model="ac_sit_go" size=2> h
    </p>
    <p>
      hauptsächlich stehend / gehend (1.8)
      <input v-model="ac_sit_stand" size=2> h
    </p>
    <p>
      anstrengende Arbeit / Sportliche Aktivität (2.0)
      <input v-model="ac_sport" size=2> h
    </p>
    <p>
      Summe Stunden
      <input v-model="calc_hours" size=2 :readonly="true">
    </p>

    <h2>
      Dein Gesamtkalorienbedarf beträgt:
      <input v-model="calc_lu" size=6 :readonly="true"> kcal
    </h2>
  </div>
</template>

<script>
export default {
  name: 'Calculator',
  data () {
    return {
      gender: '',
      age: null,
      height: null,
      weight: null,
      ac_sleeping: null,
      ac_sit_lay: null,
      ac_sit_low: null,
      ac_sit_go: null,
      ac_sit_stand: null,
      ac_sport: null
    }
  },
  computed: {
    calc_gu () {
      if (this.weight > 0 && this.age > 0 && this.height > 0) {
        if (this.gender === 'm') {
          return Math.round((66 + (13.8 * this.weight) + (5 * this.height) - (6.8 * this.age)))
        } else if (this.gender === 'w') {
          return Math.round(655 + (9.5 * this.weight) + (1.9 * this.height) - (4.7 * this.age))
        }
      }
      return null
    },
    calc_hours () {
      return (1 * this.ac_sleeping) + (1 * this.ac_sit_lay) + (1 * this.ac_sit_low) + (1 * this.ac_sit_go) + (1 * this.ac_sit_stand) + (1 * this.ac_sport)
    },
    calc_lu () {
      if (this.calc_hours === 24) {
        return Math.round(this.calc_gu * (((0.95 * this.ac_sleeping) + (1.2 * this.ac_sit_lay) + (1.4 * this.ac_sit_low) + (1.6 * this.ac_sit_go) + (1.8 * this.ac_sit_stand) + (2.0 * this.ac_sport)) / 24))
      } else {
        return 0
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
