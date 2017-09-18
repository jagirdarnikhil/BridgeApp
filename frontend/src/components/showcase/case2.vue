<template>
  <q-btn icon="create">{{msg}}</q-btn>  
</template>

<script>
import {
  QBtn
} from 'quasar'

export default {
  name: 'showcase',
  components: {
    QBtn
  },
  data () {
    return {
      msg: 'hello'
    }
  },
  computed: {
  },
  methods: {
  }
}
</script>


