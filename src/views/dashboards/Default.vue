<template>
  <div class="py-4 container-fluid">
    <div class="row">
      <div class="col-lg-12 position-relative z-index-2">
        <div class="row">
          <div class="col-lg-3 col-md-6 col-sm-6">
            <mini-statistics-card
              :title="{ text: 'Bookings', value: 281 }"
              detail="<span class='text-success text-sm font-weight-bolder'>+55%</span> than last week"
              :icon="{
                name: 'weekend',
                color: 'text-white',
                background: 'dark',
              }"
            />
          </div>
          <div class="col-lg-3 col-md-6 col-sm-6 mt-lg-0 mt-4">
            <mini-statistics-card
              :title="{ text: 'Today\'s Users', value: '2,300' }"
              detail="<span class='text-success text-sm font-weight-bolder'>+3%</span> than last month"
              :icon="{
                name: 'leaderboard',
                color: 'text-white',
                background: 'primary',
              }"
            />
          </div>
          <div class="col-lg-3 col-md-6 col-sm-6 mt-lg-0 mt-4">
            <mini-statistics-card
              :title="{ text: 'Revenue', value: '34k' }"
              detail="<span class='text-success text-sm font-weight-bolder'>+1%</span> than yesterday"
              :icon="{
                name: 'leaderboard',
                color: 'text-white',
                background: 'success',
              }"
            />
          </div>
          <div class="col-lg-3 col-md-6 col-sm-6 mt-lg-0 mt-4">
            <mini-statistics-card
              :title="{ text: 'Followers', value: '+91' }"
              detail="Just updated"
              :icon="{
                name: 'person_add',
                color: 'text-white',
                background: 'info',
              }"
            />
          </div>
        </div>
        <div class="mt-4 row">
          <div class="col-lg-4 col-sm-6">
            <channels-chart-card />
          </div>
          <div class="mt-4 col-lg-8 col-sm-6 mt-sm-0">
            <revenue-chart-card />
          </div>
        </div>
      </div>
    </div>

    <div class="row"></div>
  </div>
</template>
<script>
import SalesTableCard from "./components/SalesTableCard.vue";
import ChartHolderCard from "./components/ChartHolderCard.vue";
import ReportsBarChart from "@/examples/Charts/ReportsBarChart.vue";
import ReportsLineChart from "./components/ReportsLineChart.vue";
import MiniStatisticsCard from "./components/MiniStatisticsCard.vue";
import BookingCard from "./components/BookingCard.vue";

import US from "../../assets/img/icons/flags/US.png";
import DE from "../../assets/img/icons/flags/DE.png";
import GB from "../../assets/img/icons/flags/GB.png";
import BR from "../../assets/img/icons/flags/BR.png";
import booking1 from "../../assets/img/products/product-1-min.jpg";
import booking2 from "../../assets/img/products/product-2-min.jpg";
import booking3 from "../../assets/img/products/product-3-min.jpg";
import ChannelsChartCard from "@/views/dashboards/components/ChannelsChartCard.vue";
import RevenueChartCard from "@/views/dashboards/components/RevenueChartCard.vue";

export default {
  name: "DashboardDefault",
  components: {
    RevenueChartCard,
    ChannelsChartCard,
    SalesTableCard,
    ChartHolderCard,
    ReportsBarChart,
    ReportsLineChart,
    MiniStatisticsCard,
    BookingCard,
  },
  data() {
    return {
      booking1,
      booking2,
      booking3,
      US,
      DE,
      GB,
      BR,
    };
  },
};
</script>
