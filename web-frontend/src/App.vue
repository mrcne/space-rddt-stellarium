// Stellarium Web - Copyright (c) 2018 - Noctua Software Ltd
//
// This program is licensed under the terms of the GNU AGPL v3, or
// alternatively under a commercial licence.
//
// The terms of the AGPL v3 license can be found in the main directory of this
// repository.

<template>

<v-app>
  <v-navigation-drawer v-model="nav" app stateless width="300">
    <v-layout column fill-height>
      <v-list dense>
        <v-expansion-panels
         v-model="panel"
        >
          <v-expansion-panel >
            <v-expansion-panel-header>What the Duck?!</v-expansion-panel-header>
            <v-expansion-panel-content>
              <p>Our project goal is to raise awareness about space debris.</p>
              <p>Contrary to popular beliefs, space around Earth is far from empty.</p>
              <p>We want to counter the “out of sight, out of mind” careless approach of the general public towards the issue of space debris. In order to make it memorable, entertaining and funny, we decided to show space debris from an Earthling’s perspective but with a twist: we have marked known space debris with oversized rubber duckies.</p>
            </v-expansion-panel-content>
          </v-expansion-panel>
          <v-expansion-panel>
            <v-expansion-panel-header>How did trash end up there?</v-expansion-panel-header>
            <v-expansion-panel-content>Space debris (also known as space junk, space pollution, space waste, space trash, or space garbage) is defunct artificial objects in space—principally in Earth orbit—which no longer serve a useful function. These include derelict spacecraft—nonfunctional spacecraft and abandoned launch vehicle stages—mission-related debris, and particularly numerous in Earth orbit, fragmentation debris from the breakup of derelict rocket bodies and spacecraft. In addition to derelict man-made objects left in orbit, other examples of space debris include fragments from their disintegration, erosion and collisions or even paint flecks, solidified liquids expelled from spacecraft, and unburned particles from solid rocket motors. Space debris represents a risk to spacecraft.
              <br /><br />
              <a target="_blank" href="https://en.wikipedia.org/wiki/Space_debris">Read more on Wikipedia</a>
            </v-expansion-panel-content>
          </v-expansion-panel>
          <v-expansion-panel>
            <v-expansion-panel-header>Space debris detection technologies</v-expansion-panel-header>
            <v-expansion-panel-content>Two complementary technologies exist for space debris tracking: optical tracking with lasers or telescopes equipped with event-driven cameras and radar tracking with phased-array radars.
              Event-driven cameras are a special type of digital cameras that - contrary to well-known CCD cameras in our smartphones or DSLRs - only register the pixels seeing movement which greatly reduces readout times and the amount of data generated.
            </v-expansion-panel-content>
          </v-expansion-panel>
          <v-expansion-panel>
            <v-expansion-panel-header>Space Debris Elimination (SpaDE)</v-expansion-panel-header>
            <v-expansion-panel-content>The amount of debris in low Earth orbit (LEO) has increased rapidly over the last twenty years. This prevalence of debris increases the likelihood of cascading collisions that cause the debris generation rate to outstrip the rate at which debris deorbits, falling into the atmosphere and burning up. This accumulation creates debris belts that render many orbits unusable. Current strategies emphasize debris mitigation, as there is no practical method for debris removal. Raytheon BBN Technologies (BBN) and the University of Michigan will study the Space Debris Elimination (SpaDE) system to remove debris from orbit by firing focused pulses of atmospheric gases into the path of targeted debris. These pulses will increase drag sufficiently to cause the deorbit rate to exceed the debris generation rate. The pulses themselves will fall back into the atmosphere, leaving no residual trace in orbit to interfere with LEO satellites. In contrast to other proposed methods, SpaDE is failsafe, in that it places no solid material in orbit where a malfunction could create new debris. This project will conduct technology risk reduction analyses and modeling. The research will produce an academic paper and presentation describing the technical results and providing the foundation for future work, to include prototyping, field experiments and ultimately deployment of a SpaDE system.
              <br /><br />
              Read more on:

              <a target="_blank" href="https://data.nasa.gov/dataset/Space-Debris-Elimination-SpaDE-/x9yp-8wsa">https://data.nasa.gov/dataset/Space-Debris-Elimination-SpaDE-/x9yp-8wsa</a>
            </v-expansion-panel-content>
          </v-expansion-panel>
          <v-expansion-panel>
            <v-expansion-panel-header>It looks like Stellarium Web</v-expansion-panel-header>
            <v-expansion-panel-content>
              Because it's based on <a target="_blank" href="https://github.com/Stellarium/stellarium-web-engine">Stellarium Web Engine</a> and licenced under AGPL-3.0. Source code is <a target="_blank" href="https://github.com/mrcne/space-rddt-stellarium">here</a>
            </v-expansion-panel-content>
          </v-expansion-panel>
        </v-expansion-panels>
        <template v-for="(item,i) in menuItems">
          <template v-if="$store.state[item.store_show_menu_item] === false"></template>
          <v-subheader v-else-if="item.header" v-text="item.header" class="grey--text text--darken-1" :key="i"/>
          <v-divider class="divider_menu" v-else-if="item.divider" :key="i"/>
          <v-list-item v-else-if="item.switch" @click.stop="toggleStoreValue(item.store_var_name)" :key="i">
            <v-list-item-action>
              <v-switch value :input-value="getStoreValue(item.store_var_name)" label=""></v-switch>
            </v-list-item-action>
            <v-list-item-content>
              <v-list-item-title>{{ item.title }}</v-list-item-title>
            </v-list-item-content>
          </v-list-item>
          <template v-else>
            <v-list-item v-if='item.link' target="_blank" rel="noopener" :href='item.link' :key="i">
              <v-list-item-icon><v-icon>{{ item.icon }}</v-icon></v-list-item-icon>
              <v-list-item-title v-text="item.title"/>
              <v-icon disabled>mdi-open-in-new</v-icon>
            </v-list-item>
            <v-list-item v-else-if='item.footer===undefined' @click.stop="toggleStoreValue(item.store_var_name)" :key="i">
              <v-list-item-icon><v-icon>{{ item.icon }}</v-icon></v-list-item-icon>
              <v-list-item-title v-text="item.title"/>
            </v-list-item>
          </template>
        </template>
      </v-list>
      <template v-for="(item,i) in menuComponents">
        <component :is="item" :key="i"></component>
      </template>
      <v-spacer></v-spacer>
      <v-list dense>
        <v-divider class="divider_menu"/>
        <template v-for="(item,i) in menuItems">
          <v-list-item v-if='item.footer' @click.stop="toggleStoreValue(item.store_var_name)" :key="i">
            <v-list-item-icon><v-icon>{{ item.icon }}</v-icon></v-list-item-icon>
            <v-list-item-title v-text="item.title"/>
          </v-list-item>
        </template>
      </v-list>
    </v-layout>
  </v-navigation-drawer>

  <v-main>
    <v-container class="fill-height" fluid style="padding: 0">
      <div id="stel" v-bind:class="{ right_panel: $store.state.showSidePanel }">
        <div style="position: relative; width: 100%; height: 100%">
          <component v-bind:is="guiComponent"></component>
          <canvas id="stel-canvas" ref='stelCanvas'></canvas>
        </div>
      </div>
    </v-container>
  </v-main>
  <cookie-law theme="dark-lime"></cookie-law>

