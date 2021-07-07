<template>
  <div>
    <h1>Eventos</h1>
    <event-card
    v-for="(event, index) in events"
    :key='index'
    :event='event'
    :data-index='index'
    />
  </div>
</template>

<script>
import EventCard from '@/components/EventCard.vue'
import { mapState } from 'vuex'


export default {
  components: {
    EventCard
  },

  async fetch({ store, error }){
    try {
     await store.dispatch('events/fetchEvents')
    } catch (e) {
          error({
            statusCode: 503,
            message: 'Unable to fetch events events at this time'
          })
    }

  },

  head() {
    return {
        title: 'Event Listing - Real world events',
       meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'pipipipopopo palmeiras 2 santos 0'
        }
      ]
    }
  },

  computed: mapState({
    events: state => state.events.events
  })



}
</script>
