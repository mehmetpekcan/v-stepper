<template>
  <div>
    <div class="vsteps--wrapper">
      <div class="vsteps--bar" v-for="(item, key) in 5" :key="key">
        <div class="bar--top" :class="{ 'active': key < 3 }">
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

}
</script>

<style lang="scss">
@import "./main.scss";
</style>