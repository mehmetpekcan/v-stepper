<template>
  <div>
    <slot v-if="isActive" />
  </div>
</template>

<script>
export default {
  props: {
    stepKey: { required: true, type: Number },
    title: { required: true, type: String },
    icon: { required: false, type: String },
    description: { required: false, type: String}
  },
  data() {
    return {
      isActive: false
    }
  },
}
</script>
