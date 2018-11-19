<template>
  <form id="meetup-form">
    <GeneralInfo></GeneralInfo>
    <div class="guests">
      <div class="add-guests">
        <h4>Add guests</h4>
        <div class="event-name">
          <div class="input-container">
            <input type="text">
            <button>Add</button>
          </div>
          <div class="checkbox-container">
            <label class="container">
              <input type="checkbox">
              <span class="checkmark"></span>
              Invite others
            </label>
            <label class="container">
              <input type="checkbox">
              <span class="checkmark"></span>
              Modify event
            </label>
            <label class="container">
              <input type="checkbox">
              <span class="checkmark"></span>
              See guest list
            </label>
          </div>
        </div>
      </div>
      <div class="event-publish">
        <div class="dropdowns">
          <div class="select-wrapper">
            <select name="publicity">
              <option v-for="(type, index) in eventType" :key="type + '-' + index" :value="type">{{type}}</option>
            </select>
          </div>
          <div class="select-wrapper">
            <select name="actions">
              <option v-for="(action, index) in moreActions" :key="action + '-' + index" :value="action">{{action}}</option>
            </select>
          </div>
        </div>
        <p class="additional-info">By default this event will follow the sharing settings of this calendar: event
          details will be visible to anyone who can see details of other events in this calendar.
          <a href="#">More</a></p>
        <button>Publish event</button>
      </div>
    </div>
    <div class="event-details">
      <div class="tabs">
        <span class="active">Event details</span>
        <span>Find a time</span>
      </div>
      <div class="location">
        <label for="location">Where</label>
        <input placeholder="Enter Location of your event" type="text">
        <label for="Description">Description</label>
        <textarea type="text"></textarea>
      </div>
      <div class="additional-info">
        <div class="notifications">
          <label>Notifications</label>
          <div class="notification-dropdowns">
            <div class="select-wrapper">
              <select name="notifications">
                <option v-for="(type, index) in notifications.type" :key="type + '-' + index" :value="type">{{type}}</option>
              </select>
            </div>
            <input type="text">
            <div class="select-wrapper">
              <select name="time">
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
              <select name="person">
                <option v-for="(user, index) in calendar.users" :key="user + '-' + index" :value="user">{{user}}</option>
              </select>
            </div>
            <div class="select-wrapper">
              <select name="show-as">
                <option v-for="(as, index) in calendar.showAs" :key="as + '-' + index" :value="as">{{as}}</option>
              </select>
            </div>
          </div>
        </div>
        <div class="event-colors">
          <label>Event color</label>
          <div class="checkbox-container">
            <label class="container">
              <input name="color" type="radio">
              <span class="checkmark"></span>
            </label>
            <label class="container">
              <input name="color" type="radio">
              <span class="checkmark"></span>
            </label>
            <label class="container">
              <input name="color" type="radio" checked="checked">
              <span class="checkmark"></span>
            </label>
            <label class="container">
              <input name="color" type="radio">
              <span class="checkmark"></span>
            </label>
            <label class="container">
              <input name="color" type="radio">
              <span class="checkmark"></span>
            </label>
            <label class="container">
              <input name="color" type="radio">
              <span class="checkmark"></span>
            </label>
            <label class="container">
              <i class="fas fa-ellipsis-h"></i>
            </label>
          </div>
        </div>
      </div>
    </div>
  </form>
</template>

<script>
import GeneralInfo from './GeneralInfo'
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
      }
    }
  },
  components: {GeneralInfo},
  methods: {
    populateFields: function (response) {
      this.eventType = response.eventType
      this.moreActions = response.moreActions.values
      this.notifications.type = response.notifications.type
      this.notifications.time = response.notifications.time
      this.calendar.users = response.calendar.users
      this.calendar.showAs = response.calendar.showAs.values
    }
  },
  mounted () {
    events.$on('onResponse', this.populateFields)
  }
}
</script>
