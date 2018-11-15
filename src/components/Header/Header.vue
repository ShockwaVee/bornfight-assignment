<template>
    <header>
      <div class="back-button">
        <i class="fas fa-angle-left"></i>
      </div>
      <HeaderMain></HeaderMain>
      <div class="menu">
        <div class="notification">
          <i class="far fa-bell"></i>
        </div>
        <div class="additional-menu">
          <i class="fas fa-th"></i>
        </div>
      </div>
    </header>
</template>

<script>
import HeaderMain from './HeaderMain.vue'

export default {
  name: 'Header',
  components: {HeaderMain}
}
</script>
