<template>
  <div class="layout-padding card-examples row items-start">
    <q-card inline>
      <q-card-main>
        {{lorem}}
      </q-card-main>
    </q-card>

  </div>
</template>
<script>
import {
  QCard
} from 'quasar'
export default {
  components: {
    QCard
  },
  data () {
    return {
      stars: 3,
      lorem: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.'
    }
  }
}
</script>

<style lang="stylus">
@import '~variables'
.card-examples
  .q-card
    width 300px
  .bigger
    width 450px
  @media (max-width $breakpoint-xs-max)
    .q-card
      width 100%
</style>
