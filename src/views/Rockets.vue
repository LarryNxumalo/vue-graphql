<template>
  <div class="rockets">
    <h1>This is the rockets page</h1>
    <RocketsList/>
  </div>
</template>

<script>

import RocketsList from '@/components/RocketsList.vue'
export default {
    name: 'Rockets',
    components: {
        RocketsList
    }
}
</script>