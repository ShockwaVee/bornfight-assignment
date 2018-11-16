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
              <option value="public">Public</option>
              <option value="dva">Dva</option>
              <option value="tri">Tri</option>
            </select>
          </div>
          <div class="select-wrapper">
            <select name="actions">
              <option value="more">More actions</option>
              <option value="dva">Dva</option>
              <option value="tri">Tri</option>
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
          <div class="select-wrapper">
            <select name="notifications">
              <option value="email">Email</option>
              <option value="dva">dva</option>
              <option value="tri">tri</option>
            </select>
          </div>
          <input type="text">
          <div class="select-wrapper">
            <select name="time">
              <option value="minutes">Minutes</option>
              <option value="hours">Hours</option>
            </select>
          </div>
          <i class="fas fa-times"></i>
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
                <option value="public">Mario Šestak</option>
                <option value="dva">Dva</option>
                <option value="tri">Tri</option>
              </select>
            </div>
            <div class="select-wrapper">
              <select name="show-as">
                <option value="more">Show me as</option>
                <option value="dva">Dva</option>
                <option value="tri">Tri</option>
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
            <div class="misc-options"></div>
          </div>
        </div>
      </div>
    </div>
  </form>
</template>

<script>
  import GeneralInfo from './GeneralInfo'

  export default {
    name: 'MeetupForm',
    components: {GeneralInfo}
  }
</script>

<style scoped>

</style>
