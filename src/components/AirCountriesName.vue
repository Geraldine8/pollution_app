<template lang="html">
  <div v-if='country'>
    <span>
      <li>{{country}}</li>
    </span>

  </div>
</template>

<script>

import {eventBus} from '../main.js'
export default {
  name: 'air-countries-name',
  props: ['country']
}
</script>

<style lang="css" scoped>
</style>
