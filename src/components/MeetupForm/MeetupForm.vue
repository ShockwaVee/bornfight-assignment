<template>
  <form @submit.prevent="submitForm" id="meetup-form">
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
      window.localStorage.setItem('event', JSON.stringify(this.event))
    },
    updateValue (property, value) {
      this.event[property] = value
    }
  },
  mounted () {
    events.$on('onResponse', this.populateFields)
    events.$on('valueChange', this.updateValue)
  }
}
</script>
