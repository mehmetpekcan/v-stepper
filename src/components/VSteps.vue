<template>
  <div>
    <div class="vsteps--wrapper">
      <div class="vsteps--bar-wrapper">
        <div class="vsteps--bar" v-for="(item, key) in steps" :key="key" @click="stepsChanged(key)">
          <div class="bar--top" :class="{ 'active': key < actives + 1 }">
            <span class="bar--top-step">{{ key + 1 }}</span>
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
  data() {
    return {
      actives: 0,
      steps: []
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
  created() {
    this.steps = this.$children
  }
}
</script>

<style lang="scss">
@import "./main.scss";
</style>