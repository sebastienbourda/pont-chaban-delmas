<script>
const API_URL = `https://opendata.bordeaux-metropole.fr/api/records/1.0/search/?dataset=previsions_pont_chaban&q=&lang=fr&rows=1000&sort=-date_passage&facet=bateau`
export default {
  data() {
    return {
      status: "Open",
      current_date: "",
      passage_infos: "",
      test_date: "2022-09-03",
      datas: null,
      display: false,
      isHide: true
    }
  },
  created() {
    // fetch on init
    this.currentDateTime()
    this.fetchData()
  },
  updated() {
    this.animateFooter()
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
    },
    animateFooter() {
      // this.isActive = false
      console.log(this.status)
      if (this.status === "Closed") {
        setTimeout(() => {
          this.isHide = false
        }, 700)
      }
    }
  }
}
</script>

<template>
  <main>
    <h1>The bridge is <span class="status">{{ status }}.</span></h1>
    <!-- <h1>Closed between {{ passage_infos.fermeture_a_la_circulation }} and {{ passage_infos.re_ouverture_a_la_circulation }}.</h1> -->
  </main>
  <footer :class="{ 'footer-hide': isHide }">
    <h4>{{ passage_infos.fermeture_a_la_circulation }}</h4>
    <span class="line"></span>
    <h3>{{ passage_infos.bateau }}</h3>
    <span class="line"></span>
    <h4>{{ passage_infos.re_ouverture_a_la_circulation }}</h4>
  </footer>
</template>


<style>
  footer {
    transition: all 600ms cubic-bezier(0.175, 0.885, 0.32, 1.275);
    min-height: 100px;
  }
  .footer-hide {
    transform: translatey(120%);
  }
  .line {
    border-bottom: 1px solid #000;
    height: 1px;
    flex-grow: 1;
  }
</style>
