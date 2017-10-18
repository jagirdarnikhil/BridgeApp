<template>
  <div class="layout-padding docs-btn row justify-center">
    <div style="width: 500px; max-width: 90vw;">
    <center><h3 class="caption"><b>Day 1</b></h3></center>
    <q-btn color="primary" class="full-width">Today's Evaluation</q-btn>
    </div>
      <div style="width: 500px; max-width: 90vw;">
        <!--Mood-->
        <p>Mood</p>
        <q-fab
        color="green"
        icon="mood"
        direction="right"
        >
          <q-fab-action
          color="red-2"
          icon="sentiment very satisfied"
          />
          <q-fab-action
          color="red-3"
          icon="sentiment satisfied"
          />
          <q-fab-action
          color="red-4"
          icon="sentiment neutral"
          />
          <q-fab-action
          color="red-5"
          icon="sentiment dissatisfied"
          />
          <q-fab-action
          color="red-6"
          icon="sentiment very dissatisfied"
          />
        </q-fab>

        <!--anxiety-->
        <p>Anxiety</p>
        <q-fab
        color="yellow"
        icon="face"
        direction="right"
        >
          <q-fab-action
          color="red-2"
          icon="sentiment very satisfied"
          />
          <q-fab-action
          color="red-3"
          icon="sentiment satisfied"
          />
          <q-fab-action
          color="red-4"
          icon="sentiment neutral"
          />
          <q-fab-action
          color="red-5"
          icon="sentiment dissatisfied"
          />
          <q-fab-action
          color="red-6"
          icon="sentiment very dissatisfied"
          />
        </q-fab>

        <!--pain-->
        <p>Pain</p>
        <q-fab
        color="red"
        icon="whatshot"
        direction="right"
        >
          <q-fab-action
          color="red-2"
          icon="sentiment very satisfied"
          />
          <q-fab-action
          color="red-3"
          icon="sentiment satisfied"
          />
          <q-fab-action
          color="red-4"
          icon="sentiment neutral"
          />
          <q-fab-action
          color="red-5"
          icon="sentiment dissatisfied"
          />
          <q-fab-action
          color="red-6"
          icon="sentiment very dissatisfied"
          />
        </q-fab>
        <!--itch-->
        <p>Itch</p>
        <q-fab
        color="blue-grey"
        icon="pan tool"
        direction="right"
        >
          <q-fab-action
          color="red-2"
          icon="sentiment very satisfied"
          />
          <q-fab-action
          color="red-3"
          icon="sentiment satisfied"
          />
          <q-fab-action
          color="red-4"
          icon="sentiment neutral"
          />
          <q-fab-action
          color="red-5"
          icon="sentiment dissatisfied"
          />
          <q-fab-action
          color="red-6"
          icon="sentiment very dissatisfied"
          />
        </q-fab>
      </div>

    <q-fab
    class="fixed"
    style="right: 18px; bottom: 18px"
    color="purple"
    icon="video library"
    direction="up"
    >
      <q-fab-action
      color="primary"
      icon="healing"
      />

      <q-fab-action
      color="secondary"
      icon="directions run"
      />
    </q-fab>

  </div>
</template>

<script>
import {
  QBtn,
  QFab,
  QFabAction
} from 'quasar'
export default {
  components: {
    QBtn,
    QFab,
    QFabAction
  },
  data () {
    return {
    }
  },
  methods: {
  }
}
</script>
