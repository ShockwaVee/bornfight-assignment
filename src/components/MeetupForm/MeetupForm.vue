<template>
  <form ref="form" @submit.prevent="submitForm" id="meetup-form">
    <ul v-if="errors.length>0" class="errors">
      <li v-for="(error, index) of errors" :key="index">{{error}}</li>
    </ul>
    <GeneralInfo></GeneralInfo>
    <Guests :eventType="eventType" :moreActions="moreActions"></Guests>
    <EventDetails :notifications="notifications" :calendars="calendar"></EventDetails>
  </form>
</template>

<script>
import GeneralInfo from './GeneralInfo'
import Guests from './Guests'
import EventDetails from './EventDetails'
import {events} from '../../events'

export default {
  name: 'MeetupForm',
  data () {
    return {
      eventType: [],
      moreActions: [],
      notifications: {
        type: [],
        time: []
      },
      calendar: {
        users: [],
        showAs: []
      },
      errors: [],
      event: {
        notification: {
          type: 'Email',
          time: 'Minutes',
          amount: ''
        },
        calendar: {
          user: 'Mario Šestak',
          as: 'Show me as'
        },
        color: 'indigo',
        action: 'More actions',
        typeEvent: 'Public',
        startDateTime: {
          date: '11/25/2016',
          time: '5:00pm'
        },
        endDateTime: {
          date: '11/25/2016',
          time: '6:00pm'
        }
      }
    }
  },
  components: {GeneralInfo, Guests, EventDetails},
  methods: {
    populateFields (response) {
      this.eventType = response.eventType
      this.moreActions = response.moreActions.values
      this.notifications.type = response.notifications.type
      this.notifications.time = response.notifications.time
      this.calendar.users = response.calendar.users
      this.calendar.showAs = response.calendar.showAs.values
    },
    submitForm () {
      let isFormValid = []
      this.errors = []
      if (!this.event.hasOwnProperty('name') || this.event.name.length < 2) isFormValid.push('Event name needs to be longer than two character')
      if (!this.event.hasOwnProperty('guests') || this.event.guests.length === 0) isFormValid.push('Guest list must not be empty')
      if (!this.event.hasOwnProperty('location') || this.event.location.length < 1) isFormValid.push('Location needs to be longer than one character')
      if (!this.event.hasOwnProperty('description') || this.event.description.length < 10) isFormValid.push('Description needs to be longer than 10 characters')
      if (this.event.notification.amount === '' || this.event.notification.amount <= 0) isFormValid.push('Value of notification interval must be a number greater than zero')
      if (!isFormValid.length) {
        window.localStorage.setItem('event', JSON.stringify(this.event))
        this.clearForm()
      } else {
        this.errors = isFormValid
      }
    },
    updateValue (property, value) {
      this.event[property] = value
    },
    clearForm () {
      this.$refs.form.reset()
      events.$emit('resetForm')
    }
  },
  mounted () {
    events.$on('onResponse', this.populateFields)
    events.$on('valueChange', this.updateValue)
    events.$on('clearForm', this.clearForm)
    events.$on('submitForm', this.submitForm)
  }
}
</script>
