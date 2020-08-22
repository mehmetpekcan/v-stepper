<template>
  <div>
    <div class="vsteps--wrapper">
      <div class="vsteps--bar" v-for="(item, key) in 5" :key="key" @click="stepsChanged(key + 1)">
        <div class="bar--top" :class="{ 'active': key < actives }">
          <span class="bar--top-step">{{ key + 1 }}</span>
        </div>
        <div class="bar--title">
          <p>Title {{ key + 1 }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      actives: 1,
    }
  },
  methods: {
    stepsChanged(key) {
      this.actives = key
    }
  }
}
</script>

<style lang="scss">
@import "./main.scss";
</style>