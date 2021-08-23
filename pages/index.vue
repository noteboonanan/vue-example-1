<template>
  <div class="container">
    <h3>สถานการณ์ผู้ติดเชื้อ COVID-19 อัพเดทรายวัน</h3>
    <div>รายงานสถานการณ์ COVID-19 ประจำวัน แยกตามรายจังหวัด</div>
    <table class="table table-striped">
      <thead>
        <tr>
          <th>จังหวัด</th>
          <th>ผู้ป่วย</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in covid_lists" :key="index">
          <td>{{ item.province }}</td>
          <td>{{ item.total_case }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  layout: "auth",
  middleware: "test",
  name: "index",
  data() {
    return {
      count: 0,
      xxx: 2,
      covid_lists: [],
    };
  },
  computed: {
    sum() {
      return this.count * this.xxx;
    },
  },
  mounted() {
    this.initPage();
    this.getApi();
  },
  methods: {
    initPage() {
      console.log("initPage");
    },
    push() {
      this.count += 1;
    },
    async getApi() {
      const data = await this.$axios.$get(
        "https://covid19.ddc.moph.go.th/api/Cases/today-cases-by-provinces"
      );
      this.covid_lists = data;
    },
  },
};
</script>
