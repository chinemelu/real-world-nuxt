<template>
  <div>
    <h1>Events</h1>

    <event-card 
      v-for="(event, index) in events" :key="index"
      :event="event"
      :data-index="index"
    />
  </div>
</template>

<script>
import { mapState } from 'vuex'
import EventCard from '@/components/EventCard.vue'
// import EventService from '@/services/EventService'

export default {
  components: { 
    EventCard 
  },
  // async asyncData({ error }) {
    // return $axios.get('http://localhost:3000/events').then(response => {
    //   return {
    //     events: response.data
    //   }
    // })
    // .catch(e => {
    //   error({ statusCode: 503, message: 'Unable to fetch events at this time. Please try again.' })
    // })
    // try {
    //   const { data } = await EventService.getEvents();
    //   return {
    //     events: data
    //   }
    // } catch(e) {
    //   error({ statusCode: 503, message: 'Unable to fetch events at this time. Please try again.' })
    // }

  // },
  async asyncData({ store, error }) {
    try {
      await store.dispatch('events/fetchEvents')
    } catch(e) {
      error({ statusCode: 503, message: 'Unable to fetch events at this time. Please try again.' })
    }
  },
  head() {
    return {
      title: 'Event Listing',
    }
  },
  computed: mapState({
    events: state => state.events.events
  })
}
</script>
