<template>
  <component :is="iconComponent" />
</template>

<script setup>
import { computed, ref } from 'vue'

const props = defineProps({
  icon: {
    type: String,
    default: 'home'
  }
})

const iconComponent = computed(() => require(`./icons/${props.icon}`).default)
</script>
