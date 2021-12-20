<template>
  <h3>Order by {{ order }}</h3>
  <ul>
    <li v-for="job in orderedJobs" :key="job.id">{{ job.title }}- {{ job.location }}</li>
  </ul>
</template>

<script lang="ts">
import Job from '@/types/Job'
import OrderTerm from '@/types/OrderTerm'
import { defineComponent, PropType, computed } from 'vue'

export default defineComponent({
  props: {
    jobs: {
      required: true,
      type: Array as PropType<Job[]>,
    },
    order: {
      required: true,
      type: String as PropType<OrderTerm>
    }
  },
  setup(props){
    const orderedJobs = computed(() => {
      return [...props.jobs].sort((a: Job, b: Job) => { 
        return a[ props.order ] > b[props.order] ? 1 : -1
       })
    });

    return { orderedJobs }
  }
})
</script>
<style scoped>

</style>
