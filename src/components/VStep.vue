<template>
  <div v-if="$parent.slide">
    <transition name="slide" class="slider">
      <div class="slot" v-if="isActive">
        <slot />
      </div>
    </transition>
  </div>
  <div v-else>
    <div v-if="isActive">
      <slot />
    </div>
  </div>
</template>

<script>
export default {
  props: {
    stepKey: { required: true, type: Number },
    title: { required: true, type: String },
    icon: { required: false, type: String },
    description: { required: false, type: String }
  },
  data() {
    return {
      isActive: false,
    }
  }
}
</script>

<style scoped lang="scss">
.slider{
  overflow: hidden;
  position: relative;
  height: 200px;
  width: 400px;
  
  .slot {
    position: absolute;
    top: 0;
    left: 0;
    bottom: 0;
    right:0;
  }
}

.slide-leave-active,
.slide-leave-to {
    display: none;
}

.slide-enter-active {
  transition: 1s;
}
.slide-enter {
  transform: translate(100%, 0);
}
</style>