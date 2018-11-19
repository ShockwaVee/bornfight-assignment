<template>
  <div class="event-details">
    <div class="tabs">
      <span class="active">Event details</span>
      <span>Find a time</span>
    </div>
    <div class="location">
      <label for="location">Where</label>
      <input title="location" placeholder="Enter Location of your event" v-model="location" type="text" required>
      <label for="description">Description</label>
      <textarea title="description" type="text" v-model="description" required></textarea>
    </div>
    <div class="additional-info">
      <div class="notifications">
        <label>Notifications</label>
        <div class="notification-dropdowns">
          <div class="select-wrapper">
            <select title="notifications" name="notifications" v-model="notification.type" required>
              <option v-for="(type, index) in notifications.type" :key="type + '-' + index" :value="type" :selected="type === notification.type">{{type}}</option>
            </select>
          </div>
          <input title="amount" type="text" v-model="notification.amount" required>
          <div class="select-wrapper">
            <select title="time" name="time" v-model="notification.time" required>
              <option v-for="(time, index) in notifications.time" :key="time + '-' + index" :value="time">{{time}}</option>
            </select>
          </div>
          <i class="fas fa-times"></i>
        </div>
        <div class="add-notification">
          <i class="fas fa-plus"></i>
          <span>Add a notification</span>
        </div>
      </div>
      <div class="calendar">
        <label>Calendar</label>
        <div class="dropdowns">
          <div class="select-wrapper">
            <select title="user" name="user" v-model="calendar.user" required>
              <option v-for="(user, index) in calendars.users" :key="user + '-' + index" :value="user" :selected="user === calendar.user">{{user}}</option>
            </select>
          </div>
          <div class="select-wrapper">
            <select title="show-as" name="show-as" v-model="calendar.as" required>
              <option v-for="(as, index) in calendars.showAs" :key="as + '-' + index" :value="as" :selected="as === calendar.as">{{as}}</option>
            </select>
          </div>
        </div>
      </div>
      <div class="event-colors">
        <label>Event color</label>
        <div class="checkbox-container">
          <label class="container" v-for="(colorSelect, index) in colors" :key="index">
            <input v-model="color" :name="colorSelect" :selected="color === colorSelect" :value="colorSelect" type="radio">
            <span class="checkmark"></span>
          </label>
          <label class="container">
            <i class="fas fa-ellipsis-h"></i>
          </label>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import {events} from '../../events'

export default {
  name: 'EventDetails',
  data () {
    return {
      location: '',
      description: '',
      notification: {
        type: 'Email',
        time: 'Minutes',
        amount: ''
      },
      calendar: {
        user: 'Mario Šestak',
        as: 'Show me as'
      },
      colors: ['blue', 'pale-blue', 'indigo', 'aquamarine', 'yellow', 'red'],
      color: 'indigo'
    }
  },
  props: ['notifications', 'calendars'],
  watch: {
    location () {
      events.$emit('valueChange', 'location', this.location)
    },
    description () {
      events.$emit('valueChange', 'description', this.description)
    },
    notification: {
      handler () {
        events.$emit('valueChange', 'notification', this.notification)
      },
      deep: true
    },
    calendar: {
      handler () {
        events.$emit('valueChange', 'calendar', this.calendar)
      },
      deep: true
    },
    color () {
      events.$emit('valueChange', 'color', this.color)
    }
  }
}
</script>

<style scoped>

</style>
