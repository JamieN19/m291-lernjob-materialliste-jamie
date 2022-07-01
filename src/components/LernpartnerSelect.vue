<script setup>
import {store} from '@/store';
</script>
<template>
  <label for="lernpartner">Lernpartner</label>
  <select id="lernpartner" v-model="store.lernpartner_id">
    <option v-for="lp in lernpartner" :value="lp.ID" :key="lp.ID">
      {{lp.Fullname}}
    </option>
  </select>
</template>

<script>

export default {
  name: "LernpartnerSelect",
  data() {
    return{
      lernpartner: [],
      lernpartner_id: 0
    };
  },
  created() {
    this.getLernpartner();
  },
  methods: {
    async getLernpartner() {
      const response = await fetch("https://projects.sbw.media/student");
      this.lernpartner = await response.json();
    }
  },
};
</script>

<style>
</style>