<template>
  <div class="content">
    <div class="actions">
      <button @click="submitForm">Save</button>
      <div @click="clearForm(false)"><i class="fas fa-times-circle"></i>Discard</div>
      <div @click="clearForm(true)"><i class="fas fa-trash"></i>Delete</div>
    </div>
    <div class="user">
      <i class="fas fa-search"></i>
      <div class="image"><img src="../../assets/davor.jpg" alt="User image"></div>
    </div>
  </div>
</template>

<script>
import {events} from '../../events'

export default {
  name: 'HeaderMain',
  methods: {
    clearForm (withAlert) {
      let shouldClear = true
      if (withAlert) {
        shouldClear = confirm('Are you sure you want to delete all of the data?')
      }
      if (shouldClear) events.$emit('clearForm')
    },
    submitForm () {
      events.$emit('submitForm')
    }
  }
}
</script>
