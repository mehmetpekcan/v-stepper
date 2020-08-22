<template>
  <div>
    <div class="vsteps--wrapper">
      <div class="vsteps--bar-wrapper">
        <div class="vsteps--bar" v-for="(item, key) in steps" :key="key" @click="stepsChanged(key)">
          <div class="bar--top" :class="{ 'active': key < actives + 1 }">
            <div class="bar--top-step">
              <span v-if="key > actives - 1 && options.hasIcon">{{ key + 1 }}</span>
              <i v-else-if="key <= actives - 1 && options.hasIcon" class="fas fa-check"></i>
              <span v-else-if="key > actives - 1 && !options.hasIcon">{{ key + 1 }}</span>
              <span v-else-if="key <= actives - 1 && !options.hasIcon">{{ key + 1 }}</span>
            </div>
          </div>
          <div class="bar--title">
            <p>{{ item.title }}</p>
          </div>
        </div>
      </div>
      <div class="vsteps--content-wrapper">
        <div class="vsteps--content">
          <slot />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "VSteps",
  data() {
    return {
      actives: 0,
      steps: []
    }
  },
  props: {
    options: {
      required: false,
      type: Object,
      default: () => ({
          hasIcon: false,
      })
    }
  },
  methods: {
    stepsChanged(key) {
      this.steps.forEach(step => {
        if (step.stepKey === key) {
          step.isActive = true
        } else {
          step.isActive = false
        }
      })
      this.actives = key
    }
  },
  mounted() {
    this.steps = this.$children

    /* 
    |----------------------------------------
    | Initially make active the first step
    |----------------------------------------
    */
    this.steps[0].isActive = true
  }
}
</script>

<style lang="scss">
@import "./main.scss";
@import "https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.14.0/css/all.min.css";
</style>