<template lang="html">
  <aside>
    <div class="columns is-marginless">
      <div class="column">
        <h1 class="title has-text-warning is-marginless">Dozzle</h1>
      </div>
      <div class="column is-narrow has-text-right is-hidden-mobile">
        <router-link
          :to="{ name: 'settings' }"
          active-class="is-active"
          class="button is-small is-rounded is-settings-control"
        >
          <span class="icon">
            <icon name="cog"></icon>
          </span>
        </router-link>
      </div>
    </div>
    <p class="menu-label is-hidden-mobile">Containers</p>
    <ul class="menu-list is-hidden-mobile">
      <li v-for="item in containers">
        <router-link
          :to="{ name: 'container', params: { id: item.id, name: item.name } }"
          active-class="is-active"
          :title="item.name"
        >
          <div class="hide-overflow">
            <span
              @click.stop.prevent="appendActiveContainer(item)"
              class="icon is-small will-append-container"
              :class="{ 'is-active': activeContainersById[item.id] }"
            >
              <icon name="pin"></icon>
            </span>
            {{ item.name }}
          </div>
        </router-link>
      </li>
    </ul>
  </aside>
</template>

<script>
import { mapActions, mapGetters, mapState } from "vuex";

import Icon from "./Icon";

export default {
  props: [],
  name: "SideMenu",
  components: {
    Icon,
  },
  data() {
    return {};
  },
  computed: {
    ...mapState(["containers", "activeContainers"]),
    ...mapGetters(["activeContainersById"]),
  },
  methods: {
    ...mapActions({
      appendActiveContainer: "APPEND_ACTIVE_CONTAINER",
    }),
  },
};
</script>
<style scoped lang="scss">
aside {
  padding: 1em;
  height: 100vh;
  overflow: auto;
  position: fixed;
  width: inherit;

  .hide-overflow {
    text-overflow: ellipsis;
    white-space: nowrap;
    overflow: hidden;
  }

  .burger.is-white {
    color: #fff;
  }

  .is-hidden-mobile.is-active {
    display: block !important;
  }
}

.will-append-container.icon {
  transition: transform 0.2s ease-out;
  &.is-active {
    pointer-events: none;
    color: #00d1b2;
  }
  .router-link-exact-active & {
    visibility: hidden;
  }
}
</style>
