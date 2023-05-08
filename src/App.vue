<template>
  <div id="app" :class="{'darkMode':drawer}">
      <div class="navbar">
        <h2>Where in the world?</h2>
        <div class="mode" @click="drawer =! drawer">
          <i class="fas fa-moon"></i>Dark Mode
        </div>
      </div>
    <RouterView/>
  </div>
</template>

<script>
export default {
  data() {
    return{
      drawer: false
    }
  },
  methods: {
    mode() {
      
    }
  }
}
</script>