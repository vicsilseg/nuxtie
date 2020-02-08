<template>
  <div>
    <h1>Hello World!</h1>
    <event-card
      v-for="(event, index) in events"
      :key="index"
      :event="event"
      :data-index="index"
    ></event-card>
  </div>
</template>

<script>
import EventCard from '@/components/EventCard'
import { mapState } from 'vuex'

export default {
  head() {
    return {
      title: 'Hi everybody'
    }
  },
  components: {
    EventCard
  },
  computed: {
    ...mapState({
      events: (state) => state.events.events
    })
  },
  async fetch({ store, error }) {
    try {
      await store.dispatch('events/fetchEvents')
    } catch (e) {
      error({
        statusCode: 503,
        message: 'Unable to fetch events at this time. Please try again'
      })
    }
  }
}
</script>
