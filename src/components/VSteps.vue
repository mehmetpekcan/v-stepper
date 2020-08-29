<template>
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
        <div
          class="vsteps--bar-progress"
          :class="{ completed: key < actives, active: key === actives }"
          >
          <div class="bar--top dot-style" v-if="dotStyle">
            <span class="circle" :class="['color']"></span>
          </div>
          <div class="bar--top" v-else-if="!hasCheckIcon">
            <span class="circle">{{ key + 1 }}</span>
          </div>
          <div class="bar--top" v-else-if="hasCheckIcon">
            <i v-if="key < actives" class="circle fas fa-check" />
            <span v-else class="circle">{{ key + 1 }}</span>
          </div>
          <div class="bar--title">
            <p class="bar--title-h1">{{ item.title }}</p>
            <p v-if="item.description" class="bar--title-description"> {{ item.description }}</p>
          </div>
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
    <div class="vsteps--buttons-wrapper" v-if="buttons">
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
</template>

<script>
export default {
  name: "VSteps",
  data() {
    return {
      actives: 0,
      steps: [],
    }
  },
  props: {
    hasCheckIcon: { required: false, type: Boolean, default: false },
    color: { required: false, type: String, default: "red" },
    buttons: { required: false, type: Boolean, default: true },
    dotStyle: { required: false, type: Boolean, default: false },
    animation: { required: false, type: String, default: "fade" }
  },
  computed: {
    lineWidth() {
      return { width: 10 + 'rem'}
    }
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
  },
  created() {
  }
}
</script>

<style lang="scss">
@import "./main.scss";
@import "https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.14.0/css/all.min.css";
</style>