</v-app>

</template>

<script>

import _ from 'lodash'
import Gui from '@/components/gui.vue'
import GuiLoader from '@/components/gui-loader.vue'
import swh from '@/assets/sw_helpers.js'
import Moment from 'moment'
import CookieLaw from 'vue-cookie-law'

export default {
  data (context) {
    return {
      menuItems: [
        { divider: true }
      ].concat(this.getPluginsMenuItems()).concat([
        { title: this.$t('View Settings'), icon: 'mdi-settings', store_var_name: 'showViewSettingsDialog', store_show_menu_item: 'showViewSettingsMenuItem' },
        { title: this.$t('Data Credits'), footer: true, icon: 'mdi-copyright', store_var_name: 'showDataCreditsDialog' }
      ]),
      menuComponents: [].concat(this.getPluginsMenuComponents()),
      guiComponent: 'GuiLoader',
      startTimeIsSet: false,
      initDone: false,
      panel: 0,
      dataSourceInitDone: false
    }
  },
  components: { Gui, GuiLoader, CookieLaw },
  methods: {
    getPluginsMenuItems: function () {
      let res = []
      for (const i in this.$stellariumWebPlugins()) {
        const plugin = this.$stellariumWebPlugins()[i]
        if (plugin.menuItems) {
          res = res.concat(plugin.menuItems)
        }
      }
      return res
    },
    getPluginsMenuComponents: function () {
      let res = []
      for (const i in this.$stellariumWebPlugins()) {
        const plugin = this.$stellariumWebPlugins()[i]
        if (plugin.menuComponents) {
          res = res.concat(plugin.menuComponents)
        }
      }
      return res
    },
    toggleStoreValue: function (storeVarName) {
      this.$store.commit('toggleBool', storeVarName)
    },
    getStoreValue: function (storeVarName) {
      return _.get(this.$store.state, storeVarName)
    },
    setStateFromQueryArgs: function () {
      // Check whether the observing panel must be displayed
      this.$store.commit('setValue', { varName: 'showSidePanel', newValue: this.$route.path.startsWith('/p/') })

      // Set the core's state from URL query arguments such
      // as date, location, view direction & fov
      var that = this

      if (!this.initDone) {
        this.$stel.core.time_speed = 1
        let d = new Date()
        if (this.$route.query.date) {
          d = new Moment(this.$route.query.date).toDate()
          this.$stel.core.observer.utc = d.getMJD()
          this.startTimeIsSet = true
        }

        if (this.$route.query.lng && this.$route.query.lat) {
          const pos = { lat: Number(this.$route.query.lat), lng: Number(this.$route.query.lng), alt: this.$route.query.elev ? Number(this.$route.query.elev) : 0, accuracy: 1 }
          swh.geoCodePosition(pos, that).then((loc) => {
            that.$store.commit('setCurrentLocation', loc)
          }, (error) => { console.log(error) })
        }

        this.$stel.core.observer.yaw = this.$route.query.az ? Number(this.$route.query.az) * Math.PI / 180 : 0
        this.$stel.core.observer.pitch = this.$route.query.alt ? Number(this.$route.query.alt) * Math.PI / 180 : 30 * Math.PI / 180
        this.$stel.core.fov = this.$route.query.fov ? Number(this.$route.query.fov) * Math.PI / 180 : 120 * Math.PI / 180

        this.initDone = true
      }

      if (this.$route.path.startsWith('/skysource/')) {
        const name = decodeURIComponent(this.$route.path.substring(11))
        console.log('Will select object: ' + name)
        return swh.lookupSkySourceByName(name).then(ss => {
          if (!ss) {
            return
          }
          let obj = swh.skySource2SweObj(ss)
          if (!obj) {
            obj = this.$stel.createObj(ss.model, ss)
            this.$selectionLayer.add(obj)
          }
          if (!obj) {
            console.warning("Can't find object in SWE: " + ss.names[0])
          }
          swh.setSweObjAsSelection(obj)
        }, err => {
          console.log(err)
          console.log("Couldn't find skysource for name: " + name)
        })
      }
    }
  },
  computed: {
    nav: {
      get: function () {
        return this.$store.state.showNavigationDrawer
      },
      set: function (v) {
        if (this.$store.state.showNavigationDrawer !== v) {
          this.$store.commit('toggleBool', 'showNavigationDrawer')
        }
      }
    },
    storeCurrentLocation: function () {
      return this.$store.state.currentLocation
    }
  },
  watch: {
    storeCurrentLocation: function (loc) {
      const DD2R = Math.PI / 180
      this.$stel.core.observer.latitude = loc.lat * DD2R
      this.$stel.core.observer.longitude = loc.lng * DD2R
      this.$stel.core.observer.elevation = loc.alt

      // At startup, we need to wait for the location to be set before deciding which
      // startup time to set so that it's night time.
      if (!this.startTimeIsSet) {
        this.$stel.core.observer.utc = swh.getTimeAfterSunset(this.$stel)
        this.startTimeIsSet = true
      }
      // Init of time and date is complete
      this.$store.commit('setValue', { varName: 'initComplete', newValue: true })
    },
    $route: function () {
      // react to route changes...
      this.setStateFromQueryArgs()
    }
  },
  mounted: function () {
    var that = this

    for (const i in this.$stellariumWebPlugins()) {
      const plugin = this.$stellariumWebPlugins()[i]
      if (plugin.onAppMounted) {
        plugin.onAppMounted(that)
      }
    }

    import('@/assets/js/stellarium-web-engine.wasm').then(f => {
      // Initialize the StelWebEngine viewer singleton
      // After this call, the StelWebEngine state will always be available in vuex store
      // in the $store.stel object in a reactive way (useful for vue components).
      // To modify the state of the StelWebEngine, it's enough to call/set values directly on the $stel object
      try {
        swh.initStelWebEngine(that.$store, f.default, that.$refs.stelCanvas, function () {
          // Start auto location detection (even if we don't use it)
          swh.getGeolocation().then(p => swh.geoCodePosition(p, that)).then((loc) => {
            that.$store.commit('setAutoDetectedLocation', loc)
          }, (error) => { console.log(error) })

          that.$stel.setFont('regular', process.env.BASE_URL + 'fonts/Roboto-Regular.ttf', 1.38)
          that.$stel.setFont('bold', process.env.BASE_URL + 'fonts/Roboto-Bold.ttf', 1.38)
          that.$stel.core.constellations.show_only_pointed = false
          that.$stel.core.planets.hints_visible = false
          that.$stel.core.stars.hints_visible = false

          that.setStateFromQueryArgs()
          that.guiComponent = 'Gui'
          for (const i in that.$stellariumWebPlugins()) {
            const plugin = that.$stellariumWebPlugins()[i]
            if (plugin.onEngineReady) {
              plugin.onEngineReady(that)
            }
          }

          if (!that.dataSourceInitDone) {
            // Set all default data sources
            const core = that.$stel.core
            core.stars.addDataSource({ url: process.env.BASE_URL + 'skydata/stars' })
            core.skycultures.addDataSource({ url: process.env.BASE_URL + 'skydata/skycultures/western', key: 'western' })
            core.dsos.addDataSource({ url: process.env.BASE_URL + 'skydata/dso' })
            core.landscapes.addDataSource({ url: process.env.BASE_URL + 'skydata/landscapes/guereins', key: 'guereins' })
            core.milkyway.addDataSource({ url: process.env.BASE_URL + 'skydata/surveys/milkyway' })
            core.minor_planets.addDataSource({ url: process.env.BASE_URL + 'skydata/mpcorb.dat', key: 'mpc_asteroids' })
            core.planets.addDataSource({ url: process.env.BASE_URL + 'skydata/surveys/sso/moon', key: 'moon' })
            core.planets.addDataSource({ url: process.env.BASE_URL + 'skydata/surveys/sso/sun', key: 'sun' })
            core.planets.addDataSource({ url: process.env.BASE_URL + 'skydata/surveys/sso/moon', key: 'default' })
            core.comets.addDataSource({ url: process.env.BASE_URL + 'skydata/CometEls.txt', key: 'mpc_comets' })
            // core.satellites.addDataSource({ url: process.env.BASE_URL + 'skydata/tle_satellite.jsonl.gz', key: 'jsonl/sat' })
            core.satellites.addDataSource({ url: 'https://api.theduckening.space/tle_satellites_debris.jsonl.gz', key: 'jsonl/sat' })
          }
        })
      } catch (e) {
        this.$store.commit('setValue', { varName: 'wasmSupport', newValue: false })
      }
    })
  }
}
</script>

