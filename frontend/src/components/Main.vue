<template>
  <q-layout
    ref="layout"
    view="lHh Lpr fff"
    :left-class="{'bg-grey-2': true}"
  >
  <div class="layout-padding docs-input row justify-center">
    <div style="width: 500px; max-width: 90vw;">
    <q-input v-model="email" type="email" float-label="Email" suffix="@gmail.com" clearable />
    <q-input v-model="password" type="password" float-label="Password" />
    </div>
  </div>
    <q-toolbar slot="header" class="glossy">
      <q-btn
        flat
        @click="$refs.layout.toggleLeft()"
      >
        <q-icon name="menu" />
      </q-btn>

      <q-toolbar-title>
        Bridge App
        <div slot="subtitle">Running on Quasar v{{$q.version}}</div>
      </q-toolbar-title>
    </q-toolbar>

    <q-tabs slot="navigation" v-if="true">
      <q-route-tab slot="title" icon="accessibility" to="/case2" replace label="Evaluation" />
      <q-route-tab slot="title" icon="view_array" to="/case2" replace label="Progress" />
      <q-route-tab slot="title" icon="chat" to="/case1" replace label="Message" />
      <q-route-tab slot="title" icon="play_circle_outline" to="/showcase/layout/floating-action-button" replace label="Videos" />
      <q-route-tab slot="title" icon="play_for_work" to="/showcase" label="Click me" />
    </q-tabs>

    <div slot="left">
      <!--
        Use <q-side-link> component
        instead of <q-item> for
        internal vue-router navigation
      -->



      <q-list no-border link inset-delimiter>
        <q-list-header>Essential Links</q-list-header>
        <q-item @click="launch('http://quasar-framework.org')">
          <q-item-side icon="accessibility" />
          <q-item-main label="Evaluation" sublabel="Daily Evaluation of the patient" />
        </q-item>
        <q-item @click="launch('http://forum.quasar-framework.org')">
          <q-item-side icon="view_array" />
          <q-item-main label="Progress" sublabel="Progress report of the patient" />
        </q-item>
        <q-item to="/case1">
          <q-item-side icon="chat" />
          <q-item-main label="Message" sublabel="Quasar Lobby" />
        </q-item>
        <q-item @click="launch('https://www.youtube.com/results?search_query=burn+care')">
          <q-item-side icon="play_circle_outline" />
          <q-item-main label="Videos" sublabel="Wound care and daily exercise" />
        </q-item>
      </q-list>

      <q-side-link item to="/showcase">
        <q-item-side icon="account circle" />
        <q-item-main label="Page 1" sublabel="Learn more about it" />
        <q-item-side right icon="thumb_up" />
      </q-side-link>
      <q-side-link item to="/case2">
        <q-item-side icon="school" />
        <q-item-main label="Page 2" sublabel="Learn more about it" />
        <q-item-side right icon="chat" />
      </q-side-link>



    </div>

    <!--
      Replace following <div> with
      <router-view /> component
      if using subRoutes
    -->
    <router-view />
<!--     <div class="layout-padding logo-container non-selectable no-pointer-events">
      <div class="logo" :style="position">
        <img src="~assets/quasar-logo-full.svg">
      </div>
    </div> -->


  </q-layout>
</template>

import './docs-input.styl'

<script>
import {
  dom,
  event,
  openURL,
  QLayout,
  QToolbar,
  QToolbarTitle,
  QBtn,
  QIcon,
  QList,
  QListHeader,
  QItem,
  QItemSide,
  QItemMain,
  QSideLink,
  QTabs,
  QRouteTab,
  QInput
} from 'quasar'

const
  { viewport } = dom,
  { position } = event,
  moveForce = 30,
  rotateForce = 40,
  RAD_TO_DEG = 180 / Math.PI

