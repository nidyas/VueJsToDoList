<script>
import sidebarklink from './sidebarklink.vue'
import { collapsed, toggleSidebar, sidebarWidth } from './state'

export default {
  props: {},
  components: { sidebarklink },
  setup() {
    return { collapsed, toggleSidebar, sidebarWidth }
  }
}
</script>

<template>
  <div class="sidebar" :style="{ width: sidebarWidth }">
    <h1>
      <span v-if="collapsed">
        <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="30" height="30" />
      </span>
      <span v-else>Welcome Friend!</span>
    </h1>

    <sidebarklink to="/" icon="fas fa-home">Home</sidebarklink>
    <sidebarklink to="/dashboard" icon="fas fa-columns">Dashboard</sidebarklink>
    <sidebarklink to="/analytics" icon="fas fa-chart-bar">Analytics</sidebarklink>
    <sidebarklink to="/friends" icon="fas fa-users">Friends</sidebarklink>
    <sidebarklink to="/image" icon="fas fa-image">Images</sidebarklink>

    <span
      class="collapse-icon"
      :class="{ 'rotate-180': collapsed }"
      @click="toggleSidebar"
    >
      <i class="fas fa-angle-double-left" />
    </span>
  </div>
</template>

<style>
:root {
  --sidebar-bg-color: #1e293b;
  --sidebar-item-hover: #41B883;
  --sidebar-item-active: #41B883;
}
</style>

<style scoped>
.sidebar {
  color: rgb(255, 252, 252);
  background-color: var(--sidebar-bg-color);

  float: left;
  position: fixed;
  z-index: 1;
  top: 0;
  left: 0;
  bottom: 0;
  padding: 0.5em;

  transition: 0.3s ease;

  display: flex;
  flex-direction: column;
}

.sidebar h1 {
  height: 2.5em;
}

.collapse-icon {
  position: absolute;
  bottom: 0;
  padding: 0.75em;

  color: rgba(255, 255, 255, 0.7);

  transition: 0.2s linear;
}

.rotate-180 {
  transform: rotate(180deg);
  transition: 0.2s linear;
}
</style>