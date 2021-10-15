<template>
  <div class="home_body">
    <h1>Please fill the form with the hero information</h1>

    <form>
      <div class="form_container">
        <div>
          <label for="stamina" class="form_input__label">Heroe Stamina</label>
          <input type="number" :value="form.stamina" @input="$set(form, 'stamina', Number($event.target.value))" id="stamina" class="form_input" />
        </div>

        <div>
          <span class="form_input__label">Energy extra gained by Battery Skill</span>

          <div class="form_input__radio">
            <input type="radio" value="0" v-model.number="form.energyByMinute.batterySkill" name="skill" checked id="withoutSkill" />
            <label for="withoutSkill">0/m</label>
            <input type="radio" value="0.5" v-model.number="form.energyByMinute.batterySkill" name="skill" id="withSkill" />
            <label for="withSkill">0.5/m</label>
          </div>
        </div>

        <div>
          <span class="form_input__label">Energy extra gained by House</span>

          <div class="form_input__radio form_input__radio--house">
            <span class="form_subtitle">Select your house</span>
            <div>
              <input value="0.5" v-model.number="form.energyByMinute.house" type="radio" name="house" checked id="withoutHouse" />
              <label for="withoutHouse">No house (0.5/m)</label>
            </div>
            <div>
              <input value="2" v-model.number="form.energyByMinute.house" type="radio" name="house" checked id="tinyHouse" />
              <label for="tinyHouse">Tiny House (2/m)</label>
            </div>
            <div>
              <input value="5" v-model.number="form.energyByMinute.house" type="radio" name="house" checked id="miniHouse" />
              <label for="miniHouse">Mini House (5/m)</label>
            </div>
            <div>
              <input value="8" v-model.number="form.energyByMinute.house" type="radio" name="house" checked id="luxHouse" />
              <label for="luxHouse">Lux House (8/m)</label>
            </div>
            <div>
              <input value="11" v-model.number="form.energyByMinute.house" type="radio" name="house" checked id="penHouse" />
              <label for="penHouse">Pen House (11/m)</label>
            </div>
            <div>
              <input value="14" v-model.number="form.energyByMinute.house" type="radio" name="house" checked id="villa" />
              <label for="villa">Villa (14/m)</label>
            </div>
            <div>
              <input value="17" v-model.number="form.energyByMinute.house" type="radio" name="house" checked id="superVilla" />
              <label for="superVilla">Super Villa (17/m)</label>
            </div>
          </div>
        </div>

        <div class="form_total">
          Time needed: 
        </div>

          <span class="form_total--number">
            {{ totalMinsNeeded }} mins / {{ totalHoursNeeded }} hours
          </span>
        </div>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      form: {
        stamina: 1,
        energyByMinute: {
          batterySkill: 0,
          house: 0.5,
        }
      }
    }
  },
  computed: {
    totalMinsNeeded() {
      return (this.totalStamina / this.totalEnergyByMinute).toFixed();
    },
    totalEnergyByMinute() {
      const {
        batterySkill,
        house,
      } = this.form.energyByMinute;

      return batterySkill + house;
    },
    totalStamina() {
      return this.form.stamina * 50;
    },
    totalHoursNeeded() {
      return (this.totalMinsNeeded / 60).toFixed(2);
    }
  },
}
</script>

<style>
.home_body {
  width: 50%;
  margin: 0 auto;
  font-family: Georgia, 'Times New Roman', Times, serif;
}

@media (max-width: 768px) {
  .home_body {
    width: 90%;
  }  
}

.form_input {
  width: 100%;
  border-radius: 5px;
  padding: 10px;
  font-size: 1.4rem;
  font-family:'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif
}

.form_input__label {
  display: block;
  text-align: left;
}

.form_container {
  display: grid;
  grid: 1fr;
  gap: 1.5rem;
}

.form_input__radio {
  text-align: left;
}

.form_input__radio--house {
  display: grid;
  gap: 1rem;
}

.form_subtitle {
  display: block;
  font-size: 0.9rem;
  margin: 0.5rem 0rem;
  opacity: 0.5;
}

.form_total {
  font-size: 4rem;
  background: #3B82F6;
  color: white;
  border-radius: 10px;
}

.form_total--number {
  background: #3B82F6;
  color: white;
  border-radius: 10px;
}
</style>
