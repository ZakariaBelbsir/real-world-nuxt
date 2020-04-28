<template>
  <div>
    <h1>Events</h1>
    <EventCard
      v-for="(event, index) in events"
      :key="index"
      :event="event"
      :data-index="index"
    />
  </div>
</template>
<script>
import { mapState } from 'vuex'
import EventCard from '../components/EventCard'
export default {
  components: {
    EventCard
  },
  head() {
    return {
      title: 'Event Listing',
      meta: [
        {
          hid: 'description',
          name: 'description',
          content:
            'Where you can find all the events taking place in your neighborhood'
        }
      ]
    }
  },
  async fetch({ store, error }) {
    try {
      await store.dispatch('Event/fetchEvents')
    } catch (e) {
      error({
        statusCode: 503,
        message: 'Unable to fetch events at this time. Please try again'
      })
    }
  },
  computed: mapState({
    events: state => state.Event.events
  })
}
</script>
