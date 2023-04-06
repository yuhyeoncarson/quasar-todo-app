<template>
  <q-layout view="lHh lpR fFf">
    <q-header class="bg-primary text-white">
      <q-toolbar>
        <q-btn
          dense
          flat
          round
          icon="menu"
          @click="isDrawerOpen = !isDrawerOpen"
        />
      </q-toolbar>
      <div class="q-pa-lg">
        <div class="text-h4 text-weight-medium">What To Do Today</div>
        <div>Today is {{ date }}.</div>
      </div>
    </q-header>

    <q-drawer
      v-model="isDrawerOpen"
      show-if-above
      :width="200"
      :breakpoint="500"
    >
      <q-scroll-area class="fit">
        <q-list padding class="menu-list">
          <q-item to="/" clickable v-ripple>
            <q-item-section avatar>
              <q-icon name="list" />
            </q-item-section>

            <q-item-section> Home </q-item-section>
          </q-item>

          <q-item to="/important" active clickable v-ripple>
            <q-item-section avatar>
              <q-icon name="star" />
            </q-item-section>

            <q-item-section> Important </q-item-section>
          </q-item>

          <q-item clickable v-ripple>
            <q-item-section avatar>
              <q-icon name="help" />
            </q-item-section>

            <q-item-section> How To Use </q-item-section>
          </q-item>
        </q-list>
      </q-scroll-area>
    </q-drawer>

    <q-page-container>
      <router-view v-slot="{ Component }">
        <KeepAlive>
          <component :is="Component" />
        </KeepAlive>
      </router-view>
    </q-page-container>
  </q-layout>
</template>

<script>
import { date } from "quasar";
import { ref } from "vue";

export default {
  data() {
    return {
      isDrawerOpen: false,
    };
  },

  computed: {
    date() {
      const timeStamp = Date.now();
      return date.formatDate(timeStamp, "dddd MMMM D");
    },
  },
};
</script>
