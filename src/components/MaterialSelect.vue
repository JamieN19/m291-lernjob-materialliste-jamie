<template>
  <label for="material">Gerät</label>
  <select id="material">
    <option v-for="material in materials" :key="material.id">
      {{material.Name}}
    </option>
  </select>
</template>

<script>
export default {
  name: "MaterialSelect",
  data() {
      return{
        materials: []
      }
  },
  created() {
    this.getMaterials();
  },
  methods: {
    async getMaterials(){
      const response = await fetch("https://projects.sbw.media/equipmentview");
      this.materials = await response.json();
    }
  },
};
</script>

<style>
</style>