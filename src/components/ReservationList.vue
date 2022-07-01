<template>
  <table>
    <thead>
      <tr>
        <th>Lernpartner</th>
        <th>Material</th>
        <th>Von</th>
        <th>Bis</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="reservation in reservations" :key="reservation.ID" :data-id="reservation.ID">
      <td>{{ reservation.Fullname }}</td>
      <td>{{ reservation.Equipment }}</td>
      <td>{{ reservation.Start }}</td>
      <td>{{ reservation.End }}</td>
      <button @click="deleteReservation()">Delete</button>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  name: "ReservationList",
  data() {
    return {
      reservations: []
    };
  },
  created() {
    this.getReservations();
  },
  methods: {
    async getReservations(){
      const response = await fetch(
        "https://projects.sbw.media/reservationview"
      );
      this.reservations = await response.json();
    },


    async deleteReservation(){
      const resId = event.currentTarget.parentElement.dataset.id;
      const response = await fetch(`https://projects.sbw.media/equipment_reservation/${resId}`,
      {method: "DELETE"})
      const result = await response.json();
      if (result.result) {
        alert("entry deleted");
      }
      console.log(result);
    }

  },
};
</script>

<style lang="sass" scoped>
table
  border-collapse: collapse
  margin: 0 auto
  td
    padding: 0.5rem
</style>