function getRotationFromAccel (accelX, accelY, accelZ) {
  /* Reference: http://stackoverflow.com/questions/3755059/3d-accelerometer-calculate-the-orientation#answer-30195572 */
  const sign = accelZ > 0 ? 1 : -1
  const miu = 0.001

  return {
    roll: Math.atan2(accelY, sign * Math.sqrt(Math.pow(accelZ, 2) + miu * Math.pow(accelX, 2))) * RAD_TO_DEG,
    pitch: -Math.atan2(accelX, Math.sqrt(Math.pow(accelY, 2) + Math.pow(accelZ, 2))) * RAD_TO_DEG
  }
}

export default {
  name: 'index',
  components: {
    QLayout,
    QToolbar,
    QToolbarTitle,
    QBtn,
    QIcon,
    QList,
    QListHeader,
    QItem,
    QItemSide,
    QItemMain,
    QSideLink,
    QTabs,
    QRouteTab,
    QInput
  },
  data () {
    return {
      orienting: window.DeviceOrientationEvent && !this.$q.platform.is.desktop,
      rotating: window.DeviceMotionEvent && !this.$q.platform.is.desktop,
      moveX: 0,
      moveY: 0,
      rotateY: 0,
      rotateX: 0,
      text: 'text',
      num: 5,
      email: 'email',
      password: 'password'
    }
  },
  computed: {
    position () {
      const transform = `rotateX(${this.rotateX}deg) rotateY(${this.rotateY}deg)`
      return {
        top: this.moveY + 'px',
        left: this.moveX + 'px',
        '-webkit-transform': transform,
        '-ms-transform': transform,
        transform
      }
    }
  },
  methods: {
    launch (url) {
      openURL(url)
    },
    move (evt) {
      const
        {width, height} = viewport(),
        {top, left} = position(evt),
        halfH = height / 2,
        halfW = width / 2

      this.moveX = (left - halfW) / halfW * -moveForce
      this.moveY = (top - halfH) / halfH * -moveForce
      this.rotateY = (left / width * rotateForce * 2) - rotateForce
      this.rotateX = -((top / height * rotateForce * 2) - rotateForce)
    },
    rotate (evt) {
      if (evt.rotationRate &&
          evt.rotationRate.beta !== null &&
          evt.rotationRate.gamma !== null) {
        this.rotateX = evt.rotationRate.beta * 0.7
        this.rotateY = evt.rotationRate.gamma * -0.7
      }
      else {
        /* evt.acceleration may be null in some cases, so we'll fall back
           to evt.accelerationIncludingGravity */
        const
          accelX = evt.acceleration.x || evt.accelerationIncludingGravity.x,
          accelY = evt.acceleration.y || evt.accelerationIncludingGravity.y,
          accelZ = evt.acceleration.z || evt.accelerationIncludingGravity.z - 9.81,
          rotation = getRotationFromAccel(accelX, accelY, accelZ)

        this.rotateX = rotation.roll * 0.7
        this.rotateY = rotation.pitch * -0.7
      }
    },
    orient (evt) {
      if (evt.beta === null || evt.gamma === null) {
        window.removeEventListener('deviceorientation', this.orient, false)
        this.orienting = false

        window.addEventListener('devicemotion', this.rotate, false)
      }
      else {
        this.rotateX = evt.beta * 0.7
        this.rotateY = evt.gamma * -0.7
      }
    }
  },
  mounted () {
    this.$nextTick(() => {
      if (this.orienting) {
        window.addEventListener('deviceorientation', this.orient, false)
      }
      else if (this.rotating) {
        window.addEventListener('devicemove', this.rotate, false)
      }
      else {
        document.addEventListener('mousemove', this.move)
      }
    })
  },
  beforeDestroy () {
    if (this.orienting) {
      window.removeEventListener('deviceorientation', this.orient, false)
    }
    else if (this.rotating) {
      window.removeEventListener('devicemove', this.rotate, false)
    }
    else {
      document.removeEventListener('mousemove', this.move)
    }
  }
}
</script>

<style lang="stylus">
.logo-container
  width 255px
  height 242px
  perspective 800px
  position absolute
  top 50%
  left 50%
  transform translateX(-50%) translateY(-50%)
.logo
  position absolute
  transform-style preserve-3d
</style>
