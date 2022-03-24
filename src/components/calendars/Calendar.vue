<template>
  <div class="mb-xl border radius-md py-md px-md flex  justify-between">
    <div v-for="(month, index) in months" :key="index" class="calendar-events">
      <div class="text-primary text-center mb-md">{{ month }}</div>
     
      <div class="flex flex-column ">
        <span 
          class="inline-block calendar-event"
          :class="{
            'calendar-event--success': monthEvent.status === 'completed',
            'calendar-event--primary': monthEvent.status === 'booked',
            'calendar-event--secondary': monthEvent.status === 'pending'
          }"
          v-for="(monthEvent, index) in getMonthEvents(month)"
          :key="index"
        ></span>
      </div>
    </div> 
  </div>
</template>

<script>
export default {
  name: 'Calendar',
  props: {
    events: {
      type: Array,
      default: () => []
    }
  },
  data() {
    return {
      months: [
        'Jan', 
        'Feb', 
        'Mar',
        'Apr',
        'May', 
        'Jun',
        'Jul',
        'Aug', 
        'Sep', 
        'Oct', 
        'Nov',
        'Dec'
      ]
    }
  },
  methods: {
    getMonthEvents(month) {
      return this.events.filter(e => e.month === month)
    },
  }
}
</script>
