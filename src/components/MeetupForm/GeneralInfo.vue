<template>
  <div class="general-info">
    <div class="event-name">
      <div class="input-container">
        <input v-model="name" title="event-name" type="text" required>
        <button type="submit">Save event</button>
      </div>
      <div class="checkbox-container">
        <label v-for="(eventOccurrence, index) in eventOccurrences" :key="index" class="container">
          <input :value="eventOccurrence" v-model="eventChecks" type="checkbox">
          <span class="checkmark"></span>
          {{eventOccurrence}}
        </label>
      </div>
    </div>
    <div class="event-time">
      <div class="starting-time">
        <div class="time"><span>5:00pm</span></div>
        <div class="date"><span>11/25/2016</span></div>
      </div>
      <div class="ending-time">
        <div class="time"><span>6:00pm</span></div>
        <div class="date"><span>11/25/2016</span></div>
      </div>
      <a href="#">Time zone</a>
    </div>
  </div>
</template>

<script>
import {events} from '../../events'

export default {
  name: 'GeneralInfo',
  data () {
    return {
      name: '',
      eventOccurrences: ['All day', 'Repeat'],
      eventChecks: []
    }
  },
  methods: {
    resetData () {
      this.name = ''
      this.eventChecks = []
    }
  },
  watch: {
    name () {
      events.$emit('valueChange', 'name', this.name)
    },
    eventChecks () {
      events.$emit('valueChange', 'occurrence', this.eventChecks)
    }
  },
  mounted () {
    events.$on('resetForm', this.resetData)
  }
}
</script>
