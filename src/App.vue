<template>
  <div id="app">
    <Header></Header>
    <MeetupForm></MeetupForm>
  </div>
</template>

<script>
import Header from './components/Header/Header.vue'
import MeetupForm from './components/MeetupForm/MeetupForm.vue'

export default {
  name: 'App',
  components: {
    Header,
    MeetupForm
  }
}
</script>
