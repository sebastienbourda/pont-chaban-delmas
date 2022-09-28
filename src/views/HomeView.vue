<script>
const API_URL = `https://opendata.bordeaux-metropole.fr/api/records/1.0/search/?dataset=previsions_pont_chaban&q=&lang=fr&rows=1000&sort=-date_passage&facet=bateau`
export default {
  data() {
    return {
      status: "",
      current_date: "",
      passage_infos: "",
      test_date: "2022-09-27",
      datas: null,
      display: false
    }
  },
  created() {
    // fetch on init
    this.currentDateTime()
    this.fetchData()
  },
  methods: {
    async fetchData() {
      const url = `${API_URL}`
      this.datas = await (await fetch(url)).json()
      this.datas = this.datas.records
      this.checkOpening(this.datas)
    },
    currentDateTime() {
      const current = new Date();
      const date = current.getFullYear() + '-' + '0' + (current.getMonth()+1) + '-' + current.getDate();
      const time = current.getHours() + ":" + current.getMinutes() + ":" + current.getSeconds();
      const dateTime = date + ' ' + time;
      this.timestamp = dateTime;
      this.current_date = date;
    },
    checkOpening(datas) {
      datas.forEach(passage => {
        // console.log(passage.fields.date_passage)
        if (passage.fields.date_passage === this.current_date) {
          this.status = "Closed"
          this.passage_infos = passage.fields
        }
      });
    }
  }
}
</script>

<template>
  <main>
    <h1>The bridge is <span class="status">{{ status }}.</span></h1>
    <!-- <h1>Closed between {{ passage_infos.fermeture_a_la_circulation }} and {{ passage_infos.re_ouverture_a_la_circulation }}.</h1> -->
  </main>
</template>
