<template>
  <div id="app">
    <Header></Header>
    <MeetupForm></MeetupForm>
    <div v-if="modalActive" class="preloader">
      <div v-if="!errorOccurred" class="loading">
        <div class="loading-bar"></div>
        <div class="loading-bar"></div>
        <div class="loading-bar"></div>
        <div class="loading-bar"></div>
      </div>
      <div v-else class="error">
        <span>An error occurred, please try reloading the page!</span>
      </div>
    </div>
  </div>
</template>

<script>
import Header from './components/Header/Header.vue'
import MeetupForm from './components/MeetupForm/MeetupForm.vue'
import axios from 'axios'
import {events} from './events'

export default {
  name: 'App',
  data () {
    return {
      modalActive: true,
      errorOccurred: false
    }
  },
  methods: {
    toggleModal () {
      this.modalActive = !this.modalActive
    }
  },
  components: {
    Header,
    MeetupForm
  },
  mounted () {
    axios
      .get('http://deghq.com/yapp/front-labs/jfed112018/data.json')
      .then(response => {
        this.toggleModal()
        events.$emit('onResponse', response.data)
      })
      .catch(error => { this.errorOccurred = true; console.log(error) })
  }
}
</script>
