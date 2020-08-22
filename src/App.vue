<template>
  <div id="app">
    <div style="height: 100vh; display: flex; align-items: center; justify-content: center;">
      <v-steps></v-steps>
    </div>
  </div>
</template>

<script>
import VSteps from "@/components/VSteps"

export default {
  name: 'App',
  components: { VSteps }
}
</script>
