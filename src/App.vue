<template>
  <div>{{ nombre }}</div>
  <div>{{ person }}</div>

  <button @click="handlerClick('title')">Order by title</button>
  <JobList :jobs="jobs" :order="order" />
  
  <router-view/>
</template>
<script lang="ts">
import { defineComponent, reactive, toRefs, ref } from 'vue'
import Job from './types/Job'
import OrderTerm from './types/OrderTerm'
import JobList from './components/JobsLists.vue'

export default defineComponent({
  components:{ JobList },
  setup() {
    const state = reactive({
      nombre : 'Juan Betos',
      age: 25 as string | number
    })

    const person = ref('Ugaldes')
    const age = ref<number | string>(17);
    const jobs = ref<Job[]>([
      { title: 'form warker', location: 'ranchos', salary:700, id: '1' },
      { title: 'pinche poyos', location: 'ranchos', salary:3500, id: '2' },
      { title: 'el vue azul', location: 'colonia', salary:1400, id: '3' }
    ]);
  const order = ref<OrderTerm>('title');

  const handlerClick = (term: OrderTerm) => {
    order.value = term;
  }

    return { ...toRefs(state), person, age, jobs, handlerClick, order }
  },
})
</script>

<style>

</style>
