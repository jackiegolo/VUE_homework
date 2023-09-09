<script setup>
import { computed } from "vue"

const props = defineProps({
  Jobs: {
    type: Array,
    required: true,
    default: [],
  },
})

const JobCount = computed(() => props.Jobs.length)
const noJob = computed(() => JobCount.value === 0)
</script>

<template>
  <h3 v-if="noJob">目前無任何工作</h3>
  <h3 v-else>目前共計 {{ JobCount }} 項工作</h3>
</template>
