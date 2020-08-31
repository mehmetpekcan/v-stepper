<template>
  <div id="app">
    <div>
      <v-stepper>
        <v-step :stepKey="0" title="Üye Ol">Step 1</v-step>
        <v-step :stepKey="1" title="Numara Onayla">Step 2</v-step>
        <v-step :stepKey="2" title="Tebrikler">Step 3</v-step>
      </v-stepper>
    </div>
  </div>
</template>

<script>
import VStepper from "@/components/VStepper"
import VStep from "@/components/VStep"

export default {
  name: 'App',
  components: { VStepper, VStep }
}
</script>
