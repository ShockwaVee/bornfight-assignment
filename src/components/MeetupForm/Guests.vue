<template>
  <div class="guests">
    <div class="add-guests">
      <h4>Add guests</h4>
      <div class="event-name">
        <div class="input-container">
          <input v-model="guests" title="guests" type="text" required>
          <button>Add</button>
        </div>
        <div class="checkbox-container">
          <label v-for="(guestAction, index) of guestActions" :key="index" class="container">
            <input :value="guestAction" v-model="guestChecks" type="checkbox">
            <span class="checkmark"></span>
            {{guestAction}}
          </label>
        </div>
      </div>
    </div>
    <div class="event-publish">
      <div class="dropdowns">
        <div class="select-wrapper">
          <select title="event-type" v-model="typeEvent" name="event-type" required>
            <option v-for="(type, index) in eventType" :key="type + '-' + index" :value="type" :selected="type === typeEvent">{{type}}</option>
          </select>
        </div>
        <div class="select-wrapper">
          <select title="actions" v-model="action" name="actions" required>
            <option v-for="(action, index) in moreActions" :key="action + '-' + index" :value="action" :selected="action === action">{{action}}</option>
          </select>
        </div>
      </div>
      <p class="additional-info">By default this event will follow the sharing settings of this calendar: event
        details will be visible to anyone who can see details of other events in this calendar.
        <a href="#">More</a></p>
      <button>Publish event</button>
    </div>
  </div>
</template>

<script>
import {events} from '../../events'

export default {
  name: 'Guests',
  props: ['eventType', 'moreActions'],
  data () {
    return {
      guests: '',
      guestActions: ['Invite others', 'Modify event', 'See guest list'],
      action: 'More actions',
      typeEvent: 'Public',
      guestChecks: []
    }
  },
  watch: {
    guests () {
      events.$emit('valueChange', 'guests', this.guests.trim().split(','))
    },
    action () {
      events.$emit('valueChange', 'action', this.action)
    },
    typeEvent () {
      events.$emit('valueChange', 'typeEvent', this.typeEvent)
    },
    guestChecks () {
      events.$emit('valueChange', 'guestActions', this.guestChecks)
    }
  }
}
</script>
