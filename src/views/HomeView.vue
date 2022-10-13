<script setup>
import dayjs from 'dayjs';
</script>

<script>
const API_URL = `https://opendata.bordeaux-metropole.fr/api/records/1.0/search/?dataset=previsions_pont_chaban&q=&lang=fr&rows=1000&facet=bateau`

export default {
  data() {
    return {
      status: "Open",
      current_date: "",
      passage_infos: [],
      test_date: "2022-05-30",
      data: null,
      display: false,
      isHide: true
    }
  },
  updated() {
    this.animateInfos()
  },
  mounted() {
    // fetch on init
    this.currentDateTime()
    this.fetchData()
  },
  methods: {
    async fetchData() {
      const url = `${API_URL}`
      this.data = await (await fetch(url)).json()
      this.data = this.data.records
      this.checkOpening(this.data)
    },
    currentDateTime() {
      const current = new Date();
      console.log(this.formatDate(current))
      const date = current.getFullYear() + '-' + (current.getMonth()+1) + '-' + current.getDate();
      const time = current.getHours() + ":" + current.getMinutes() + ":" + current.getSeconds();
      this.current_date = this.formatDate(date);
    },
    checkOpening(data) {
      data.forEach(passage => {
        if (passage.fields.date_passage === this.test_date) {
          this.status = "Closed"
          this.passage_infos.push(passage.fields)
        }
      });
      if (this.passage_infos.length > 1) {
        this.passage_infos.forEach(passage => {
          console.log(passage.re_ouverture_a_la_circulation)
        });
        this.passage_infos.reverse();
      }
    },
    animateInfos() {
      // this.isActive = false
      console.log(this.status)
      if (this.status === "Closed") {
        setTimeout(() => {
          this.isHide = false
        }, 1200)
      }
    },
    formatDate(dateString) {
      const date = dayjs(dateString);
      // Then specify how you want your dates to be formatted
      return date.format('YYYY-MM-DD');
    }
  }
}
</script>

<template>
  <main>
    <h1 v-if="status === 'Open'">The bridge will be <span class="status">{{ status }}.</span></h1>
    <h1 v-else>The bridge will be <span class="status">{{ status }}</span>.</h1>
  </main>
  <div :class="[{ 'infos-hide': isHide }, 'infos']">
    <div class="passage" v-for="passage in passage_infos">
      <h3>{{ passage.bateau }}</h3>
      <div class="schedule">
        <h4>{{ passage.fermeture_a_la_circulation }}</h4>
        <span class="line"></span>
        <h4>{{ passage.re_ouverture_a_la_circulation }}</h4>
      </div>
    </div>
  </div>
</template>

<style>
  .infos{
    transition: all 600ms cubic-bezier(0.175, 0.885, 0.32, 1.275);
    min-height: 100px;
    margin-bottom: 100px;
    display: flex;
    align-items: center;
    width: 100%;
    gap: 100px;
    justify-content: center;
    text-align: center;
  }
  .infos-hide{
    transform: translateY(150%);
  }
  .line{
    border-bottom: 1px solid #000;
    height: 1px;
    width: 30px;
  }
  .schedule{
    display: flex;
    gap: 10px;
    justify-content: center;
    align-items: center;
  }
  .passage{

  }
  @media (max-width: 800px) {
    .infos {
      flex-direction: column;
    }
  }

</style>
