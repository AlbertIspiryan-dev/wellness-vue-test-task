<template>
  <main class="p-md">
    <h1 class="text-semibold text-dark-blue mb-md">2021 Wellness Plan</h1>

    <card>
      <template #title>
        <div class="flex">
          <h2 class="text-semibold text-dark-blue">Your Progress</h2>
          <span class="text-gray text-medium mb-3px self-end ml-sm">3 steps to complete</span>
        </div>
      </template>

      <div class="flex mobile-flex-wrap px-4xl mt-lg">
        <div class="flex-grow chart-section">
          <DoughnutChart :chartData="chartData" ref="chart" />

          <div class="text-center mt-lg">
            Completed <br /> appointments
          </div>
        </div>

        <div class="items-section ml-2xl">
          <div>
            <calendar :events="appointments" />
          </div>

          <list>
            <list-item
              v-for="appointment in appointments"
              :key="appointment.id"
              :item-data="appointment"
              @deleteItem="removeAppointment"
              class="mb-md py-lg px-md"
            />
          </list>
        </div>
      </div>
    </card>
  </main>
</template>

<script>
import Card from '@/components/cards/Card.vue'
import List from '@/components/lists/List.vue'
import ListItem from '@/components/lists/ListItem.vue'
import Calendar from '@/components/calendars/Calendar.vue'
import DoughnutChart from '@/components/charts/DoughnutChart.vue'

export default {
  name: 'App',
  components: {
    Card,
    List,
    ListItem,
    Calendar,
    DoughnutChart,
  },
  data() {
    return {
      appointments: [
        { id: 1, month: 'Jun', title: 'Hormone replacement therapy', status: 'completed' },
        { id: 2, month: 'Jun', title: 'Ozone therapy', status: 'completed' },
        { id: 3, month: 'Jun', title: 'NAD', status: 'completed' },
        { id: 4, month: 'Jun', title: 'Hormone replacement therapy', status: 'completed' },
        { id: 5, month: 'Feb', title: 'Ozone therapy', status: 'booked' },
        { id: 6, month: 'Feb', title: 'NAD', status: 'booked' },
        { id: 7, month: 'Apr', title: 'Hormone replacement therapy', status: 'pending' },
      ],
    }
  },
  computed: {
    chartData() {
      let finishedAppointments = this.appointments.filter(a => a.status === 'completed').length
      let bookedAppointments   = this.appointments.filter(a => a.status === 'booked').length
      
      return {
        datasets: [
          {
            data: [finishedAppointments, bookedAppointments]
          }
        ]
      }
    },
  },
  methods: {
    removeAppointment(appointmentId) {
      this.appointments = this.appointments.filter(a => a.id !== appointmentId)
    }
  }
}
</script>
