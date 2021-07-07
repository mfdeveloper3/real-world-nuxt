<template>
  <div>
    <h1>{{ event.title }}</h1>
  </div>
</template>

<script>
import { mapState } from 'vuex'

export default {


  async fetch({store, error, params }){
    try {
      await store.dispatch('events/fetchEvent', params.id)
    } catch (e) {
          error({
            statusCode: 503,
            message: 'Unable to fetch event #' + params.id
          })
    }
  },

  head() {
    return {
      title: this.event.id,
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'evento ' + this.event.id
        }
      ]
    }
  },

  computed: mapState({
    event: state => state.events.event
  })


}
</script>

