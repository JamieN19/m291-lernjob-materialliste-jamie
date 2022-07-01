<template>
  <img alt=" logo" src="../assets/logo.png">

  <div class="form">
    <lernpartner-select></lernpartner-select>
    <material-select></material-select>
    <label for="from">Von:</label>
    <input if="from" type="date" v-model="fromDate"/>
    <label fro="to">Bis:</label>
    <input it="to" type="date" v-model="toDate"/>
  </div>
  <div class="home-buttons">
    <button class="btn btn-primary" @click="doReserve">Reserve</button>
  </div>

</template>

<script>
// @ is an alias to /src
import LernpartnerSelect from '@/components/LernpartnerSelect.vue'
import MaterialSelect from '@/components/MaterialSelect.vue'
import { store } from '@/store'
export default {
  name: 'HomeView',
  data() {
    return {
      store,
      fromDate: null,
      toDate: null,
    };
  },
  components: {
    LernpartnerSelect,
    MaterialSelect,
  },
  methods: {
    async doReserve() {
      const payload = {
        StudentID: store.lernpartner_id,
        EquipmentID: store.equipment_id,
        Start: this.fromDate,
        End: this.toDate,
      };
      console.log(payload);
      const response = await fetch('https://projects.sbw.media/equipment_reservation', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify(payload)
      });
      const result = await response.json();
      alert(result.result);
    }
  },
}
</script>

<style lang=sass scoped>
  .form
    width: 80%
    display: grid
    grid-template-columns: 0.4fr 0.5fr
    gap: 1em

</style>