<style>

a {
  color: #82b1ff;
}

a:link {
  text-decoration-line: none;
}

.divider_menu {
  margin-top: 8px;
  margin-bottom: 8px;
}

html {
  overflow-y: visible;
}

html, body, #app {
  overflow-y: visible!important;
  overflow-x: visible;
  position: fixed!important;
  width: 100%;
  height: 100%;
  padding: 0!important;
  font-size: 14px;
}

.fullscreen {
  overflow-y: hidden;
  position: fixed;
  width: 100%;
  height: 100%;
  padding: 0!important;
}

.click-through {
  pointer-events: none;
}

.get-click {
  pointer-events: all;
}

.dialog {
  background: transparent;
}

.menu__content {
  background-color: transparent!important;
}

#stel {height: 100%; width: 100%; position: absolute;}
#stel-canvas {z-index: -10; width: 100%; height: 100%;}

.right_panel {
  padding-right: 400px;
}

.v-btn {
  margin-left: 8px;
  margin-right: 8px;
  margin-top: 6px;
  margin-bottom: 6px;
}

.v-application--wrap {
  min-height: 100%!important;
}

.rubber-duck {
  position: absolute;
  z-index: 1000;
  animation: rubber-duck-spin infinite 60s linear;
  top: 150px;
}
.rubber-duck img {
  width: 50px;
}

.v-expansion-panel.v-item--active button {
  color: #f2c802;
  font-weight: bold;
}

.theme--dark.v-expansion-panels .v-expansion-panel{
  background: none!important;
  border: none!important;
}

.Cookie.Cookie {
  position: inherit;
}

@keyframes rubber-duck-spin {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }

  0%,
  100% {
    left: 0;
  }

  50% {
    left: 100%;
  }
}

</style>
