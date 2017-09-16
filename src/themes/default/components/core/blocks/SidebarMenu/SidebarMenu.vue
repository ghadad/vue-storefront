<template>
    <div class="sidebar-menu" :class="{ active: isOpen }">
        <div class="row">
            <div class="col-md-12 close end-xs" @click="closeMenu">
                <i class="material-icons p15">close</i>
            </div>
        </div>
        <div class="row">
            <div class="col-md-12">
                <ul>
                    <li>
                        <router-link to="/" exact>Home</router-link>
                    </li>
                </ul>
            </div>
        </div>
    </div>
</template>

<script>
import { coreComponent } from 'lib/themes'

import EventBus from 'src/event-bus/event-bus'

export default {
  data () {
    return {
      isOpen: false
    }
  },
  created () {
    const self = this
    EventBus.$on('toggle-sidebar-menu', () => {
      self.isOpen = !self.isOpen
    })
  },
  methods: {
    closeMenu () {
      this.isOpen = false
      EventBus.$emit('toggle-overlay')
    }
  },
  mixins: [coreComponent('core/blocks/SidebarMenu/SidebarMenu')]
}
</script>

<style scoped>
.sidebar-menu {
    position: absolute;
    height: 100vh;
    width: 350px;
    background: #F2F2F2;
    top: 0;
    left: -350px;
    overflow: hidden;
}
.sidebar-menu.active {
    left: 0;
}
.close {
    cursor: pointer;
    background: white;
    text-align: right;
    display: inline-flex;
}
</style>