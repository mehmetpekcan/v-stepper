<template>
  <div>
    <div class="vsteps--wrapper">
      <!-- 
      |----------------------------------------
      | Steps Area
      |----------------------------------------
      -->
      <div class="vsteps--bar-wrapper">
        <div
          class="vsteps--bar"
          v-for="(item, key) in steps" :key="key"
          @click="stepsChanged(key)"
          >
          <div class="bar--top" :class="[{ active: key < actives + 1 }, color]">
            <div class="bar--top-step" v-if="!item.icon">
              <span v-if="key > actives - 1 && hasCheckIcon">{{ key + 1 }}</span>
              <i v-else-if="key <= actives - 1 && hasCheckIcon" class="fas fa-check"></i>
              <span v-else-if="key > actives - 1 && !hasCheckIcon">{{ key + 1 }}</span>
              <span v-else-if="key <= actives - 1 && !hasCheckIcon">{{ key + 1 }}</span>
            </div>
            <div class="bar--top-step" v-else>
              <i v-if="key <= actives - 1 && hasCheckIcon" class="fas fa-check"></i>
              <i v-else :class="item.icon" />
            </div>
          </div>
          <div class="bar--title">
            <p>{{ item.title }}</p>
          </div>
        </div>
      </div>
      <!-- 
      |----------------------------------------
      | Content Area
      |----------------------------------------
      -->
      <div class="vsteps--content-wrapper">
        <div class="vsteps--content">
            <slot />
        </div>
      </div>
      <!-- 
      |----------------------------------------
      | Buttons Area
      |----------------------------------------
      -->
      <div class="vsteps--buttons-wrapper" v-if="hasButtons">
        <div class="vsteps--buttons">
          <button
            v-if="actives === 0"
            disabled="true"
            class="vsteps--buttons-btn"
            style="color: #bdc3c7; box-shadow: 0 3px 10px -5px #bdc3c7; background-color: #ecf0f1; transition: .2s all ease;"
            >
            Back
          </button>
          <button
            v-if="actives !== 0"
            class="vsteps--buttons-btn"
            :class="color"
            @click="stepChangeByButton(-1)"
            >
            Back
          </button>
          <button
            v-if="actives !== steps.length - 1"
            class="vsteps--buttons-btn"
            :class="color"
            @click="stepChangeByButton(1)"
            >
            Next
          </button>
          <button
            v-if="actives === steps.length - 1"
            class="vsteps--buttons-btn"
            :class="color"
            @click="stepsFinished"
            >
            Finish
          </button>
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
    hasCheckIcon: { required: false, type: Boolean, default: false },
    color: { required: false, type: String, default: "blue" },
    hasButtons: { required: false, type: Boolean, default: true },
    hasDotStyle: { required: false, type: Boolean, default: false }
  },
  methods: {
    stepChangeByButton(payload) {
      if (payload === 1) {
        if (this.actives !== (this.steps.length - 1)) {
          this.actives += 1
        } else {
          return
        }
      } else {
        if (this.actives !== 0) {
          this.actives -= 1
        } else {
          return
        }
      }
      this.stepsChanged(this.actives)
    },
    stepsChanged(key) {
      this.steps.forEach(step => {
        if (step.stepKey === key) {
          step.isActive = true
        } else {
          step.isActive = false
        }
      })
      this.actives = key
      this.$emit("change", this.actives)
    },
    stepsFinished() {
      this.$emit("finish")
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